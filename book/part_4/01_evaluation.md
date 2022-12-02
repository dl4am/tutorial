# Evaluation

One of the main challenges of automatic mixing systems is their evaluation. Music mixing is inherently a creative process and therefore a highly subjective task whose result cannot be objectively categorized as correct or incorrect. So, by modeling or automating this process, we often generate an ill-posed problem, where there is no unique correct solution, and which cannot be fully expressed through objective metrics either.
This directly affects the way we train and evaluate our models, as there is not a single feasible metric that will fully encompass the production quality of a generated mix. For a supervised learning task, the use of a professional human-made mix as the ground truth is often a good indicator of performance, however, we must acknowledge that a mix that deviates from the ground truth does not always corresponds to an aesthetically unpleasant or “bad” mix.
Thus, perceptual listening tests have become the conventional way to evaluate these systems, and while there is no standardized test type or platform, we can base the design of a perceptual test on a set of best practices that can be found within the literature and adjust them to the specific characteristics of the automatic mixing system to be tested.

## Objective Metrics


Objective evaluation of music production tasks is not a straightforward task and remains an open field of research. For instance, no audio feature, loss function or deep learning embedding have yet been found that fully represent solely the mixing, post-production, or audio effects processing of an input audio. The existence of such a metric has the potential to significantly reduce the research and development time of automatic mixing systems. This, since in comparison with perceptual tests, the evaluation through metrics requires less time and effort. 

With this in mind, we can approximate the objective evaluation of automatic mixing systems through audio features that relate to the most common audio effects used during mixing. Since audio effects generally manipulate audio characteristics such as frequency content, dynamics, spatialization, timbre, or pitch, we can use audio features that are associated with these audio characteristics as a way to numerically evaluate mixes.

Considering the shortcomings of an objective evaluation when comparing mixtures, these features should only be taken as an indicator of performance when testing our models. An example of such flaws is a lack of ability to capture production quality or aesthetic improvements, or a lack of evidence of artifacts within the mix {cite}`IMPbook19`.

 We can use the following audio features {cite}`colonel2021reverse`:
    
- **Spectral features** for EQ and reverberation: centroid, bandwidth, contrast, flatness, and roll-off {cite}`peeters2004large`
- **Spatialisation features** for panning: the Panning Root Mean Square (RMS) {cite}`tzanetakis2007stereo`
- **Dynamic features** for dynamic range processors: RMS level, dynamic spread and crest factor {cite}`ma2015intelligent`
- **Loudness features** the integrated loudness level (LUFS) and peak loudness {cite}`itu2011itu`


To capture the dynamics of audio effects information we can compute the running mean over a fixed number of past frames {cite}`tzanetakis2007stereo`. We can calculate the mean absolute percentage error between the target and output features to get a better understanding of the overall relative error.

Deep features such as the embedding output of the Fx encoder proposed in {cite}`koo2022music` could also be used as an indicator of similarity for audio effect information, although a further analysis of such embeddings is required. Likewise, this applies to general purpose deep features related to audio perception, such as the Fréchet Audio Distance {cite}`kilgour2019frechet`.