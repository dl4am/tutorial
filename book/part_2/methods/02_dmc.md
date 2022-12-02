# Differentiable Mixing Console

In contrast to Mix-Wave-U-Net, the Differentiable Mixing Console (DMC) is a parameter estimation approach that explicitly defines the structure of a mixing console and uses a neural network to predict the configuration based on an analysis of the input recordings {cite}`steinmetz2021automatic`. The main architecture consists of three subsystems, an encoder, post-processor, and transformation network. A unique property of this system is that weight-sharing is heavily utilized such that one instance of each of these subsystems is used to produce mixing parameters for each input recording and a context embedding is used to signal to the weight-shared networks the content of the other input when selecting the parameters for a specific input.


```{figure} /assets/figures/dmc.svg
:name: dmc
:align: center

Complete Differentiable Mixing Console with subsystems
```

The differentiable mixing console (DMC) is comprised of three main subsystems, each implemented as a separate neural network module. To construct the complete system, the same instance of these modules are applied to each input recording, enabling weight sharing, which treats the input recordings as an unordered set. The encoder is tasked with extracting relevant features from each input recording. These embeddings are then combined to create a context embedding that captures information across all input recordings in a single embedding. Each input embedding is combined with the context embedding and passed to the post-processor that maps these inputs to the control parameter space of the mixing console for the respective channel of the mixing console. Finally, a transformation network takes the audio signal from the respective input recording along with the predicted parameters to process the manipulated recording. The final stereo mixture is then created by the summation of all of the manipulated recordings. 

This provides a number of unique benefits, namely permutation invariance with respect to the ordering of the input recordings, but more importantly the ability to adapt to a variable number of tracks and no assumed taxonomy for the input sources. This means that the system is capable of adapting to real-world scenarios wherein the number of inputs and their identity is highly variable. This contrasts with Mix-Wave-U-Net which accepts a fixed number and ordering of the input tracks. While this works in cases where the training dataset obeys a strict structure, it places a limitation on scenarios where the model can be applied. Now we will walk through each of the subsystems describing the overall operation of the system. 

## Encoder

In order to estimate mixing parameters for each input recording the model must first extract relevant information from each recording. To achieve this, DMC utilizes a standard CNN operating on spectrograms, in this case the VGGish architecture {cite}`hershey2017cnn`. This encoder produces one embedding for approximately each second of the input signal. This means that a series of embeddings will be produced for each input recording. To aggregate information over time the mean of these embeddings is computed, which equally weights each time step. More sophisticated temporal aggregation approaches could be considered here, however the original implementation considers the mean as it is the simplest aggregation method.

It is important to note that the parameter estimation is a cross-dependant process that must consider the content of all other tracks when making a decision about the parameters for a single track. To address this DMC introduces a context embedding. The context embedding is simply the mean across all aggregated input recording embeddings. This creates a representation that captures all of the content present within the mix. Again more sophisticated aggregation methodologies could be considered, however the mean represents one of the most straightforward methods for permutation invariant aggregation. After computing the embedding for each input recording and using these embeddings to produce the context embedding (there is only a single context embedding for each mix), this set of embeddings will be passed on to the post-processor module in order to project the embeddings from each track into the parameter space of each channel of the mixing console.

## Post-processor

Once the input embeddings and context embedding have been generated, it is the task of the post-processor to map these embeddings to the control parameters for each effect that will operate on each input recording. Again, the weights of the post-process are shared across all input recordings. In effect this means that the post-processor, which is implemented as a multi-layer perception (MLP) will be run once for each input recording, where the input to the post-processor is the concatenation of the respective input embedding along with the global content embedding. Each time the post-processor is called one set of control parameters is generated, which will then be passed onto the differentiable mixing console in order to generate the mix.

## Transformation network

One key contribution of this work was the introduction of the concept of *proxy networks*. Since our goal is to train an automatic mixing system in an end-to-end fashion using a loss computed in the audio domain (as opposed to the parameter space), this requires a method for computing gradients through each operation of the mixing console. In practice this entails computing gradients for potentially complex signal processing devices such as dynamic range compressors and artificial reverberators, which either might not be differentiable, have intractable gradients, or be black-box in nature. The proxy network approach provides an alternative by first training a neural network to emulate the behavior of the mixing console, which can then be used as a proxy during optimization.

```{figure} /assets/figures/channel-strip.svg
:name: channel-strip
:align: center

Audio effects and their control parameters in the proposed transformation network.
```

In the original work, the authors construct two variants of what they call the transformation network, which is tasked with emulating the set of effects in each channel of the mixing console.
In the first case, they use a simple transformation network that consists of only gain and panning, which can be implemented as differentiable components.
In the second formulation they leverage a pretrained neural network that was trained to emulate the behavior of a chain of audio effects (equalisation, compression, and reverberation), as a function of their control parameters. This formulation is shown in {numref}`channel-strip`. 

```{figure} /assets/figures/proxy-network.svg
:name: proxy-network
:align: center

Proxy network architecture implemented as a temporal convolution network (TCN)
```

To construct the proxy networks they leverage recent work in neural audio effects {cite}`damskagg2019real`. 
The basic architecture is shown in {numref}`proxy-network`.
At the high level (left) the network is composed of a number of temporal convolutional network (TCN) {cite}`bai2018empirical` blocks along with a conditioning network implemented with an MLP. 
Each TCN block consists of a 1-d convolution, batch normalization, and a nonlinear activation function. 
In order to adapt the behavior of the network as a function of the control parameters feature-wise linear modulation {cite}`perez2018film` is used. 
This technique enables adaptation by dynamically shifting and scaling the intermediate activations of the network as a function of the control parameters $\mathbf{p}$.
This modulation technique is shown in {numref}`proxy-network` (right), where the latent embedding $\mathbf{z}$ produced by the MLP is projected to a set of scaling $\bm{\gamma}_n$ and shifting $\bm{\beta}_n$ parameters. These parameters operate on the output of the batch normalized signal to produce a modulated signal before passing through the nonlinearaity, which is implemented with a Parametric ReLU {cite}`he2015delving`.

