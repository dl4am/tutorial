# Reverberation

<iframe width="560" height="315" src="https://www.youtube.com/embed/tuIgIS2o-rU?start=218" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Reverberation is the process of reflecting sound off different surfaces. In music production this can be created by the use of real space or artificially using algorithmic or convolution techniques. Types of reverberation vary from Room, Hall, Cathedral, Plate or Spring. Digital iterations and incarnations can be found in most commercial music software. The video shows the addition of a large reverb adding a stadium-like spatial effect to the snare sound. {numref}`voxrev` depicts the reverberation processing for vocals mixing and below we introduce reverberation from a signal processing perspective. 


```{figure} /assets/figures/mixing/Flare-Vocal-Processing.png
:name: voxrev
:align: center
:width: 100%

Appliction of reverberation to the vocal in the context of a mix. 
```

Artificial reverberation is often used to emulate an indoor space or to complement the acoustics of a recording {cite}`pestana2017user`, it consists of frequency-dependent reflections of delayed and attenuated copies of the input {cite}`zolzer2002dafx`.
 
Reverberation occurs when delayed and attenuated copies of the direct sound appear as reflections. Each reflection is frequency dependent and defined by the sound source's directivity as well as the physical properties of the reflecting surfaces. {cite}`zolzer2011`. The reflections that occur immediately after the sound event are considered early reflections. These are not perceived individually, but as a combination of all the reflections {cite}`martinez2020deeplearning`.
 
Late reflections appear more randomly and are distinguished by an increase in echo density, or the quantity of echoes per unit of time, which produces a diffuse reverberation. These reflections are perceived as one continuous decaying sound. {cite}`reiss2014audio`. Therefore, the impulse response of an acoustic space is often divided into: direct sound, early reflections and late reflections. 

```{figure} /assets/figures/audio-effects/IR.svg
:name: ir
:align: center
:width: 40%

Impulse response of an acoustic space.
```

In the music and film industry, artificial reverberation was initially developed as a way of approximating the reflections occurring in room acoustics. This led to techniques that simulate reverberation, such as chamber, plate, spring and digital reverberators {cite}`valimaki2012`
 
Reverberation is approximately linear and time-invariant. As a result, the majority of digital techniques that simulate reverberation make an effort to mimic the perceptual traits of the respective impulse responses. There are various methods which rely on digital filters, delay networks and convolution-based algorithms {cite}`martinez2020deeplearning`. 

## Comb and Allpass filters
 
{cite}`schroeder1961` proposed a digital reverberator based on a parallel filter bank of feedback comb filters and a series of allpass filters. Allpass filters allow all frequencies, but modify the phase relationships of the frequencies of the input signal. In general, the cut-off frequency is where the phase response reaches $-90$. A comb filter consists of adding a delayed version of a signal to itself {cite}`martinez2020deeplearning`.
 
The difference equation of a feedback comb filter is

$$
y(n) = x(n-M)+gy(n-M),
\label{eq:differenceCombReverb}
$$

where $M$ and $N$ are the input and output delay times respectively, and $g$ is the feedback coefficient. When $M$ is large, the impulse response of the filter is heard as discrete echoes or reflections that decay exponentially and are equally spaced in time. {cite}`martinez2020deeplearning`.
Thus, by varying the delay time of each feedback comb filter, the parallel filter bank replicates the reverberant reflections of an acoustic environment.
The late reflections are modeled by the allpass filters, for which the difference equation is

$$
y(n) = x(n-M)-gx(n)+gy(n-M).
\label{eq:differenceAllpassReverb}
$$

Each allpass filter also generate a series of decaying echoes, which increases the overall echo density, by expanding the previous single reflections into many reflections. This simulates the diffuse characteristic of late reflections {cite}`martinez2020deeplearning`.

## Convolutional

consists in convolving the input signal with a recorded or estimated impulse response of an acoustic environment. The impulse response can be measured via sinusoidal sweeps, where a linear or logarithmic sweep of constant amplitude is recorded in the respective acoustic space {cite}`farina2000simultaneous`.
 
Convolutional reverb is implemented via FIR filtering, where each coefficient corresponds to each value of the impulse response and this often becomes computationally expensive for large impulse responses. Block-based convolutions, comb filters, and allpass filters are typical methods for reducing this computational load. {cite}`reiss2014audio`. Thus, block-based convolutions via FIR filtering produce the early impulse response reflections, and IIR filters used in feedback comb and allpass filters produce the diffuse reverberation.

Thus, convolution via FIR filtering generates the early reflections of the impulse response, and feedback comb and allpass IIR filters generate the diffuse reverberation.

## Electromechanical reverberators

such as plate and spring were first used and researched as means to substitute real room reverberation. They are now frequently used in music production for aesthetic reasons due to their unique sonic characteristics {cite}`martinez2020deeplearning`.
 
\textit{Plate reverb} is based on a large metal plate which vibrates due to a moving-coil transducer attached to its centre. This transducer receives an amplified dry input signal, and plate vibrations are detected by a pickup sensor and amplified further {cite}`kuhl1958`. The sound of plate reverb differs from that of room acoustic reverberation because sound travels faster in metal than in air, increasing the echo density. {cite}`bilbao2009`.
 
Thus, this particular sonic characteristics are due to the mechanical and physical characteristics of the plate.
 
## Spring reverb
 
 is based on one or various helical springs suspended under low tension, attached to a magnetic bead and driven via an electromagnetic coupling {cite}`parker2009`. The input audio source is transduced to spring vibrations which are detected by a pickup sensor at the other end of the spring.

The distinct sound of spring reverb is caused by the various types of vibrations that occur, both transverse and longitudinal, resulting in an unusual combination of wave and dispersive propagation. {cite}`zolzer2011`.
