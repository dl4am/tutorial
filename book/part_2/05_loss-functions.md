# Loss Functions

The loss function is a critical component of any deep learning system. While there are many considerations regarding loss functions for applications in audio signal processing, we will discuss in this section the most important aspects that are relevant for constructing an automatic mixing system. 
Most audio-focused loss functions can generally be separated into those that compute a distance between waveforms in the time domain or those that compute a distance in the spectral domain. 
In general, we will consider a loss function $\mathcal{L}$ that operates on the output of the automatic mixing systems $\mathbf{y}$ and the ground truth target mix $\mathbf{y}$, both of which are stereo audio signals $ \{ \hat{\mathbf{y}}, \mathbf{y} \} \in \mathbb{R}^{2 \times T}$

## Time Domain

A standard approach is to consider the mean-squared error between the stereo waveforms. This amounts to first computing the sample-wise mean-squared error for each of the $N$ samples on each channel and then averaging across the error of each of the two channels

$$ \label{eq:mse}
    \mathcal{L}_{\text{MSE}}({\hat{\mathbf{y}}},\mathbf{y}) = \frac{1}{2N} \sum_{i=1}^{2} \sum_{j=1}^{N} {|{\hat{\mathbf{y}}}_{i,j} - \mathbf{y}_{i,j}|}^2.
$$

This is perhaps the simplest loss function we can utilize, but as a result it has some limitations. We know that the human auditory system does not compare sounds in this way and therefore this approach is likely to overemphasize small differences in phase between the signals, which may not be perceptual. This is the predominate motivation for frequency domain loss functions.

## Frequency Domain


Frequency domain loss functions aim to address the limitations of time domain losses by measuring the distance between two audio signal using a comparison of the time-varying magnitude spectrum. 
The general formulation involves computing the short-time Fourier transform (STFT), taking the magnitude of each channel $i$ of the estimated signal $ \hat{\mathbf{Y}}_i = |\text{STFT}(\hat{\mathbf{y}}_i)| $  and the target signal $\mathbf{Y}_i = |\text{STFT}(\hat{\mathbf{y}}_i)|$ where $\{ \hat{\mathbf{Y}}_i, \mathbf{Y}_i \in \mathbb{R}^{F \times K}$ with $F$ as the number of frequency bins and $K$ the number of time frames. 
Then we measure the mean-squared ($L_2$) or mean-absolute ($L_1$) error between these matrices. 

$$ \label{eq:stft}
    \mathcal{L}_{\text{STFT}}({\hat{\mathbf{Y}}},\mathbf{Y}) = \frac{1}{2KF}  \sum_{i=1}^{2}\sum_{k=1}^{K} \sum_{f=1}^{F} \Big(  |\text{STFT}(\hat{\mathbf{y}}_i)|[f,k] - |\text{STFT}(\mathbf{y}_i)| [f,k] \Big)^2.
$$
xw
However, using a single configuration of transform parameters (window size, hop size, etc.) is known to bias this error measurement due to the fixed time-frequency resolution. 
To address this, recent approaches have adopted the multi-resolution or multi-scale STFT loss function {cite}`engel2020ddsp, yamamoto2020parallel`. 
This approach extends the existing frequency domain loss function by consider the average error across a range of different time-frequency resolutions. 
We can achieve this by computing the average error at $M$ time-frequency resolutions

$$ \label{eq:mrstft}
    \mathcal{L}_{\text{MR-STFT}}({\hat{\mathbf{Y}}},\mathbf{Y}) = \frac{1}{M} \mathcal{L}_{\text{STFT}_m}({\hat{\mathbf{Y}}},\mathbf{Y})
$$

where the loss is the average across the error for the $M$ different STFT configurations. 
Further extensions of the approach involve using a linear combination of this error computed in the linear and $\log$ domains.

## Stereophonic

An important consideration for multitrack mixing systems is how our loss function considers stereophonic information. 
Unlike many other applications in audio signal processing, such as speech processing, proper stereo balance is a critical part of the mixing process. 
As a result, it is important that our loss function capture this behavior. 
As already discussed, existing loss functions that operate in the time or frequency domain can easily be extended to compare stereo information. 
However, reversing the left and right orientation often results in an mix that is perceived relatively the similarly by a human listener. 
Furthermore, we can see that reconstructing the exact panning from a mix is often an ill-posed problem as knowing a priori if a certain source will be panned left or right is often not possible. 

This motivates specialized stereophonic loss functions that are invariant to the absolute ordering of the channels. 
The sum and difference loss function, introduced in {cite}`steinmetz2021automatic, steinmetz2020auraloss` uses the sum and difference signals to enable computing an error on the mid and side part of the mix independently. 
First we compute the sum and difference signals in the time domain

$$
    \mathbf{y}_{\text{sum}}  = \mathbf{y}_{\text{left}} + \mathbf{y}_{\text{right}},  \quad
    \mathbf{y}_{\text{diff}} = \mathbf{y}_{\text{left}} - \mathbf{y}_{\text{right}}.  \label{eq:sd}
$$
We repeat this process for both the estimated mix and the reference mix. 
The final loss is computed by measuring the multi-resolution STFT of these sum and difference signals for both the estimated mix and the target mix. 

$$
    \mathcal{L}_{S/D}({\hat{\mathbf{Y}}},\mathbf{Y}) = \mathcal{L}_{\text{MR-STFT}}(\hat{\mathbf{Y}}_{\text{sum}}, \mathbf{Y}_{\text{sum}}) + 
    \mathcal{L}_{\text{MR-STFT}}(\hat{\mathbf{Y}}_{\text{diff}}, \mathbf{Y}_{\text{diff}}) \label{eq:sdmr}
$$

This loss function was shown to be important in training a model for automatic mixing that controlled the panning of elements within the mix when there was no consistent rule for panning within the dataset.
