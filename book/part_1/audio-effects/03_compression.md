# Compression

Dynamic Range Compression is a nonlinear audio effect that is generally used to control the dynamic range of a sound or combination of sounds. The history of the dynamic range compressor is inextricably linked to changes in trends and styles in popular music production~\citep{bromham2018impact}. In our videos compression is used to add bite to the kick drum and also control the level of bass in a subsequent video which also demonstrates how sidechaining works. Fig. \ref{kickbass} depicts the mixing session, and the following sections explain the technical concepts behind nonlinear audio effects and dynamic range compression.

\begin{figure}[h]
\centering
\includegraphics[width=\textwidth]{figures/Flare Kick:Bass Sidechaining.png}
\caption{Sidechain Compression for kick drum mixing. }
\label{kickbass}
\end{figure}


\linesubsec{Nonlinear effects} Nonlinear processors correspond to all the signal processing systems that do not satisfy the linearity condition, i.e. systems that do not have the homogeneous or additive property~\citep{chen1984}
 
These systems have a purposeful or unintentional insertion of harmonic or inharmonic frequency components that are not present in the input signal, which is known as a harmonic and intermodulation distortion~\citep{zolzer2011}.

When the system introduces energy at each harmonic or multiple of the input frequency, harmonic distortion occurs. When the system adds or subtracts frequencies between the frequency components of the input signal, intermodulation distortion results~\citep{reiss2014}.
 
In the case of musical signals, due to aesthetic reasons, harmonic distortion is a desirable property of nonlinear audio processors, while intermodulation distortion is generally avoided~\citep{reiss2014}.
 
Nonlinear audio effects are extensively used by musicians and sound engineers and, based on short-term and long-term memory capabilities, they can be classified into two main types of effects: dynamic range processors (DRC) such as compressors or limiters; and distortion effects such as tube amplifiers~\citep{martinez2020deeplearning, zolzer2011}.

\linesubsec{Dynamic range processors} DRC or compressors are traditionally used to reduce the dynamics of the input signal by applying a time-varying gain which alters the attack of the audio by effecting the transients of the input~\citep{zolzer2002dafx}.
 
The main purpose of dynamic range processors, which are nonlinear time-invariant audio effects with long temporal dependencies, is to change the variation in volume of the incoming audio. This is achieved with a varying amplification gain factor, which depends on an envelope follower along with a waveshaping nonlinearity, which distorts the shape of the incoming waveform. Long-term memory behavior describes these effects, since the output depends on the current and previous values of the input samples. These effects tend to introduce a low amount of harmonic distortion, while for distortion processors a high amount is desired~\citep{zolzer2011}.
 
Usually, the amount of gain depends on different parameters such as threshold, ratio, attack and release times and knee. For a compressor, threshold determines the level above which compression begins, and the ratio determines how much compression is used. Typically, ratio is set as the input/output rate for levels larger than the threshold. When the signal level crosses or drops below the threshold level, attack and release times determine how fast the compressor starts and stops applying compression, respectively. Knee controls the smoothness of the transition at the threshold point~\citep{martinez2020deeplearning}.
 
The various types of dynamic range processors can be classified into the following types of effects~\citep{martinez2020deeplearning, zolzer2011, reiss2014}.

\linesubsec{Compressor} Reduces the dynamics of the input signal by applying a variable gain. Based on the ratio, this decreased gain is applied to the input signals that are above the threshold. This can further increase the overall levels of the output signal thus boosting the loudness. 

\begin{figure}[H]
    \centering
    \includesvg[inkscapelatex=false,scale =0.225]{figures/audio effects/compression.svg}
    \caption{Compressor}
    \label{fig:compressor}
\end{figure}

\linesubsec{Expander} Does the opposite of the compressor by increasing the dynamics of the input signals. This is done by reducing amplitudes that are below the threshold.

\begin{figure}[H]
    \centering
    \includesvg[inkscapelatex=false,scale =0.225]{figures/audio effects/expander.svg}
    \caption{Expander}
    \label{fig:expander}
\end{figure}

\linesubsec{Multiband Compressor} Applies compression to selected frequency bands via a filter bank which splits the input signal, so each band is individually compressed.
 
\linesubsec{Sidechain Compression} Common practice within mixing tasks, where the compressor has an additional input ("side input"). When the level of the side input is above the threshold, the compressor is activated, and the dynamics of the input signal are reduced.

\linesubsec{Limiter} Eliminates any dynamics above the threshold by keeping the output level constant, i.e. ratio is $\infty$/1.

\begin{figure}[H]
    \centering
    \includesvg[inkscapelatex=false,scale =0.225]{figures/audio effects/limiter.svg}
    \caption{Limiter}
    \label{fig:limiter}
\end{figure}

\linesubsec{Noise gate} Eliminates any dynamics below the threshold by keeping the output level muted.

\begin{figure}[H]
    \centering
    \includesvg[inkscapelatex=false,scale =0.225]{figures/audio effects/noiseGate.svg}
    \caption{Noise gate}
    \label{fig:noiseGate}
\end{figure}

See~\citet{zolzer2011} for a further review of other types of nonlinear audio processors such as distortion effects, de-esser, tape saturation, exciters and enhancers.
