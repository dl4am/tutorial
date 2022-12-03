# Future Directions

Thus far in the tutorial we have provided a framework for understanding current approaches to building automatic mixing systems with deep learning and discussed the details and limitations of two existing systems. It should be clear from that these systems are limited in a number of ways leaving open a number of directions for future work. In this section we will identify a few possible directions for future research with the goal of encouraging further advancements in automatic mixing.

## Differentiable signal processing

As discussed previously, differentiable signal processing provides a method to integrate existing signal processing devices, such as audio effects, directly into the end-to-end gradient-based deep learning training framework. This facilitates the ability to build neural networks that inference with audio effects in the context of creating automatic mixing models. While the Differentiable Mixing Console explored this idea in the context of automatic mixing, significant advances in extending techniques in differentiable signal processing have been made. 
For example, recent works have proposed explicitly differentiable implementations of audio effects such as parametric and graphic equalizers {cite}`kuznetsov2020differentiable,nercessian2020neural,colonel2021reverse,colonel2022direct,steinmetz2022style`, artificial reverberation {cite}`steinmetz2021filtered,lee2022differentiable,lyster2022differentiable`, waveshaping distortion {cite}`colonel2022reverse`, as well as dynamic range compression {cite}`steinmetz2022style,wright2022grey,colonel2022approximating`. A clear direction of future work involves the integration of these ideas into a framework similar to DMC with the ability to efficiently extend the expressivity of the mixing console that is controlled by a neural network. 

Beyond leveraging recent advancements in automatic differentiation based approaches, future work also involves extending and improving the black-box gradient methods such as the neural proxy approach and gradient estimation techniques. The development of fundamentally new techniques for black-box gradient estimation in the context of audio effects is also an open area of research that has direct implications for building automatic mixing systems.

## Generative models

We have observed some of the potential limitations of treating the process of creating a multitrack mix as a one-to-one mapping between the input recordings and the mix present within a dataset (i.e. a discriminative model). However, we now know that due to the subjective and largely artistic nature of audio engineering, there always exists multiple valid mixtures for any given set of input recordings. This motivates a generative modeling approach where we construct a model $p(\mathbf{Y} | \mathbf{x}_1,  \mathbf{x}_2,  ..., \mathbf{x}_N )$ that explicitly models the data generation process of producing a mixture given the observed input recordings. Thus far, no generative approaches have been applied to this task, but they could provide an important path forward towards building more powerful automatic mixing systems. Techniques such as generative adversarial networks {cite}`goodfellow2020generative`, variational autoencoder {cite}`kingma2013auto`, autoregressive generative models {cite}`brown2020language`, flow-based models {cite}`rezende2015variational`, and diffusion models {cite}`sohl2015deep, song2019generative, ho2020denoising` all provide applicable frameworks for constructing generative models in the context of automatic mixing systems.  

## Datasets 

As mentioned throughout the tutorial, one of the main challenges in building powerful automatic mixing systems remains the lack of high-quality annotated datasets. Recently, this has been addressed in part by constructing systems that leverage datasets intended for music source separation {cite}`martinez2022automatic`. There has been significant work in developing music source separation datasets and due to the connection between music source separation and multitrack mixing there is the potential to leverage these datasets. In addition, there has been an interest in leveraging the advancements in music source separation models in order to construct multitrack datasets for the purpose of training automatic mixing systems {cite}`ward2017estimating`. However, there are some limitations to this approach. Future work in extending source separation models to separate mixes into more than four sources in addition to audio effect removal or normalization may be required before this method for dataset creation is viable. 

## Audio production representations


A key building block for automatic mixing systems are representations (or features) that capture important information about audio production. 
Unlike many applications for audio representations, in this case we are not focused solely on modeling the content of a recording, but also the stylistic and timbral elements.
Features that capture these elements will be critical for making mixing decisions. 

Recently, there has been growing interest in self-supervised audio representation learning, an approach that has potential applications in intelligent music production. 
Applications such as audio quality assessment (AQA) have recently seen success in leveraging self-supervised audio representations to predict the quality of audio recordings {cite}`manocha2021cdpam, serra2021sesqa`.

In addition, self-supervised techniques have also seen application in constructing of so-called general-purpose audio representations~ {cite}`turian2022hear`. 
These representations are often constructed by first pretraining a model on a self-supervised pretext task and then adapation of the pretrained model to a given task via fine-tuning. 
The application of self-supervised frameworks such as SimCLR {cite}`chen2020simple` and CLIP {cite}`radford2021learning` have seen success in the audio {cite}`wu2022large` and music~ {cite}`spijkervet2021contrastive`, however there has been little work in further adapting these approaches to fit the audio production paradigm. 

For example, some recent works include TimbreCLIP {cite}`jonason2022timbre`, which used a CLIP-like model to learn a shared text-audio embedding space to encode timbre. They demonstrated how they could then use this embedding space to control an equalizer with a text prompt.
Other relevant works include \citep{venkatesh2022word} that similarly leveraged pretrained work s to control an equalizer with semantic term.

In addition, {cite}`steinmetz2022style` demonstrated how a model pretrained on a self-supervised audio effect style transfer task was able to construct a representation that encoded information about audio production style. 
{cite}`koo2022music` recently demonstrated how to leverage the SimCLR framework for learning representations that specifically encode information only about audio effects, which could provide utility in future downstream applications. 
