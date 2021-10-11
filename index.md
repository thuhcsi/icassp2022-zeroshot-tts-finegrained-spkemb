---
layout: default
---
# Abstract

Zero-shot speaker adaptation aims to investigate how to better clone an unseen speaker's voice without any adaptation time and parameters. Previous attempts usually use a speaker encoder to extract a global fixed speaker embedding from the reference audio. Such global embedding lacks the ability to model diverse fine-grained speaker characteristics for personalized pronunciation phenomena, and leads to poor speaker similarity in terms of detailed speaking styles and pronunciation habits. To improve the ability of speaker encoder to model fine-grained speaker characteristics, we propose content-dependent fine-grained speaker embeddings for zero-shot speaker adaptation. Instead of modeling the temporal relations, a reference attention module is introduced to model the content relevance between the reference audio and input text, and to generate the fine-grained speaker embeddings for each output of the phoneme encoder. The experimental results show that our proposed method outperforms the baselines using utterance-level global speaker embedding, and significantly improves the similarity of fine-grained speaker characteristics for unseen speakers. Furthermore, the speaker embeddings with different granularity from reference audio impacts the intelligibility and similarity of synthesized speech.

# Subjective Evaluation
#### (S) means seen speaker in the training set and (US) means unseen speaker. A reference audio is the only reference for zero-shot speaker adaptation TTS, thus we hope the synthesized speech is more similar to the reference audio both in global timbre and local style or habit variations. 

| SpeakerID | Reference Audio | Chinese Text (Phoneme Sequence) | GSE | CLS | CDFSE |
| :---- | :---- | :---- | :---- | :---- | :---- |
| SSB0005 (S) | <audio controls><source src="./wavs/reference/SSB00050001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 家庭成员一般在除夕夜聚会吃年夜饭庆祝。 | <audio controls><source src="./wavs/gst/SSB00050001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cls/SSB00050001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB00050001.wav" type="audio/wav">Your browser does not support the audio element.</audio> |



* * *


# Ablation Study of speaker embeddings with different granularity 
#### All of them are unseen speakers.

| SpeakerID | Reference Audio | Chinese Text (Phoneme Sequence) | CDFSE-1 | CDFSE-4 | CDFSE-16 | CDFSE-64 |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| SSB0112 | <audio controls><source src="./wavs/reference/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 一三三三七零八零七八七。 | <audio controls><source src="./wavs/cdfse-1/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0393 | <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 如新兴区域的望京奥运村地区。 | <audio controls><source src="./wavs/cdfse-1/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0710 | <audio controls><source src="./wavs/reference/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 甜心特工国语版（tian2 xin1 te4 gong1 guo2 yu3 ban3）。 | <audio controls><source src="./wavs/cdfse-1/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1020 | <audio controls><source src="./wavs/reference/SSB10200001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 将依据发行人的信息披露文件进行独立的投资判断。 | <audio controls><source src="./wavs/cdfse-1/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1630 | <audio controls><source src="./wavs/reference/SSB16300375.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 广州的电影有什么。 | <audio controls><source src="./wavs/cdfse-1/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> |

* * *


# Sentences with multiple different syntactic parse trees 
## (displayed as different word segmentation results)


| No. | Chinese Text | WRF | Proposed |
| :---- | :---- | :---- | :---- |
| 1 | 白天鹅 在湖上游泳。["白天鹅", "在", "湖上", "游泳"] | <audio controls><source src="./wavs/wrf/wav-batch_59_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/bnm/wav-batch_59_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> |

