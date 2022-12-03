# Problem Formulation

Generally, an automatic mixing system will take as input a set of $N$ recordings $\mathbf{x_1}, \mathbf{x}_2, ..., \mathbf{x}_N$ each containing $T$ samples. These recordings, when processed and combined, will create the final stereophonic mixture $\mathbf{Y} \in \mathbb{R}^{2 \times T}$. In popular music, the input recordings generally contain isolated recordings of the individual instruments that make up the composition (e.g. vocals, guitar, bass, drums, etc.). In other genres, these recordings may come from microphones placed close to sources within an orchestra or ensemble while they were performing. In electronic productions all of these sources may come from synthesized instruments. It is important to note automatic mixing systems also have applications outside of music, so recordings may constitute multiple speakers in a podcast or the dialogue, sound effects, and score of a film.

As discussed, the process of creating these constituent recordings is largely unstructured, meaning that different productions may feature vastly different recordings in terms of the number of sources and their identity. The task of an automatic mixing system involves analyzing and then manipulating these individual recordings to create a mixture similar to a trained audio engineer. Due to these complexities, there are a number of challenges that arise in constructing an automatic system that can learn from data, which are often addressed by systems in different ways.

```{figure} /assets/figures/types-of-systems.svg
:name: types-of-systems
:alt: Types of systems
:align: center
:width: 120%

Formulations for deep learning based automatic mixing systems.
```

The problem formulation adopted by a particular approach depends primarily on the form of the data that will be used for training the automatic mixing system. The two predominant formulations can are classified as *direct transformation*, where the input recordings are directly mapped to the output mixture, as shown in {numref}`types-of-systems`a, or *parameter estimation*, where the parameters of a mixing console are estimated by a model and then used in a downstream mixing console to produce a mix, as shown in {numref}`types-of-systems`b and c. 
There are two general forms of parameter estimation that depend on the form of the dataset and loss function used. When a dataset of both input recordings and parameter is available we can compute the loss in the parameter space (shown in {numref}`types-of-systems`b) and when parameters not available, only the final mixtures, we can instead compute the loss in the audio domain (shown in {numref}`types-of-systems`c). However the second form requires that the mixing console $h$ is differentiable. We will introduce these formulations in the following subsections in a general sense and discuss their tradeoffs. Then we will discuss the Mix-Wave-U-Net {cite}`martinez2021deep` and Differentiable Mixing Console {cite}`steinmetz2021automatic`, which are examples of these two different formulations.

## Direct Transformation

In the direct transformation approach we consider a dataset of $E$ examples

$$
\mathcal{D} = \{  \mathbf{x}^{(i)}_{1}, \mathbf{x}^{(i)}_{2}, ..., \mathbf{x}^{(i)}_{N}, \mathbf{Y}^{(i)} \}_{i=1}^E,
$$

where each example contains a variable number of recordings $N^{(i)}$ of the form $\mathbf{x}^{(i)}_{1}, \mathbf{x}^{(i)}_{2}, ..., \mathbf{x}^{(i)}_{N}$, along with a mixture of these recordings $\mathbf{Y}^{(i)}$ created by an audio engineer. 
We do not need knowledge of the underlying signal processing devices that were used (audio effects, digital audio workstation, etc.) in this approach. 
We construct a model $f_\theta$ that takes as input the recordings and is trained to produce an estimate of the mix $\hat{\mathbf{Y}}^{(i)}$ that is as close as possible to the corresponding mix in the dataset $\mathbf{Y}^{(i)}$. 
This involves optimizing the parameters of the model $\theta$ according to a loss that measures the difference between the predicted and ground truth mixes. $\mathcal{L}_a(\hat{\mathbf{Y}}^{(i)}, \mathbf{Y}^{(i)})$. This distance is often computed in either the time or frequency domains, or a linear combination of both. 

This formulation makes limited assumptions and depending on the flexibility of $f_\theta$ can enable learning to reproduce common audio effects without any direct supervision or knowledge of these devices beyond the mapping between the input recordings and mixes.
While this approach is desirable due to its limited assumptions and flexibility, this comes with some potential drawbacks. One limitation arises from this flexibility, which can lead to the need for large scale datasets for satisfactory training and generalization. This is of particular importance since in general the availability of even unstructured multitrack data is quite limited. Furthermore, this flexibility can also lead to undesirable signal transformations, namely the introduction of artifacts, which are highly undesirable in the audio engineering context. In addition, both interpretability and controllability are limited in this approach. Users of a system of this nature are unable to both see the control parameters that give rise to the final output mix, and more importantly, they are unable to adapt or modify this mix using traditional control parameters, potentially limiting the utility of the system.

## Parameter Estimation

The limitations of direct transformation approaches motivate parameter estimation approaches that instead construct a model $f_\theta$ to estimate the parameters of a particular mixing console. This mixing console is described by a function $h$ takes a set of $N$ input recordings and parameters for each recording to produce a final stereo mixture $\mathbf{Y} = h(\mathbf{x}_{1}, \mathbf{x}_{2}, ..., \mathbf{x}_{N}, \mathbf{p}_1, \mathbf{p}_2, ..., \mathbf{p}_N)$. In most configurations we assume that the signal processing chain operating on each input is made of the same building blocks, for example a series connection of an equalizer, dynamic range compressor, and artificial reverberation.
Is should be noted that this framing limits the expressivity of the system as compared to the direct transformation approach since we are limited to the capabilities of $h$ when creating a mix. However, it reduces the work that must be done by the model $f_\theta$ and provides a level of interpretability and controllability, since manipulation of the input recordings to create the mixture is handled by a predefined set of signal processing devices described by $h$.

### Parameter Loss

The first variant of the parameter estimation method involves training our system using a loss in the parameter space. In this case we assume we are given a dataset 

$$
    \mathcal{D} = \{ \mathbf{x}^{(i)}_{1}, \mathbf{x}^{(i)}_{2}, ..., \mathbf{x}^{(i)}_{N}, \mathbf{p}^{(i)}_{1}, \mathbf{p}^{(i)}_{2}, ..., \mathbf{p}^{(i)}_{N} \}_{i=1}^E,
$$

that contains the $N$ input recordings and the $K$ parameters of a mixing console for each of these inputs that were selected by an audio engineer to produce a mix.
With this dataset we could design a model that learns to estimate these parameters computing a loss in the parameter space. This formulation is shown in {numref}`types-of-systems`b, where a model $f_\theta$ is trained to estimate control parameters. The weights of the network $\theta$ are then trained according to a loss function $\mathcal{L}_p(\hat{\mathbf{p}}^{(i)}_{1}, \hat{\mathbf{p}}^{(i)}_{2}, ..., \hat{\mathbf{p}}^{(i)}_{N}, \mathbf{p}^{(i)}_{1}, \mathbf{p}^{(i)}_{2}, ..., \mathbf{p}^{(i)}_{N})$ that measures the distance (e.g. mean squared error) between the estimated parameters and the ground truth parameters from the dataset. While this is a potentially desirable formulation since it provides a straightforward training setup, it is problematic for two main reasons.

**Datasets** Foremost is the reality that data of this form is not widely available. While it is possible to collect data of this form, it is challenging due to the diversity of the tools utilized by audio engineers. We could export the settings that describe the mix from digital audio workstation projects, but due to the wide range of digital audio workstations and the audio effect implementations present, defining a singular ontology onto which all mixing parameters can be mapped will require significant effort and is likely to face many edge cases. A route towards constructing a dataset of this form would likely require defining a fixed mixing chain and asking audio engineers to use this to generate training data. However, this results in a significant compromise in data realism.

**Overparameterization** Another consideration for parameter estimation approach is the potential overparameterization of the audio effects and mixing console. An audio effect or signal processing device is overparameterized when there exists many different configurations in the parameter space of the device that result in outputs that are very close in the audio domain. 
This could be close in the audio domain with respect to an established objective metric, such as the time domain error or spectral distance, but also in the perceptual space, which is significantly harder to measure, but more likely to cause effects to be overparameterized. 
This is an issue when using a loss in the parameter space since it is possible for the model to generate parameter predictions that produce a mix close to or similar to the ground truth mix from the dataset but are far apart in the parameter space, and hence penalized during training {cite}`steinmetz2022style`.

### Audio Loss

As a result, existing parameter estimation systems for automatic mixing generally utilize a dataset that contains only input recordings and the stereo mix created by an audio engineer, without any knowledge of the underlying effect implementation or parameter configurations that were used. This approach uses the same dataset formulation as in the direct transformation approach, which addresses the limitations of the parameter space loss. Training then involves the process of learning to map the input recordings to a mix that is as close as possible to the target mix in the dataset according to a predefined error metric $\mathcal{L}_a(\hat{\mathbf{Y}}, \mathbf{Y})$. Often this error metric is the $L_1$ or $L_2$ distance between the mixes in the time domain, or the distance between the magnitude spectrum of the mixes. 

However, as mentioned earlier, this formulation requires that our mixing console, represented by a function $h$, is a continuous and differentiable function.
This is required since computing the gradient of of the loss function with respect to the model parameters $\nabla_\theta \mathcal{L}$ requires computing the gradient of the intermediate operations within the mixing console. 
Unfortunately, this is a non-trivial task. 
As a result, existing parameter estimation methods often focus on designing methods for working around this constraint to enable training. 
Recently, the field of differentiable signal processing has emerged to address these questions. 
In the following section we will introduce the general differentiable signal processing problem. 
Then we will outline existing methods for enabling audio domain losses for training neural networks in controlling audio effects, which has clear applications for automatic mixing systems. 
