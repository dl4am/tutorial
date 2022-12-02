# Panning

Stereo panning is the positioning of sound sources typically done using gain amplitude techniques that create azimuthal cues from mono sources {cite}`pestana2014cross`. 
In a stereo pair of loudspeakers, applying panning consists of changing the amplitude of the left and right channels, which places the signal from left to right. 
This is usually implemented according to specific panning laws which operate within a $\pi$/2 range, where the left and right speakers are at 0 and $\pi$/2, respectively, i.e. the range of the panning value $\theta$ is defined as $\theta \in [0, \pi/2]$. The following are common used panning laws {cite}`panlaws`.

## Linear panning 

The gains of the left and right channels, $L(\theta)$ and $R(\theta)$ respectively, should sum to 1 and are defined as

$$
L(\theta) + R(\theta) = 1,
\label{eq:linear1}
$$

$$
L(\theta)=\frac{2}{\pi}(\frac{\pi}{2}-\theta),
\label{eq:linear2}
$$

$$
R(\theta)=\frac{2}{\pi}\theta.
\label{eq:linear3}
$$

However, when the signal is panned to the middle ($\theta=\pi$/4), the per-channel amplitude gain is -6 dB, and the total power, $P(\theta)=L(\theta)^2+R(\theta)^2$, is -3dB, thus creating a “hole-in-the-middle” effect {cite}`panlaws`.

## Constant power panning 

The total power of the left and right channels remains constant across all panning positions and is defined as

$$
L(\theta)=\cos(\theta),
\label{eq:constant1}
$$

$$
R(\theta)=\sin(\theta). 
\label{eq:constant2}
$$

The total power at every panning position is 0 dB and the channel amplitude at the center is -3 dB (3 dB boost when compared to linear panning).

## -4.5 dB panning law 

Motivated for equal loudness panning, the -4.5 dB panning law is defined as the square root of the product of the linear and constant power laws:

$$
L(\theta)=\sqrt{\frac{2}{\pi}(\frac{\pi}{2}-\theta) \cdot \cos(\theta)},
$$

$$
R(\theta)=\sqrt{\frac{2}{\pi}\theta \cdot \sin(\theta)}.
$$


Where the channel attenuation at the center is -4.5 dB and the total power is -1.5 dB.

Both constant power panning and the -4.5 dB laws are widely used, and both are preferred over linear panning. 
Figure {numref}`pan_law` shows the amplitude and total power for the linear, constant and -4.5 dB panning laws.


```{figure} /assets/figures/audio-effects/panning_laws.svg
:name: pan_law
:alt: Pan law
:align: center

Amplitude and total power for the linear, constant and -4.5 dB panning laws.
```