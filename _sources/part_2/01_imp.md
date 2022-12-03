# Intelligent Music Production

Intelligent music production is concerned with the design of systems that provide assistance in the process of creating an audio production {cite}`IMPbook19`.
As introduced in the previous section, the music production process encompasses a wide range of tasks and often places a significant burden on the creator with regards to their knowledge in using the available tools. 
Even for expert users the process of creating a professional production is often time consuming. This reality motivates intelligent music production. 
These systems can provide assistance in many different ways, for example by simply providing insights or helpful suggestions or, on the other end of the spectrum, fully automating the process of manipulating many different control parameters across a multitrack project {cite}`moffat2019approaches`.

For nearly 50 years there has been an interest in the creation of systems capable of automating aspects of audio engineering. One of the earliest such systems was presented in 1975 at the AES Convention in Los Angeles {cite}`dugan1975automatic`. This work presented a system for automatic microphone mixing that aimed to control the gain of multiple microphones for speech adaptively by monitoring the level of other microphones with the goal of reducing feedback. These mixers, which have developed through the years and are still in use in the industry, are intended to give straightforward control over the volume of several channels in situations where a skilled audio engineer is not necessary. The limited control and versatility of these early automatic leveling systems left open the question of how to construct more powerful systems capable of automating more aspects of the music production process. 

Interest in this area was renewed many years layer when {cite}`pachet2000fly` proposed a system that allowed listeners to adjust the spatialization of a multitrack mix while meeting a set of constraints set by the audio engineer. This work framed multitrack mixing as an optimization problem, which is a paradigm that has remained influential in the field. As research has developed in intelligent music production, existing approaches are often categorized into three predominant approaches namely, knowledge-based systems, machine learning-based systems and deep learning-based systems {cite}`moffat2019approaches`.


## Knowledge-based Systems

The earliest works posed various multitrack mixing tasks as an optimisation problem that aimed at reducing perceptual masking. The expert knowledge was used to define certain rules that controlled the system to function in the desired manner as shown in figure\ref{fig:knowledge_based}. Most of these systems had two signal paths: the main signal path, which applied the transformation, and the side-chain, that aimed at analysing and extracting features from the incoming signal and generating conditional information that directed the main signal path to apply the transformation in a specific manner. The main signal path was optimised based on an optimisation algorithm or a rule base. Most of these systems were based on the assumption that perceptual models used for masking were representative of human perception and the set of underlying rules and constraints truly aligned with the internal goal of mixing engineers.

In 2007, an autonomous system for panning multitracks in a multitrack mixture was proposed {cite}`gonzalez2007automatic`. Through a straightforward prioritisation structure and a filter bank of K filters that assess the energy inside each band of each input, this method seeks to lessen spectral masking among K input tracks. With the intention of eliminating spectral masking by spacing apart sources with comparable spectral content, these values are then utilised to guide the panning of each source over various panning steps in the stereo field. Thereafter, other tasks associated with multitrack mixing like balance {cite}`perez2009automatic` equalisaion {cite}`perez-gonzalez2009automatic`, delay correction {cite}`perez2008determination` were also optimised in a similar way. Though these systems were state-of-the-art at that time, they still lacked versatility to be able to cater to the entire spectrum of the real world projects and were very sensitive to parameter tuning.

The next few years saw attempts in improving the performance and accuracy of perceptual models. Some researchers also examined approaches that sought to achieve an equal loudness criteria across input channels were also examined, in addition to the objective of decreasing spectral masking within a mix {cite}`perez-gonzalez2009automatic, mansbridge2012implementation, ward2012multitrack, fenton2018automatic`. More thorough examination of the mixing practices were also conducted by some researchers to improve the rule base, thus improving the performance of knowledge-based systems {cite}`moffat2019approaches`. All in all, these systems produced explainable results but could not adapt well to the complexities of real world projects.


## Classical Machine Learning

With the popularity of machine learning in the early 21st century, some researchers began to explore these directions for multitrack mixing systems. These systems leverage large amounts of parametric data collected from pros to train systems to do a specific task. \citet{kolasinski2008framework} utilised genetic algorithm and extracted audio features for leveling tracks. Scott et al utilized linear dynamical systems to predict time varying gains based on extracted audio features and a dataset of mutlitrack mixes {cite}`scott2011automatic`. Investigations were also made into designing more complex processing units like dynamic range compression {cite}`ramirez2018end, sheng2019feature`, reverberation {cite}`benito2017intelligent, chourdakis2017machine, chourdakis2016automatic`, and equalisation {cite}`mimilakis2020one` which was not possible with knowledge-based systems. However, the lack of availability of enough parametric data (parameter values for the processor along with the dry and processed audio) proved to be a limitation in the further development of this field.

## Deep Learning Systems

The advancement of deep learning has provided a new framework for approaching the multitrack mixing problem. 
Through the use of several layers of parameterized computations, deep learning offers a framework for learning complicated, nonlinear mappings directly from high-dimensional data. 
These methods are often characterised by the use of neural networks with many layers, which is optimized using an appropriate loss function with stochastic gradient descent and backpropagation {cite}`goodfellow2016deep`. This enables that constructing representations that are tailored for the task at hand instead of employing features that are hand-crafted for each sort of input data and task as in earlier machine learning approaches.
This opens the door to learning the complex relationship between the input recordings for a song and the possible mixes that are produced by expert audio engineers. 

%Deep learning based approaches heavily rely on data. However, the lack of availability of copyright-free multitrack data has been the major challenge in designing systems using these approaches. 

Deep learning systems generally either aim to reverse engineering an existing mix, or create a new mix given a set of stems. 
Recent work has demonstrated how to recover the mixing parameters for a multitrack mix given the original stems and the final mixture {cite}`colonel2021reverse`.
In the case of producing mixes, a end-to-end drum mixing system involved re-purposing the well known source separation model architecture of Wave-U-Net to generate drum mixes in time domain {cite}`martinez2021deep`. At the same time, {cite}`steinmetz2021automatic` proposed a differentiable mixing console where they implemented neural proxies of a chain of audio processing units that predict parameters for the mixing console controls and are then applied to individual stems and summed to generate a mix. This model was the first to be able to generate mixes for complete songs with any number of stems. However, it still didn’t always produce mixes in sub par with what a human engineer can, which is potentially due to the limited availability of training data. 

{cite}`martinez2022automatic` propose the idea of using out-of-domain and source separation dataset to train a model to mix. They use wet or processed stems that are easily available and propose a pipeline to normalise the wet audio using effect normalisation schemes that they propose for dynamic range compressor, EQ, Reverb, pan and gain. They then use an adaptive front end to predict the latent representation and feature map of the frequency band which is fed into a latent space mixer, which predicts the mixing mask which is then upsampled to generate the mix. It is noteworthy to mention that they also design a stereo-invariant, perceptually-motivated loss function using a pre-emphasis filter pre-processing which has been found to be very crucial for the mixing task.

### Style transfer

Music mixing is a one-to-many problem. There are various acceptable mixes possible for a given set of stems. Most often a mix engineer communicates with the client to understand what they are looking for in a mix and creates a mix that satisfies these conditions. However, a model trained on a multitrack dataset will generate a mix from the dataset mix distribution and it has no way to know what the client wants. Therefore, an intention-driven music mixing system is crucial to the success of these systems. 

Style transfer has been proposed as one method to enable intention-driven intelligent music production. 
Recent systems have used style transfer, where the user provides a reference recording to guide the process, for tasks such as music mastering {cite}`koo2022end`, control of audio effects {cite}`steinmetz2022style`, as well as mixing {cite}`koo2022music} propose a mixing style transfer system that uses a reference mix to inform the system of the client intention.

## Considerations

Some important considerations for an automatic mixing system include interpretability, controllability, efficiency, permutation invariance, the requirement for specific input taxonomy, ability to handle a varying number of input recordings, fidelity, and the expressivity of the signal manipulation in mix creation. There are a lot of details to unpack there. Let’s introduce these eight considerations as we will keep them in mind as we discuss the details of different approaches in the following sections.

### Interpretability
While it might not be critical to have a fully explainable model in the XAI sense {cite}`bryan2022exploring`, it is often desirable for an automatic mixing system to convey what kind of manipulation is applied to each input recording in the creation of the mix. For example, this can easily be achieved by parameter estimation approaches, but is somewhat problematic for direct transformation approaches. 

### Controllability

Similar to interpretability, a system with a level of controllability will enable the user to not only understand what signal transformations have been applied, but also enable adjustment of these transformations {cite}`huang2020ai`. Again, parameter estimation approaches enable this behavior by default, but direct transformation methods could also achieve controllability if they incorporate specialized conditioning mechanisms in the model.

### Context

Closely related to controllability, although distinct, is the notion of context, or context-aware systems {cite}`lefford2021context`. As discussed in Section 1, context plays a central role in shaping the final outcome in the audio production process. As a result, it is important to consider to what degree an automatic mixing system is capable of understanding and adapting to the context. 

###  Permutation invariance

An important realization is that the input recordings provided to the system are an unordered set. This means that the order in which the recordings are provided to our system should ideally not change the results. Some systems address this by adopting a fixed input taxonomy, but this restricts the system flexibility. Other approaches might deal with this by treating the input recordings as a set, often achieving this with weight sharing across the input recordings. We will discuss this further in the following sections.

### Input taxonomy

As alluded to in the previous point, it is often beneficial to define a fixed input taxonomy. This means the system is trained using a dataset and model where the kind and number of sources that are passed to the system are fixed during training and inference. For example, in a system that mixes drum recordings, the inputs might always be presented to the system as an ordered set: “kick, snare, hi-hat, overhead left, overhead right, tom 1, tom 2”. While this often makes the process of creating an automatic mixing system simpler, it limits the ability of the system to be deployed in real-world scenarios wherein there exists limited structure with regards to the input recordings.

### Number of inputs

Closely related to the input taxonomy is how the system handles a variable number of input recordings. Some systems might handle this by simply defining a maximum number of input recordings, inserting silence when an example contains fewer than the maximum. Other approaches that utilize weight sharing can potentially work around this and adapt to a variable number of sources, even those greater than seen during training since they treat the input recordings as a set and not a fixed vector. 

### Fidelity

In audio engineering providing transformations to the sound that limit noise and distortion is critical. While noise, distortion, and other destructive transformations have applications in music production, the default assumption is that systems for processing audio signals will not impact unwanted artifacts. This is an important consideration as the utility of our automatic mixing system is largely dependent on the ability to produce a desirable mixture to the user that contains no audible artifacts.

### Expressivity

An important consideration is to ensure that the process employed to create a mixture in the automatic mixing system is capable of producing the mix in the dataset. This can be a challenge for parameter estimation models.