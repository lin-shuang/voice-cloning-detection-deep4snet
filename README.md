# Voice Cloning Detection: Deep4SNet Counter to SiF-DeepVC

Shuang Lin, BS. COGS || Thomas Snipes, MS. CSE


We will improve upon the Deep4SNet deep learning CNN model to counter the voice clones that have been camouflaged by the SiF-DeepVC method.


# Motivation
![Impersonation](/Docs/CSE398_498%20-%20Deep%20Learning%20-%20Final%20Presentation.pdf#page=2)
<object data="/Docs/CSE398_498%20-%20Deep%20Learning%20-%20Final%20Presentation.pdf#page=2" type="application/pdf" width="100%" height="600px">
    <p>PDF could not be displayed.</p>
</object>
The doctor's voice is cloned to advertise a product as "doctor approved".
https://www.instagram.com/reel/CztzP8Cx3Yj/?utm_source=ig_web_copy_link
 
![Device Hijack](W#page=2)
The smart speaker in your home can be subject to hijacking. The attacker can then, execute execute on your Siri, Alexa, Google Home, etc. [5]


# Deep4SNet
![Deep4SNet](W#page=5)
The backbone of our model follows the Deep4SNet
CNN architecture [3]. The Deep4SNet model takes
histograms, converted from real and synthesized
speech audios, as its input. Deep4SNet is a convolutional neural network solution with image augmentation and dropout. 


# Data
![Data 1/2](W#page=7)
![Data 2/2](W#page=8)
We use original human recordings from the Fake-or-Real (FoR) Validation dataset and cloned fake voices
by SiF-DeepVC (SiF) for Farid et al., Deep4SNet, and
RawNet2 [5]. All 24640 audio files, provided by SiF-DeepVC, are in .wav format and pre-labeled by their
folder names. We sample 9000 files; 4500 fakes from
Farid et al. and RawNet2 and 4500 reals from FoR.
We also sampled 1000 files from their method against
Deep4SNet to test our model’s effectiveness against
their camouflage. The SiF dataset is split into three
sets following the general 70:30 rule: 70% training,
15% validation, and 15% test.

In order to emulate the original Deep4SNet model,
we also implemented the H-Voice dataset, which was
what their model trained on

# Filtering
![Filtering](/Docs/CSE398_498%20-%20Deep%20Learning%20-%20Final%20Presentation.pdf#page=9)
As mentioned in the introduction, SiF-DeepVC accounts for the fact that the human voice ranges from 300 - 3400 Hz by silencing anything below 4000
Hz, so we decided to implement a filter in hopes of
combating their approach. Our filter, applied before
converting the .wav files to histograms, blocks out all
frequencies above 4000 Hz. By doing so we ignore
their handcrafted SiFs, so they cannot trick our model.
Please note that this filtered data is treated as a
completely different dataset that we use for training,
validation, and testing independently.

# Results
![Results 1/3](W#page=13)
![Results 2/3](W#page=14)
![Results 3/3](W#page=15)
It seems that by training the Deep4SNet model
on other handcrafted SiF examples, it can prevent
the effects of camouflage in handcrafted SiFs, even
if it’s crafted specifically to bypass the model itself.
However, our model’s low accuracy in H-Voice means
that it is too specialized for camouflaged audio. From
observing the H-Voice histograms, we notice that some
of their audios are at a lower frequency. Sometimes,
not even exceeding 200 Hz. This means our model
is not used to dealing with lower frequencies, since
SiFs are mostly in higher frequencies, which might
have led to the lower accuracy when testing with H-Voice histograms. In the end, we found that the SiF
and H-Voice models perform well in their own scenarios, but do not generalize well. Our goal to bypass
the SiF-DeepVC’s camouflage was a success because
the brown models have maintained high performance
while achieving generalizability.

# References
[1] Ehab A. AlBadawy, Siwei Lyu, and Hany Farid. Detecting
ai-synthesized speech using bispectral analysis. In CVPR
Workshops, 2019.

[2] Dora M. Ballesteros, Yohanna Rodriguez, and Diego Renza.
A dataset of histograms of original and fake voice recordings
(h-voice). Data in Brief, 29:105331, 2020.

[3] Dora M. Ballesteros, Yohanna Rodriguez-Ortega, Diego Renza,
and Gonzalo Arce. Deep4snet: deep learning for fake speech
classification. Expert Systems with Applications, 184:115465,
2021.

[4] Dora Maria Ballesteros L, Yohanna Patricia Rodriguez, and
Diego Renza. H-voice: Fake voice histograms (imitation+deepvoice), 2020.

[5] Xin Liu, Yuan Tan, Xuan Hai, Qingchen Yu, and Qingguo Zhou.
Hidden-in-wave: A novel idea to camouflage ai-synthesized
voices based on speaker-irrelative features. In 2023 IEEE 34th
International Symposium on Software Reliability Engineering
(ISSRE), pages 786–794, 2023

[6] Hemlata Tak, Jose Patino, Massimiliano Todisco, Andreas
Nautsch, Nicholas Evans, and Anthony Larcher. End-to-end
anti-spoofing with rawnet2. In ICASSP 2021 - 2021 IEEE
International Conference on Acoustics, Speech and Signal Processing (ICASSP), pages 6369–6373, 2021