[![Build Status](https://travis-ci.org/makcedward/nlpaug.svg?branch=master)](https://travis-ci.org/makcedward/nlpaug)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/2d6d1d08016a4f78818161a89a2dfbfb)](https://www.codacy.com/app/makcedward/nlpaug?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=makcedward/nlpaug&amp;utm_campaign=Badge_Grade)
[![Codecov Badge](https://codecov.io/gh/makcedward/nlpaug/branch/master/graph/badge.svg)](https://codecov.io/gh/makcedward/nlpaug)

# nlpaug

This python library helps you with augmenting nlp for your machine learning projects. Visit this introduction to understand about [Data Augmentation in NLP](https://towardsdatascience.com/data-augmentation-in-nlp-2801a34dfc28). `Augmenter` is the basic element of augmentation while `Flow` is a pipeline to orchestra multi augmenter together.

## Augmenter
| Target | Augmenter | Action | Description |
|:---:|:---:|:---:|:---:|
|Character|RandomAug|Insert|Insert character randomly|
|||Substitute|Substitute character randomly|
|||Swap|Swap character randomly|
|||Delete|Delete character randomly|
||OcrAug|Substitute|Simulate OCR engine error|
||QwertyAug|Substitute|Simulate keyboard distnace error|
|Word|RandomWordAug|Swap|Swap word randomly|
|||Delete|Delete word randomly|
||WordNetAug|Substitute|Substitute word according to WordNet's synonym|
||Word2vecAug|Insert|Insert word randomly from [word2vec](https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a) dictionary|
|||Substitute|Substitute word based on [word2vec](https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a) embeddings|
||GloVeAug|Insert|Insert word randomly from [GloVe](https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a) dictionary|
|||Substitute|Substitute word based on [GloVe](https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a) embeddings|
||FasttextAug|Insert|Insert word randomly from [fasttext](https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a) dictionary|
|||Substitute|Substitute word based on [fasttext](https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a) embeddings|
||BertAug|Insert|Insert word based by feeding surroundings word to [BERT](https://towardsdatascience.com/how-bert-leverage-attention-mechanism-and-transformer-to-learn-word-contextual-relations-5bbee1b6dbdb) language model|
|||Substitute|Substitute word based by feeding surroundings word to [BERT](https://towardsdatascience.com/how-bert-leverage-attention-mechanism-and-transformer-to-learn-word-contextual-relations-5bbee1b6dbdb) language model|
|Spectrogram|FrequencyMaskingAug|Substitute|Set block of values to zero according to frequency dimension|
||TimeMaskingAug|Substitute|Set block of values to zero according to time dimension|
|Audio|NoiseAug|Substitute|Inject noise|
||PitchAug|Substitute|Adjust pitch|
||ShiftAug|Substitute|Shift time dimension forward/ backward|
||SpeedAug|Substitute|Adjust speed of audio |

## Flow
| Pipeline | Description |
|:---:|:---:|
|Sequential|Apply list of augmentation functions sequentially |
|Sometimes|Apply some augmentation functions randomly|



## Example
* How to use [character and word augmentation](https://github.com/makcedward/nlpaug/blob/master/example/overview.ipynb)
* How to create [custom augmentation](https://github.com/makcedward/nlpaug/blob/master/example/custom_augmenter.ipynb)
* How to use [spectrogram augmentation for speech recognition](https://github.com/makcedward/nlpaug/blob/master/example/spectrogram_augmenter.ipynb)
![Frequency Masking](https://github.com/makcedward/nlpaug/blob/master/res/spectrogram-frequency_masking.png)
![Frequency Masking](https://github.com/makcedward/nlpaug/blob/master/res/spectrogram-time_masking.png)
* How to use [audio augmentation for speech recognition](https://github.com/makcedward/nlpaug/blob/master/example/audio_augmenter.ipynb)

## Installation

The library supports python 3.5+ in linux and window platform.

To install the library:
```bash
pip install nlpaug
```
or install the latestion version from github directly
```bash
pip install git+https://github.com/makcedward/nlpaug.git
```


Download word2vec or GloVe files if you use `Word2VecAug`, `GloVeAug` or `FasttextAug`:
* word2vec([GoogleNews-vectors-negative300](https://code.google.com/archive/p/word2vec/))
* GloVe([glove.6B.50d](https://nlp.stanford.edu/projects/glove/))
* fasttext([wiki-news-300d-1M.vec.zip](https://fasttext.cc/docs/en/english-vectors.html))

## Recent Changes

**BETA** Jun 3, 2019: 
Added stopwords feature in character and word augmenter.
Added character's swap augmenter

**0.0.3** May 23, 2019: Added Speed, Noise, Shift and Pitch augmenters for Audio

**0.0.2** Apr 30, 2019: 
Added Frequency Masking and Time Masking for Speech Recognition (Spectrogram).
Added librosa library dependency for converting wav to spectrogram.

**0.0.1** Mar 20, 2019: Project initialization

## Test

```
Word2vec and GloVe models are used in word insertion and substitution. Those model files are necessary in order to run test case. You have to add ".env" file in root directory and the content should be
    - MODEL_DIR={MODEL FILE PATH}
```

```
Folder structure of model should be
    -- root directory
        - glove.6B.50d.txt
        - GoogleNews-vectors-negative300.bin
        - wiki-news-300d-1M.vec
```

## Research Reference
| Augmenter | Research |
|:---:|:---|
|RandomAug|D. Pruthi, B. Dhingra and Z. C. Lipton. [Combating Adversarial Misspellings with Robust Word Recognition](https://arxiv.org/pdf/1905.11268.pdf). 2019|
|WordNetAug|X. Zhang, J. Zhao and Y. LeCun. [Character-level Convolutional Networks for Text Classification](https://arxiv.org/pdf/1509.01626.pdf). 2015|
|FrequencyMaskingAug, TimeMaskingAug|D. S. Park, W. Chan, Y. Zhang, C. C. Chiu, B. Zoph, E. D. Cubuk and Q. V. Le. [SpecAugment: A Simple Data Augmentation Method for Automatic Speech Recognition](https://arxiv.org/pdf/1904.08779.pdf). 2019|
