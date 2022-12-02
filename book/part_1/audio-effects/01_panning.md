# Panning

Stereo panning is the positioning of sound sources typically done using gain amplitude techniques that create azimuthal cues from mono sources~\citep{pestana2014cross}. 
In a stereo pair of loudspeakers, applying panning consists of changing the amplitude of the left and right channels, which places the signal from left to right. 
This is usually implemented according to specific panning laws which operate within a $\pi$/2 range, where the left and right speakers are at 0 and $\pi$/2, respectively, i.e. the range of the panning value $\theta$ is defined as $\theta \in [0, \pi/2]$. The following are common used panning laws~\citep{panlaws}.

\linesubsec{Linear panning} The gains of the left and right channels, $L(\theta)$ and $R(\theta)$ respectively, should sum to 1 and are defined as

\begin{equation}
L(\theta) + R(\theta) = 1,
\label{eq:linear1}
\end{equation}
\begin{equation}
L(\theta)=\frac{2}{\pi}(\frac{\pi}{2}-\theta),
\label{eq:linear2}
\end{equation}
\begin{equation}
R(\theta)=\frac{2}{\pi}\theta.
\label{eq:linear3}
\end{equation}

However, when the signal is panned to the middle ($\theta=\pi$/4), the per-channel amplitude gain is -6 dB, and the total power, $P(\theta)=L(\theta)^2+R(\theta)^2$, is -3dB, thus creating a “hole-in-the-middle” effect~\citep{panlaws}.

\linesubsec{Constant power panning} The total power of the left and right channels remains constant across all panning positions and is defined as

\begin{equation}
L(\theta)=\cos(\theta),
\label{eq:constant1}
\end{equation}
\begin{equation}
R(\theta)=\sin(\theta). 
\label{eq:constant2}
\end{equation}

The total power at every panning position is 0 dB and the channel amplitude at the center is -3 dB (3 dB boost when compared to linear panning).

\linesubsec{-4.5 dB panning law} Motivated for equal loudness panning, the -4.5 dB panning law is defined as the square root of the product of the linear and constant power laws:

\begin{equation}
L(\theta)=\sqrt{\frac{2}{\pi}(\frac{\pi}{2}-\theta) \cdot \cos(\theta)}, \\
\label{eq:4.5db1}
\end{equation}
\begin{equation}
R(\theta)=\sqrt{\frac{2}{\pi}\theta \cdot \sin(\theta)}.
\label{eq:4.5db2}
\end{equation}

Where the channel attenuation at the center is -4.5 dB and the total power is -1.5 dB.

Both constant power panning and the -4.5 dB laws are widely used, and both are preferred over linear panning. Figure \ref{fig:pan_law} shows the amplitude and total power for the linear, constant and -4.5 dB panning laws.

\begin{figure}[H]
    \centering
    \includesvg[scale =0.6]{figures/audio effects/panning_laws.svg}
    \caption{Amplitude and total power for the linear, constant and -4.5 dB panning laws.
}
    \label{fig:pan_law}
\end{figure}
