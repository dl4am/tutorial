# Listening Tests

When designing listening tests for automatic music mixing systems, several criteria must be taken into account, such as the type of test, the number of stimuli, the duration of the stimuli, the criteria to be rated, the requirements for the participants, the listening environment, etc. While there is no standard, pre-defined testing method, we provide a set of best practices that can be tailored based on the requirements of the mixing system being tested.

## Participants

Due to the high level of detail inherent within the perceived difference between mixes, it is preferable that participants have experience in music mixing, or at least music making or critical listening activities. Participants without such experience are likely to be unable to perceive production differences between mixes, making their ratings unreliable.

The preferable listening setup for this type of test is in a listening room with high-quality professional monitors. This is because this is the most common setting used by mixing engineers when creating or analyzing mixes. When a room with professional sound installation is not available, the use of high-quality headphones is often preferred.

However, it is worth noting that when listening to speakers compared to headphones, the stereo image changes, that is, when using headphones, the sound sources are placed "inside the head" {cite}`IMPbook19`. Moreover, most of the professional mixing engineers will mix using speakers. Therefore, it is important to consider this when one of the aspects to be rated is the stereo image. A good practice is to test exclusively with speakers or headphones, but not allow both listening configurations within the same test.

## Types of Tests

Multi-stimulus tests are often preferred over pairwise or single stimulus tests. Single stimulus tests, such as the Mean Opinion Score (MOS) test, are generally used to rate the overall quality of a stimulus, thus focusing on the content properties of the source material. Conversely, when evaluating the production quality of various mixes, it is preferable for participants to focus on the contrasting mix properties between mixes rather than on the content material of the mixes {cite}`skovenborg2016development`. Also, as the number of mixtures to be compared increases, it has been found that pairwise tests tend to be less reliable and discriminatory {cite}`IMPbook19`.   

The most common types of multi-stimulus tests are the following:

### MUSHRA 
Multiple Stimuli with Hidden Reference and Anchor (MUSHRA) is a well-known testing method initially designed for measuring the perceptual quality of audio codecs. Although this method is widely used in various audio and music perception tasks, the inherent design constraints of the method represent several limitations when evaluating music mixes.

For instance, given the subjective task at hand, having a professional human-made mix as reference can be problematic, as even commercial mixes made by renown engineers are not always rated highly {cite}`de2017towards, IMPbook19, martinez2022automatic`. Thus, when the stimulus has the potential to outperform the reference or hidden anchor, the MUSHRA methodology is not recommended {cite}`ITU1534`.
Furthermore, we often test mixes for overall production quality or technical preference and not for their similarity to a reference mix, hence rendering the use of a hidden anchor reference as unnecessary.

Regarding the use of low and mid anchors, when the participants are experts, the use of such anchors might have a negative impact on the test results. This is due to the critical listening skills of experts, whose discrimination of a low anchor, such as a monaural or random processed mix, is trivial. Thus, the presence of a low anchor will tend to compress the ratings of the other stimuli and could distract participants from focusing on the significant contrastive differences within the mixtures {cite}`IMPbook19`. Another argument for not including the anchor is to reduce the number of stimuli and thus allowing tests with a larger number of mixtures to be tested. It should be noted that when the participants are not exclusively experts, the use of low and mid anchors can serve its beneficial original purpose within the test.

Finally, the MUSHRA method recommends using stimuli of no more than 12 seconds, which, based on empirical data, we have found that experts consider this duration to be too short to adequately assess quality within a set of mixtures.

In general, it is not recommended to fully follow the MUSHRA methodology for the evaluation of this task, however, this multi-stimulus methodology could be further modified to fit the specific needs for the evaluation of automatic mixing systems.


```{figure} /assets/figures/evaluation/webmushra.svg
:name: webmushra
:width: 70%
:align: center

MUSHRA test implemented with webMUSHRA {cite}`schoeffler2018webmushra`.
```


```{figure} /assets/figures/evaluation/go-listen.svg
:name: go-listen
:width: 70%
:align: center

MUSHRA test implemented with goListen {cite}`barry2021golisten`.
```

### APE 

As an alternative for multi-stimulus testing the Audio Perceptual Evaluation (APE) was proposed by {cite}`de2014ape`.
The main difference with the MUSHRA method is that all the stimuli are placed under the same continuous horizontal line, thus allowing instant visualization of the ratings. Also, the use of reference and anchor is optional as well as the maximum length of the stimuli.
Examples of APE testing interface used in recent automatic music mixing systems:


```{figure} /assets/figures/evaluation/APE_DMC.svg
:name: ape-dmc
:width: 70%
:align: center

APE test from {cite}`steinmetz2020mixing`.
```


```{figure} /assets/figures/evaluation/APE_WaveUNet_Drums.svg
:name: ape-wun-drums
:width: 70%
:align: center

APE test from {cite}`martinez2021deep.
```


```{figure} /assets/figures/evaluation/APE_FxNorm.svg
:name: ape_fxnorm
:width: 70%
:align: center

APE test from~\cite{martinez2022automatic}. For this test, dry stems were used as references. This is based on feedback from pilot tests and was proposed by the expert participants.
```

## Criteria

The most common criterion used in multi-stimulus testing is to ask participants to rate various mixes according to their overall preference. This encompasses both technical and subjective criteria and is often based on a scale from 0 to 1 or from 0 to 100, with or without the use of semantic labels associated with a certain range of the numerical scale {cite}`IMPbook19`. 

When looking for more detailed and discriminatory perceptual ratings, the general preference criterion can be divided into Production Value, Clarity and Excitement as shown in {cite}`pestana2014cross, martinez2022automatic`, which are defined as follows:

- **Production Value**: Technical quality of the mix. This corresponds to subjective preferences related to the overall technical quality of the mix, considering all the audio mixing characteristics; such as dynamics, EQ, balance, and stereo image.
- **Clarity**: Ability to differentiate musical sources. This is entirely objective and corresponds to the perceived presence or absence of masking.
- **Excitement** A non-technical subjective reaction to the mix. This is not related to an evaluation of quality, but to a more personal perception of novelty. Due to engaging, intriguing or thought-provoking aspects within the mix.

It is worth noting that while the Clarity criterion measures the presence or absence of masking, this criterion is not objectively universal, and for certain genres or submixes, masking might be aesthetically desirable. However, Clarity can serve as an indicator for objective perceptual performance within mixes.

## Advice

The following are a set of general rules of thumb design decisions, and although they are not exhaustive, they can serve as a fundamental starting point when designing listening tests for automatic music mixing systems. 

- Participants should be blind to the stimulus as much as possible, thus, participants must not be informed of the underlying methods to generate the mixes. The contrary could lead to a negative bias towards fully automated generated mixes.
- Randomize the order of the stimuli and mixtures to be tested.
- Results when participants have experience in mix engineering are more reliable.
- Conduct a pilot listening test to get a clear idea of the approximate total duration and to recognize potential misunderstanding issues.
- Always write detailed instructions and, if possible, also provide verbal instructions to the participants to minimize the risk of misunderstandings within the task.
- Consider excluding participants if their total testing time is too short or if there are large deviations when compared to the other participants. However, when this occurs, please do report the exclusion of such participants.
- Collect additional data, such as age, gender identity, years of mixing experience, and comments regarding the test. This could lead to additional insights and findings from the test.
- The maximum total duration of a listening test in which listening fatigue does not affect the reliability of the results is 90 minutes {cite}`schatz2012impact}. However, such findings included a 10-minute break. Therefore, a recommendation is to keep the duration of the listening test under 45 minutes.
- A training stage preceding the test may be beneficial to participants. This stage must be taken into account within the total duration of the test.
- To assess various audio effects or mixing characteristics of mixes, experts prefer segments between 25 and 60 seconds. Typically, such a segment should cover a verse and a chorus or at least the transition between said musical parts.
- Do not use a ground truth reference unless the specific task at hand deems it necessary.
- Low and mid anchors tend not to be necessary if participants are skilled or experienced in mix engineering.
- The number of stimuli per multi-stimulus test page must be less than 12 {cite}`IMPbook19`.
- If labels are assigned to the rating scale, they must be properly defined and explained to the participants. Examples of such labels can be "Bad, Poor, Fair, Good, Excellent".
- Participants prefer synchronized playback between stimuli so they can better focus on contrast differences between mixes.
- Loudness should not influence the rated criteria. Therefore, samples must be loudness normalized, except for the cases where loudness is crucial to the criteria to be rated.
- Participants must limit the times they adjust the volume of their listening settings. Ideally this should be done once and only at the beginning of the test. These instructions must be given to the participants.


## Platforms


The following are the most common used platforms for perceptual listening tests:

### Web Audio Evaluation Tool 
{cite}`jillings2015web`
- APE and MUSHRA
- Reference is optional
- Training stage is possible 
- Loudness normalization within the platform 
- Synchronized playback
- Customization requires effort
 
### webMUSHRA  
{cite}`schoeffler2018webmushra`
- MUSHRA
- Training stage is possible
- Fade-in/out within the platform
- Synchronized playback
- Customization requires effort
 
### goListen 
{cite}`zhang2021golisten`
- MUSHRA
- Reference is optional
- Synchronized playback
- Customization requires effort
- Ease-of-use and implementation

## Challenges

It is worth noting that another limitation of the objective and subjective evaluation methods discussed above is the inability to measure whether the generated mixes have long-temporal coherence. This is because a song's mixing style is usually consistent throughout the song's length—and often throughout the entire album or EP—so we should investigate whether automatic mixing systems produce mixes with this level of coherence, which means that methods to measure this long-temporal coherence must be researched. For example, evaluation systems that measure mixing style coherence within different song elements such as verses, choruses, and so on, could yield more accurate objective and subjective ways of evaluating generated mixes.