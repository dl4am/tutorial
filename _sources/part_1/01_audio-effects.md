# Audio Effects

Audio effects (Fx) are analog or digital signal processing systems that transform certain characteristics of the sound source and are widely used in various media, such as music, live performances, television, movies, or video games.

In the context of music production, audio effects are used primarily for aesthetic reasons. The most typical audio effect transformations are based on frequency, such as equalization, dynamics as compression, spatialisation as panning, tone as distortion, and time as artificial reverberation, delays or modulation-based audio effects. This manipulation is achieved through effects units, or audio processors, which can be linear or nonlinear, time-invariant or time-varying, and have short-term or long-term memory.

Most of these effect units can be implemented directly in the digital domain through the use of digital filters and delay lines. However, their analog counterparts are often preferred, as their analog circuitry, often in conjunction with mechanical elements, produces a nonlinear, time-varying system whose full salient perceptual qualities are difficult to fully emulate digitally {cite}`martinez2020deep`.

Effect units can be applied as send or insert effects. Send effects are used when a copy of the input is processed and then added to the original input. Insert effects are applied directly and in series to the input signal.

[https://lh3.googleusercontent.com/NZbP3T9wBRpKlzuqaOxv650V7s7E7iSCMAAR9EO4EltTdANtzLSSnj4dG9piU9zPtv-XNk2fjYVHaaQDgVar03m7QhTC8JXrC11SN4DIFX2icZGnYfzs37Xbn1vcAdO3mQEwvT3Y8ajTYgVHPZP0jRrlsvgJwMD3yFZ3Pqup10pRUp6JldGXAmIu-zXfsQ](https://lh3.googleusercontent.com/NZbP3T9wBRpKlzuqaOxv650V7s7E7iSCMAAR9EO4EltTdANtzLSSnj4dG9piU9zPtv-XNk2fjYVHaaQDgVar03m7QhTC8JXrC11SN4DIFX2icZGnYfzs37Xbn1vcAdO3mQEwvT3Y8ajTYgVHPZP0jRrlsvgJwMD3yFZ3Pqup10pRUp6JldGXAmIu-zXfsQ)

Audio effects as inserts

[https://lh3.googleusercontent.com/-ijp3OBoKP9SsjS8GBws0V7oSwPgRtMQUwZLNIjZQYZGVaJbox1zPg7PFOs2MSlqdPX-KZOixzcPpT_Fa32oEG8_QMmKThFaLAtd7DmtYQYM0gXnbRW13tvXNDnD5OgWLj2u-sW28J_PwLH-x9JZcUqxmqEqTu8Xi-XCwFSk0otaIGr6qf19LA-u7JqtlQ](https://lh3.googleusercontent.com/-ijp3OBoKP9SsjS8GBws0V7oSwPgRtMQUwZLNIjZQYZGVaJbox1zPg7PFOs2MSlqdPX-KZOixzcPpT_Fa32oEG8_QMmKThFaLAtd7DmtYQYM0gXnbRW13tvXNDnD5OgWLj2u-sW28J_PwLH-x9JZcUqxmqEqTu8Xi-XCwFSk0otaIGr6qf19LA-u7JqtlQ)

Audio effects as sends

## Equalization

EQ is an integral part of music production, where a filter bank is used as a corrective filter to reduce masking {cite}`valimaki2016all`, i.e. overlapping of sound sources, or as a creative tool to shape the harmonic and timbral characteristics {cite}`IMPbook19.

EQ is an audio effect widely used in the production and consumption of music {cite}`valimaki2016all`. It consists of the modification of frequency content through positive or negative gains which change the harmonic and timbral characteristics of the audio.

This is performed for different purposes, such as a corrective/technical filter to reduce masking or leakage within a mixing task, to modify the frequency response of a speaker system, or as an artistic or creative tool when recording a specific audio source.

An equalizer is normally implemented via a filter bank whose coefficients are obtained from the designed cut-off frequency $f_{c}$ and quality factor $Q$.

In general, EQ is performed through a gain $G$ at a given $f_{c}$ and $Q$, and it can be applied in the time-domain and frequency-domain~\cite{verfaille2016}.

The filter bank consists of Finite Impulse Response (FIR) or Infinite Impulse Response (IIR) filters, whose main difference corresponds to the absence or presence of feedback loops~\cite{gaydecki2014}. The non-recursive FIR discrete difference equation is

[https://lh6.googleusercontent.com/C1ns-40AN8olIBq2s0iJ4rGieIBXkxkmB5mCevgYVlJh3seyXrN8kFlmseDbZPq3sBc_TttjqCy2sjZrwlpYL15Ae7F02QVQZQtklnvx-6plqTBJdCS8zARO3F7llUdJXcrKVTTCGcndJEhoheVayyXHIhU9kI8ch4woZ1Ik0I3dqE1r7CsgSoOm9V4ksw](https://lh6.googleusercontent.com/C1ns-40AN8olIBq2s0iJ4rGieIBXkxkmB5mCevgYVlJh3seyXrN8kFlmseDbZPq3sBc_TttjqCy2sjZrwlpYL15Ae7F02QVQZQtklnvx-6plqTBJdCS8zARO3F7llUdJXcrKVTTCGcndJEhoheVayyXHIhU9kI8ch4woZ1Ik0I3dqE1r7CsgSoOm9V4ksw)

where $y(n)$ is the output signal, $x(n)$ is the input signal and $a_{k}$ corresponds to the $M$ filter coefficients. This non-recursive system is characterized by being a weighted sum of delayed inputs, thus a general FIR filter consists of a feed-forward system with $M−$1 delay lines. The recursive IIR discrete difference equation is

[https://lh3.googleusercontent.com/FimtUk_p74-GLsml5NKvEg_OZmWWC_rvt78crYfeSKqwWNxwENNOZSLLKGFORrfUfmIvkmXpbz-Oal-GJ2fHzNMfErq0gdbsSGBW82LSvxtdh9vnskm1QrC4qxZRWdVPMwHVz9Gq8ozFbO0c7_71ueXUz6uQDqwfdgU8Ldd3jpmo8sv1wW-P77WfN0Nh8A](https://lh3.googleusercontent.com/FimtUk_p74-GLsml5NKvEg_OZmWWC_rvt78crYfeSKqwWNxwENNOZSLLKGFORrfUfmIvkmXpbz-Oal-GJ2fHzNMfErq0gdbsSGBW82LSvxtdh9vnskm1QrC4qxZRWdVPMwHVz9Gq8ozFbO0c7_71ueXUz6uQDqwfdgU8Ldd3jpmo8sv1wW-P77WfN0Nh8A)

The IIR systems are characterized by a weighted sum of delayed inputs and outputs. This feedback system consists of an input delay line of $M−$1 elements and an output delay line of $N$ elements. The recursive coefficients are $b_{k}$.

The various types of filters can be classified into the following classes~\cite{zolzer2014}. These types of filters can be implemented via FIR or IIR filters whose coefficients determine $G$, $f_{c}$ and $Q$. Most of the widely used EQs are based on the following filter types

- **Lowpass**: attenuates frequencies above $f_{c}$ and $Q$ determines a boost or resonance of frequencies around $f_{c}$.

[https://lh5.googleusercontent.com/POduTQljPXhEOS73XJ_EjTERngE15nK1aV5BP7_qlK9tB6t_USgO5WGcz8ye_wVLYJep9I4w3XFj8OtvbxvOEa-XbtOECENmacwkAocwT-H0keZXxmuR2WsIxq16ETYOmniOGJfOuaPWSNgEgKYTkpsVROLDN5HzaffTg25er5CF0XnbclijB0zxx69S_Q](https://lh5.googleusercontent.com/POduTQljPXhEOS73XJ_EjTERngE15nK1aV5BP7_qlK9tB6t_USgO5WGcz8ye_wVLYJep9I4w3XFj8OtvbxvOEa-XbtOECENmacwkAocwT-H0keZXxmuR2WsIxq16ETYOmniOGJfOuaPWSNgEgKYTkpsVROLDN5HzaffTg25er5CF0XnbclijB0zxx69S_Q)

- **Highpass:** attenuates frequencies below $f_{c}$ and $Q$ determines a boost or resonance of frequencies around $f_{c}$.

[https://lh6.googleusercontent.com/ifkjBF_d7kMqNrP6nMj1Sd3qJNwgQLP-u2FzMDGrbbPi3SiKj9OW2XVtC0Ar_zxs9NAUgIans8Y36G27Sn55L5DCkCq2RqGXzHQOUWlNAL-O9wulKYg63DXoWwkBxzIfMuEHVVR-NLEqFHk4DjRIQP96ia8YiCWn8GPGoCSqofOtQFT3lUCylUYWr1YaRw](https://lh6.googleusercontent.com/ifkjBF_d7kMqNrP6nMj1Sd3qJNwgQLP-u2FzMDGrbbPi3SiKj9OW2XVtC0Ar_zxs9NAUgIans8Y36G27Sn55L5DCkCq2RqGXzHQOUWlNAL-O9wulKYg63DXoWwkBxzIfMuEHVVR-NLEqFHk4DjRIQP96ia8YiCWn8GPGoCSqofOtQFT3lUCylUYWr1YaRw)

- **Bandpass:** attenuates frequencies above and below a frequency band with bandwidth $f_{b}$ and center frequency $f_{c}$. $Q$ is the relative bandwidth $f_{c}$/ $f_{b}$. A bandreject filter attenuates frequencies within the frequency band.

[https://lh5.googleusercontent.com/IGst4ad_ig9Hw0Ox-np1E94PuGDTYchx85B6scO4YrflLkBhhdELaVG3PLtJ2aLOa_PezVecYSxy4bxRbV_RkfefS1SKuzoFB3WBvVXx-wLOEQ4CfjvVxXbcSEoX_BAHIonDvSdu1In6rWhSJbbEcmxcQHFpK-3xmB2v7mP1w0PnEAuj-H8c86PTc00-PQ](https://lh5.googleusercontent.com/IGst4ad_ig9Hw0Ox-np1E94PuGDTYchx85B6scO4YrflLkBhhdELaVG3PLtJ2aLOa_PezVecYSxy4bxRbV_RkfefS1SKuzoFB3WBvVXx-wLOEQ4CfjvVxXbcSEoX_BAHIonDvSdu1In6rWhSJbbEcmxcQHFpK-3xmB2v7mP1w0PnEAuj-H8c86PTc00-PQ)

- **Shelving**: a low-frequency shelving filter (lowshelf) boosts or cuts frequencies below $f_{c}$ while preserving frequencies above $f_{c}$. A high-frequency shelving filter (highshelf) boosts or cuts frequencies above $f_{c}$ while preserving frequencies below $f_{c}$. $Q$ determines the resonance of frequencies around $f_{c}$.

[https://lh6.googleusercontent.com/FGcG4Ny1HLV7C6HbWmXSUiVHpLk-_AOsbnmGbLaWmSytCYHuy6GUDqzfWHO_ryDySQSw9jysbEaas0O8PW1iPs-iJJt3YMzNGBzLrIBePicJ-VWsL9KIVgziRd6O9DI8WoscwlJKHt5oDT54k1HnK1dSjZ1jwM4sW59OMdiWQ9jRB1UJuF9_XXtV9yDivQ](https://lh6.googleusercontent.com/FGcG4Ny1HLV7C6HbWmXSUiVHpLk-_AOsbnmGbLaWmSytCYHuy6GUDqzfWHO_ryDySQSw9jysbEaas0O8PW1iPs-iJJt3YMzNGBzLrIBePicJ-VWsL9KIVgziRd6O9DI8WoscwlJKHt5oDT54k1HnK1dSjZ1jwM4sW59OMdiWQ9jRB1UJuF9_XXtV9yDivQ)

- **Peaking**: boosts frequencies between a bandwidth $f_{b}$ with center frequency $f_{c}$ while preserving frequencies outside this frequency band. A notch filter cuts frequencies within the frequency band.

[https://lh3.googleusercontent.com/nYrgRPIr0dCYzrTIk5Op7JCSmoIt1io4Cb6FrL8pIsmHUCU4YI2P3FjT8v1xhtQQjtx3seTNV2bP0PuUFhyXZg2coZtWIDUTzsxDw7VGDyxIL9spCg0K5y0braMsIpbpX0MWnzriy93bUrkiVRScWMIqlhN9I1fK5TDOnb04rCLz1Fn50-hPBk-odqG6Ow](https://lh3.googleusercontent.com/nYrgRPIr0dCYzrTIk5Op7JCSmoIt1io4Cb6FrL8pIsmHUCU4YI2P3FjT8v1xhtQQjtx3seTNV2bP0PuUFhyXZg2coZtWIDUTzsxDw7VGDyxIL9spCg0K5y0braMsIpbpX0MWnzriy93bUrkiVRScWMIqlhN9I1fK5TDOnb04rCLz1Fn50-hPBk-odqG6Ow)

## Panning

Stereo panning is the positioning of sound sources typically done using gain amplitude techniques that create azimuthal cues from mono sources~\cite{pestana2014cross}.

In a stereo pair of loudspeakers, applying panning consists of changing the amplitude of the left and right channels, which places the signal from left to right.

This is usually implemented according to specific panning laws which operate within a $\pi$/2 range, where the left and right speakers are at 0 and $\pi$/2, respectively, i.e. the range of the panning value $\theta$ is defined as

[https://lh5.googleusercontent.com/8zPnB3DDrHwBc1FPT5Pn0nW9A-HXspeR-9a9XFdoK1NfIyvuoLVl-bU331WYB12hbWLAesBLMypx1NKVPfmcvDWJg7qpzdvyo6wIx0BS6O1Ldm190qY0SmITTCR0D-SdkxH92qo1AbU_4kcUAtD0234Icx9yB9z0fyx4k-5SPTfn7zJM00SBAmhxJ4qMZg](https://lh5.googleusercontent.com/8zPnB3DDrHwBc1FPT5Pn0nW9A-HXspeR-9a9XFdoK1NfIyvuoLVl-bU331WYB12hbWLAesBLMypx1NKVPfmcvDWJg7qpzdvyo6wIx0BS6O1Ldm190qY0SmITTCR0D-SdkxH92qo1AbU_4kcUAtD0234Icx9yB9z0fyx4k-5SPTfn7zJM00SBAmhxJ4qMZg)

- **Linear panning**: The gains of the left and right channels should sum to 1 and is defined as

[https://lh6.googleusercontent.com/nGszxB7bGRmNhI3ZSVVZZapwAbAx0kjrC9LzoffwTD3fDd0CFFWPAZe_c5UK_xdNrdyBV0yJPcx6gzYkjKeeDiLJ89qjH4yjUBhZ7leGYRz_LaZmvNT-HX0wgCgbqzlg0xrY8UTVklFopC90iTvcSWzfyREx6rN-p7K9G3yMqdwkPSCVEZwLJfY3ups_tQ](https://lh6.googleusercontent.com/nGszxB7bGRmNhI3ZSVVZZapwAbAx0kjrC9LzoffwTD3fDd0CFFWPAZe_c5UK_xdNrdyBV0yJPcx6gzYkjKeeDiLJ89qjH4yjUBhZ7leGYRz_LaZmvNT-HX0wgCgbqzlg0xrY8UTVklFopC90iTvcSWzfyREx6rN-p7K9G3yMqdwkPSCVEZwLJfY3ups_tQ)

However, when the signal is panned to the middle ($\theta=\pi$/4), the per-channel amplitude gain is -6 dB, and the total power, $P(\theta)=L($\theta$)^2+R($\theta$)^2$, is -3dB, thus creating a “hole-in-the-middle” effect.

- **Constant power panning**: The total power of the left and right channels remains constant across all panning positions and is defined as

[https://lh3.googleusercontent.com/OTSJxZh4YEX-ZRsan83LdIyzp5y3XnFrCsCJnj15SSlVzwgsqkqc7QZJOXfRxMtiwWCVv1yxRbnV7mUfa-qMslX_GFB4Q9mtmZswwsgcVPwjBZUqvqgbOD7v7juuf8G4dJwCs6D9L7gsBUjvHngKMZ2fMlMX0uxSUdTIeV_TyQQbNZyZVuSUWZWsHkM3ig](https://lh3.googleusercontent.com/OTSJxZh4YEX-ZRsan83LdIyzp5y3XnFrCsCJnj15SSlVzwgsqkqc7QZJOXfRxMtiwWCVv1yxRbnV7mUfa-qMslX_GFB4Q9mtmZswwsgcVPwjBZUqvqgbOD7v7juuf8G4dJwCs6D9L7gsBUjvHngKMZ2fMlMX0uxSUdTIeV_TyQQbNZyZVuSUWZWsHkM3ig)

The total power at every panning position is 0 dB and the channel amplitude at the center is -3 dB (3 dB boost when compared to linear panning).

- **4.5 dB panning law**: Motivated for equal loudness panning, the -4.5 dB panning law is defined as the square root of the product of the linear and constant power laws:

[https://lh6.googleusercontent.com/Rmuu8uXVqwCtSZqDLcyfzHgPyThTBiEV5WHvUi9Coymk7ViaqrAwVGNNqKHxsWClvZoB-ytZg4bVcXnU6NLp7xv8iZl9VCTnqoL9kQ8SjbZNvcIYqpyMr5J6vt87XMeGvkclcqW9UrGPFwx4RDAbEJtyZjOx7LCBjASvqxvLNAy701tJmdq1-OxjhElhHg](https://lh6.googleusercontent.com/Rmuu8uXVqwCtSZqDLcyfzHgPyThTBiEV5WHvUi9Coymk7ViaqrAwVGNNqKHxsWClvZoB-ytZg4bVcXnU6NLp7xv8iZl9VCTnqoL9kQ8SjbZNvcIYqpyMr5J6vt87XMeGvkclcqW9UrGPFwx4RDAbEJtyZjOx7LCBjASvqxvLNAy701tJmdq1-OxjhElhHg)

Where the channel attenuation at the center is -4.5 dB and the total power is -1.5 dB.

Both constant power panning and the -4.5 dB laws are widely used, and both are preferred over linear panning.

[https://lh3.googleusercontent.com/mPSMzKpdGOUwqz5Elec6AZIka0D1XC12noHxvc0lTlXyKN1U_WABYvaS1suGg_fkz1XJtTtZaXgo0YJz6j7naznJwJbPKKavMPwYMUV27Rp4dSml_ActVOTsx4MOVB_fOEpSSsH5BLOe8Rv_vS_KMMbYc6_VOAFBqbdqUOWBEDj8hZ23JHRJuKPdsKGOlw](https://lh3.googleusercontent.com/mPSMzKpdGOUwqz5Elec6AZIka0D1XC12noHxvc0lTlXyKN1U_WABYvaS1suGg_fkz1XJtTtZaXgo0YJz6j7naznJwJbPKKavMPwYMUV27Rp4dSml_ActVOTsx4MOVB_fOEpSSsH5BLOe8Rv_vS_KMMbYc6_VOAFBqbdqUOWBEDj8hZ23JHRJuKPdsKGOlw)

Panning laws, amplitude and total power.

## Nonlinear audio effects

Nonlinear processors correspond to all the signal processing systems that do not satisfy the linearity condition, i.e. systems that do not have the homogeneous or additive property~\cite{chen1998}

These systems are characterized by a harmonic and intermodulation distortion consisting of the introduction of intentional or unintentional harmonic or inharmonic frequency components that are not present in the input signal~\cite{zolzer2011}

Harmonic distortion is when the system introduces energy at every multiple, or harmonic, of each input frequency. Intermodulation distortion occurs when the system inserts frequency addition or subtraction between the frequency components of the input signal~\cite{reiss2014}.

In the case of musical signals, due to aesthetic reasons, harmonic distortion is a desirable property of nonlinear audio processors, while intermodulation distortion is generally avoided~\cite{reiss2014}.

Nonlinear audio effects are extensively used by musicians and sound engineers and, based on short-term and long-term memory capabilities, they can be classified into two main types of effects: dynamic processors such as compressors or limiters; and distortion effects such as tube amplifiers~\cite{zolzer2011}.

### Distortion

Distortion effects are mainly used for aesthetic reasons and are usually applied to electric musical instruments such as electric guitar, bass guitar, electric piano or synthesizers. The main sonic characteristic of these effects is due to their nonlinearities and the most common processors are overdrive, distortion pedals, and tube amplifiers.

These effects can be described by their characteristic curve or waveshaping nonlinearity, which distorts the shape of the incoming waveform. An instance of a distortion waveshaping curve is

[https://lh5.googleusercontent.com/SIQaPE0vv12UCHoA_owy6KETZoMfICMEYOU7QvxzyGMyQig-WhrpAe0sQj_Mm76T2Y-5rET-GXY4f7t6zzt7FDiMyPyc7Xor7-sPv8e49kIfwDH9erZ2wle1lI-v4M1EYwa8OGVZc2OJBOcerbuGkq-GPP2rFUZhWU9_29zWD0toZ93xrQIgIltKsQzBNQ](https://lh5.googleusercontent.com/SIQaPE0vv12UCHoA_owy6KETZoMfICMEYOU7QvxzyGMyQig-WhrpAe0sQj_Mm76T2Y-5rET-GXY4f7t6zzt7FDiMyPyc7Xor7-sPv8e49kIfwDH9erZ2wle1lI-v4M1EYwa8OGVZc2OJBOcerbuGkq-GPP2rFUZhWU9_29zWD0toZ93xrQIgIltKsQzBNQ)

Distortion effects can be classified into the following types~\cite{zolzer2011}.

- **Overdrive**: linear audio effect at low input levels which becomes nonlinear when driven by higher input levels. It has a warm and smooth sound e.g. tube amplifiers.
- **Distortion**: mainly operates in the nonlinear region of the waveshaping curve and saturates or clips when reaching the upper or lower input levels. It covers a tonal area from warmth to crunch.
- **Fuzz**: operates completely in the nonlinear region. It is characterized by being a more aggressive style distortion.
- **Dynamic range processors~\cite{martinez2020deep}**

DRC or compressors are traditionally used to reduce the dynamics of the input signal by applying a time-varying gain which alters the attack of the audio by effecting the transients of the input~\cite{zolzer2002dafx}.

Dynamic range processors are nonlinear time-invariant audio effects with long temporal dependencies, and their main purpose is to alter the variation in volume of the incoming audio. This is achieved with a varying amplification gain factor, which depends on an envelope follower along with a waveshaping nonlinearity. Long-term memory behavior describes these effects, since the output depends on the current and previous values of the input samples. These effects tend to introduce a low amount of harmonic distortion, while for distortion processors a high amount is desired~\cite{zolzer2011}.

Usually, the amount of gain depends on different parameters such as **threshold**, **ratio**, **attack** and **release** times and **knee**. For a compressor: threshold is the level above which compression starts, ratio determines the amount of compression applied, normally is set as the input/output rate for levels larger than the threshold. Once the signal level rises above or falls below the threshold level, attack and release times establish how fast the compressor starts and stops applying compression, respectively. Knee controls the smoothness of the transition at the threshold point.

The various types of dynamic range processors can be classified into the following types of effects~\cite{zolzer2011, reiss2014}.

### Dynamics processing

- **Compressor**: reduces the dynamics of the input signal by applying a variable gain. Based on the ratio, this decreased gain is applied to the input signals that are above the threshold. This can further increase the overall levels of the output signal thus boosting the loudness.

[https://lh3.googleusercontent.com/_nu8ma-0IR0xGbkEcOXyQl_7Bcbkf4Zq9RKh3sDknnd-_z_7YRchdsER_McXtE8Yf62g6ITFlDZtMdEzNGG3eFNeduIApOFM-SK1YL5IR7ORrObDvk--hYIvjSw0AFXlLYQHhSpTNiC-BTxbY5yn7W-9I8ll-QC3X1KF0vmwWgSdVszfktrc0jVtTJjkdA](https://lh3.googleusercontent.com/_nu8ma-0IR0xGbkEcOXyQl_7Bcbkf4Zq9RKh3sDknnd-_z_7YRchdsER_McXtE8Yf62g6ITFlDZtMdEzNGG3eFNeduIApOFM-SK1YL5IR7ORrObDvk--hYIvjSw0AFXlLYQHhSpTNiC-BTxbY5yn7W-9I8ll-QC3X1KF0vmwWgSdVszfktrc0jVtTJjkdA)

- **Expander**: does the opposite of the compressor by increasing the dynamics of the input signals. This is done by reducing amplitudes that are below the threshold.

[https://lh6.googleusercontent.com/G2q2UJaP7_GQF6lKKWpxjWidcizP9J97z8S8oK5H2uJyLv-UEDISHWVnvJlTdPSgpklZ9Qu6o99KRp81Q53KkD0TjtZrqigzdN5c6gog8Hj3bp8stkiWu7qQDq3M_lPuQtoU0q6g1ACSD4BJPi-RjW1dAgdAf0B7tFGbGEPvFucocjvlCDfpYNkxsueeTQ](https://lh6.googleusercontent.com/G2q2UJaP7_GQF6lKKWpxjWidcizP9J97z8S8oK5H2uJyLv-UEDISHWVnvJlTdPSgpklZ9Qu6o99KRp81Q53KkD0TjtZrqigzdN5c6gog8Hj3bp8stkiWu7qQDq3M_lPuQtoU0q6g1ACSD4BJPi-RjW1dAgdAf0B7tFGbGEPvFucocjvlCDfpYNkxsueeTQ)

- **Multiband Compressor**: applies compression to selected frequency bands via a filter bank which splits the input signal, so each band is individually compressed.
- **Sidechain Compression**: Common practice within mixing tasks, where the compressor has an additional input ("side input"). When the level of the side input is above the threshold, the compressor is activated, and the dynamics of the input signal are reduced.
- **Limiter**: eliminates any dynamics above the threshold by keeping the output level constant, i.e. ratio is $\infty$/1.

[https://lh6.googleusercontent.com/SQlLrRXpPkBEYaKhUe0y98ED50wfM9bdR17ZQZSCQxZrmZ81OM_zo_cm9m13tane4ckTEBwOXILDP5sbi-cBkyuMT2CJWsbE8CgZo4m83upw2C9MnQILxrLgSq-P7442Jr-Vtv9J-T1FkKcjKzPmzg2Amw1NnJzxqtW3njQgrZgAcjussOWfv0qZwILqxQ](https://lh6.googleusercontent.com/SQlLrRXpPkBEYaKhUe0y98ED50wfM9bdR17ZQZSCQxZrmZ81OM_zo_cm9m13tane4ckTEBwOXILDP5sbi-cBkyuMT2CJWsbE8CgZo4m83upw2C9MnQILxrLgSq-P7442Jr-Vtv9J-T1FkKcjKzPmzg2Amw1NnJzxqtW3njQgrZgAcjussOWfv0qZwILqxQ)

- **Noise gate**: eliminates any dynamics below the threshold by keeping the output level muted.

[https://lh6.googleusercontent.com/qztnlcBtX-m7oIg4m3eTQgX7_uW9O_eabvl3CzD_KQ3FRESn4UYptdgyaRLXbX71Bs8FFBhJzIRgCQmkvuxdj-ukwt-W6GM6xChkq45LpyNIBnjepBBaeciBLLbE7FOPvgQFuhXSBPGT190IzD4CxqB3quCBiNK4SY_MvWqbhQ2S_B1oU1IOhn21uxtegA](https://lh6.googleusercontent.com/qztnlcBtX-m7oIg4m3eTQgX7_uW9O_eabvl3CzD_KQ3FRESn4UYptdgyaRLXbX71Bs8FFBhJzIRgCQmkvuxdj-ukwt-W6GM6xChkq45LpyNIBnjepBBaeciBLLbE7FOPvgQFuhXSBPGT190IzD4CxqB3quCBiNK4SY_MvWqbhQ2S_B1oU1IOhn21uxtegA)

## Artificial Reverberation

Often used to emulate an indoor space or to complement the acoustics of a recording~\cite{pestana2017user}, it consists of frequency-dependent reflections of delayed and attenuated copies of the input~\cite{zolzer2002dafx}.

Reverberation occurs when delayed and attenuated copies of the direct sound appear as reflections. Each reflection is frequency dependent and defined by the directivity of the sound source and the physical attributes of the reflecting surfaces~\cite{zolzer2011}. The reflections that occur immediately after the sound event are considered early reflections. These are not perceived individually, but as a combination of all the reflections.

Late reflections appear more randomly and are characterized by increasing the echo density, that is, the number of echoes per time unit, which generates a diffuse reverberation. Perceptually, the reflections merge into a sound of continuous decay~\cite{reiss2014}. Therefore, the impulse response of an acoustic space is often divided into: direct sound, early reflections and late reflections.

[https://lh6.googleusercontent.com/Ncyz48vw8H4j0eC_lLr7S-5IKQ2z6aVA-XptcatULfZLwL5u3Z1VUdolwYG2ZQwmTIkHc0uLKksKh6Gw6GrOv_PX3bzkcJHMpLhX8qBCCpOmLuiFRgebQBYoeRN1hhabPihro97L5ocJBDWznbxWmhCG31fW4GazbSB4H3eB-1E_2UkovHi_Uv0TgD0aJQ](https://lh6.googleusercontent.com/Ncyz48vw8H4j0eC_lLr7S-5IKQ2z6aVA-XptcatULfZLwL5u3Z1VUdolwYG2ZQwmTIkHc0uLKksKh6Gw6GrOv_PX3bzkcJHMpLhX8qBCCpOmLuiFRgebQBYoeRN1hhabPihro97L5ocJBDWznbxWmhCG31fW4GazbSB4H3eB-1E_2UkovHi_Uv0TgD0aJQ)

Impulse response of an acoustic space

In the music and film industry, artificial reverberation was initially researched as a way of approximating the reflections occurring in room acoustics. This led to techniques that simulate reverberation, such as chamber, plate, spring and digital reverberators~\cite{valimaki2012}

Reverberation is approximately linear and time-invariant. Thus, most of the digital methods that emulate reverberation attempt to match the perceptual characteristics of the respective impulse responses. There are various methods which rely on digital filters, delay networks and convolution-based algorithms.

- **Comb and Allpass filters**: Schroeder and Logan (1961)~\cite{schroeder1961} proposed a digital reverberator based on a parallel filter bank of feedback comb filters and a series of allpass filters. Allpass filters allow all frequencies, but modify the phase relationships of the frequencies of the input signal. In general, the cut-off frequency is where the phase response reaches −90. A comb filter consists of adding a delayed version of a signal to itself.

The difference equation of a feedback comb filter is

[https://lh4.googleusercontent.com/OMABY-OjB8L9Z_ltboCWpQ1Gp1HaNoFvHJXH9kf7OjXcQcFlrn7Ax-iCMM7ZMv1ErTbxHzfz8pxnew1a0_OVYqeAIHxu23y017Y-S6QLTF8h9StNi2zu1Oq7qpa5du6AMPmO15FpPy0hnUu7WvZlHasPzu7rSDs7cjuzGOQ6r4_aaD0STeyn3Jmec1WRMg](https://lh4.googleusercontent.com/OMABY-OjB8L9Z_ltboCWpQ1Gp1HaNoFvHJXH9kf7OjXcQcFlrn7Ax-iCMM7ZMv1ErTbxHzfz8pxnew1a0_OVYqeAIHxu23y017Y-S6QLTF8h9StNi2zu1Oq7qpa5du6AMPmO15FpPy0hnUu7WvZlHasPzu7rSDs7cjuzGOQ6r4_aaD0STeyn3Jmec1WRMg)

where $M$ and $N$ are the input and output delay times respectively, and $g$ is

the feedback coefficient. When $M$ is large, the impulse response of the filter is heard as discrete echoes or reflections which are exponentially decaying and uniformly spaced in time.

Thus, by adjusting the delay time of each feedback comb filter, the parallel filter bank simulates the reverberant reflections of an acoustic environment.

The allpass filters emulate the late reflections of the reverberator, for which the difference equation is

[https://lh6.googleusercontent.com/kSHNQ0cLhboU5G8rK9RaE0pwwj6wELmM0JmKOksDlcWJMQ3VFusCOToqqhtp8k3qbYuyN1OFvgdU7Qialevf__bMPDBZG80qXsmXrzAXUdMH44VDxF56RHkF4oarKZvksAw1Dn8-phkh4Ea11KKqugmzqnhHsZs0Ti5w7LTixCJl4CUOT7Exl7ezp6TOAw](https://lh6.googleusercontent.com/kSHNQ0cLhboU5G8rK9RaE0pwwj6wELmM0JmKOksDlcWJMQ3VFusCOToqqhtp8k3qbYuyN1OFvgdU7Qialevf__bMPDBZG80qXsmXrzAXUdMH44VDxF56RHkF4oarKZvksAw1Dn8-phkh4Ea11KKqugmzqnhHsZs0Ti5w7LTixCJl4CUOT7Exl7ezp6TOAw)

Each allpass filter also produces a series of decaying echoes, thus increasing overall echo density, and expanding the previous single reflections into many reflections. This simulates the diffuse reverberation

- **Convolutional**: consists in convolving the input signal with a recorded or estimated impulse response of an acoustic environment. The impulse response can be measured via sinusoidal sweeps, where a linear or logarithmic sweep of constant amplitude is recorded in the respective acoustic space~cite{farina2000}.

Convolutional reverb is implemented via FIR filtering, where each coefficient corresponds to each value of the impulse response, resulting in a very high order filter~cite{valimaki2014}. A common approach to overcome this computational load is to use block-based convolutions and comb and allpass filters~cite{reiss2014}. Thus, convolution via FIR filtering generates the early reflections of the impulse response, and IIR filters, such as feedback comb and allpass filters, generate the diffuse reverberation.

- **Electromechanical reverberators:** such as plate and spring were first used and researched as means to substitute real room reverberation. Currently, they are often used in music production for aesthetic reasons due to their particular sonic characteristics.
- **Plate reverb**: is based on a large metal plate which vibrates due to a moving-coil transducer attached to its centre. This transducer is fed with an amplified dry input signal and the plate vibrations are read by a pickup sensor and further amplified~\cite{kuhl1958}. The plate reverb sound is different from room acoustic reverberation as the speed of sound is faster in metal than in air, increasing the echo density~\cite{bilbao2009}.

This particular response is due to the mechanical and physical characteristics of the plate.

- **Spring reverb**: is based on one or various helical springs suspended under low tension, attached to a magnetic bead and driven via an electromagnetic coupling~\cite{parker2009}. The input audio source is transduced to spring vibrations which are read through a pickup sensor at the opposite end.

The distinct sound of spring reverb is due to the various types of vibrations that occur, transverse and longitudinal, which cause a peculiar combination of wave and dispersive propagation~\cite{zolzer2011}.

See Zölzer (2011)~\cite{zolzer2011} for a further review of other types of nonlinear audio processors such as de-esser, tape saturation, exciters and enhancers, as well as modulation-based audio effects such as chorus, flanger and phaser.