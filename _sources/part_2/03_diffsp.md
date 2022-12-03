# Differentiable signal processing

Differentiable signal processing involves the process of applying gradient-based optimization algorithms to control the parameters of some set of signal processing devices.
In practice, this can mean using gradient-based optimization as a method for controlling synthesizers to reproduce reference sounds {cite}`engel2020ddsp,masuda2021synthesizer,shan2022differentiable`, reverse engineering audio effects {cite}`colonel2021reverse, colonel2022reverse`, automatic control of audio effects {cite}`nercessian2020neural, ramirez2021differentiable, steinmetz2022style`, or other audio signal processing applications such as room acoustics {cite}`steinmetz2021filtered`, hearing aids {cite}`tu2021dhasp, drakopoulos2022differentiable`, and echo cancellation {cite}`casebeer2022meta`.
This can involve online optimization applications where the parameters of the device are optimized directly, or training a neural network to predict these control parameters as a function of some external signal. 
Both cases require that we develop specialized techniques for facilitating gradient-based optimization.
This is due to the fact that existing signal processing devices often include non-differentiable, discontinous, recursive, or otherwise problematic operations for applying gradient-based optimization techniques {cite}`steinmetz2022style`. 

```{figure} /assets/figures/ddsp.svg
:name: ddsp
:width: 50%
:align: center

General formulation of the differentiable signal processing problem.
```

The general formulation for neural network control of a signal processing device with differentiable signal processing is illustrated in {numref}`ddsp`. 
Here we have a neural network $f_\theta(\mathbf{x})$ with weights $\theta$ that takes as input an audio signal $\mathbf{x}$ and produces a set of control parameters $\hat{\mathbf{p}}$ that will configure our signal processing device. 
This device is represented as a function $h(\mathbf{x}, \hat{\mathbf{p}})$ that operates on the audio signal according to the supplied control parameters. 
As a result, it will produce a processed signal $\hat{\mathbf{y}}$. 

During training, given an appropriate dataset of desired input-output audio recordings, our goal is then to adjust the weights $\theta$ such that the estimated parameters produce audio that minimizes an error metric or loss $\mathcal{L}$ across all examples in the dataset. 
Applying backpropgation requires that we first compute the gradient of the loss with respect to the output signal $\nabla_{\hat{\mathbf{y}}} \mathcal{L}$, and then compute the gradient of the loss with respect to the estimated control parameters $\nabla_{\hat{\mathbf{p}}} \mathcal{L}$. As shown by the dashed line in {numref}`ddsp`, this requires taking into account the operations within our signal processing device $h$. 
Existing methods for differentiable signal processing are focused on providing techniques for computing $\nabla_{\hat{\mathbf{p}}} \mathcal{L}$ to facilitate this kind of end-to-end learning when we do not have ground truth values for $\mathbf{p}$.


## Automatic differentiation

The predominate approach in facilitating backpropagation through signal processing devices involves explicit gradient computation via automatic differentiation {cite}`griewank1989automatic`. 
In this approach we can leverage the power of automatic differentiation (AD) frameworks, like PyTorch {cite}`paszke2019pytorch`, TensorFlow {cite}`tensorflow2015whitepaper` or JAX {cite}`jax2018github`. 
By implementing the operations of our signal processing device directly in an AD framework we can enable computation of gradients for each operation within signal processing device.
In the context of audio, this approach was popularized by DDSP {cite}`engel2020ddsp`, which proposed a method for automatic control of a harmonic plus noise synthesis model in the reconstruction of monophonic musical instruments. 

While automatic differentiation provides a straightforward method for computing the desired gradients, it places a number of constraints on the signal processing device that we can use. 
It requires foremost that we have access or knowledge to the underlying algorithm implemented in our signal processing device, make this a white-box approach. 
Not only does it require that we have knowledge of the signal processing operations, it also requires that these operations are differentiable, which excludes binary decisions, or other discrete operations. 
Finally, compute cost and efficiency must also be considered. While signal processing devices with recursive operations, such as infinite impulse response filters, are differentiable {cite}`kuznetsov2020differentiable`, the application of these filters in the time domain can be problematic for gradient computation since backpropagation will require serial computation of the gradient at each timestep. This can lead to extremely slow or infeasible gradient computations when operating at audio samples (e.g. 44.1 kHz) {cite}`wright2022grey`.
These limitations motivate alternative strategies for gradient computation that relax some of these constraints.

## Neural proxies

Neural proxies of audio effects enable a black-box approach by first training a neural network to emulate the behavior of the device and then use this continuous and differentiable proxy of the original device during optimization {cite}`steinmetz2021automatic`. 
This does not require that the original signal processing device is differentiable or continuous. It only requires that we can generate input-output examples from this device over the range of its control parameters so we can train a neural network proxy to emulate its behavior.
During training of our control network we can use this proxy to compute gradients. 

Recent work investigated the feasibility of neural proxy hybrids, where the pretrained proxy network is used only during the backward pass and the original signal processing implementation is used in the forward pass both during training and inference {cite}`steinmetz2022style`. 
However, results indicate that this approach does not perform well in comparison as the input-output behavior with respect to the audio effect control parameters is often not sufficiently captured with existing neural proxy implementations. 
While this method provides the benefit of a fully black-box formulation, further work is required in developing the appropriate model architectures for creating accurate emulations of signal processing devices.

## Gradient approximation

Another black-box approach involves estimation of the gradient of the loss with respect to the parameters $\nabla_\mathbf{p} \mathcal{L}$.  {cite}`ramirez2021differentiable` demonstrated how to apply this technique for the control of audio effects across a number of tasks. In their approach they leverage simultaneous perturbation stochastic approximation (SPSA) {cite}`spall1997one`, which provides a more scalable alternative to finite differences.
This approach generally involves generating multiple outputs from the device with a small random perturbation of the parameter values in order to compute a local estimate of the gradient. 

Under the right conditions with appropriate hyperparameter tuning this approach can enable backpropgation to train a neural network for the control of black-box audio effects without the need for a proxy network. 
However, this method has also been shown to struggle with instability and exhibit sensitivity to the hyperparameters selection {cite}`steinmetz2022style`.
In addition, there can be implementation challenges as the black-box audio effects often run only on CPU and may need to have independent state handled. This often requires efficient orchestration between the neural network on GPU and multiprocessing of CPU workers for the audio effect. 