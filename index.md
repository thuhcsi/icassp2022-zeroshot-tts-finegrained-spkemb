---
layout: default
---
# Abstract

Zero-shot speaker adaptation aims to investigate how to better clone an unseen speaker's voice without any adaptation time and parameters. Previous attempts usually use a speaker encoder to extract a global fixed speaker embedding from the reference audio. Such global embedding lacks the ability to model diverse fine-grained speaker characteristics for personalized pronunciation phenomena, and leads to poor speaker similarity in terms of detailed speaking styles and pronunciation habits. To improve the ability of speaker encoder to model fine-grained speaker characteristics, we propose content-dependent fine-grained speaker embeddings for zero-shot speaker adaptation. Instead of modeling the temporal relations, a reference attention module is introduced to model the content relevance between the reference audio and input text, and to generate the fine-grained speaker embeddings for each output of the phoneme encoder. The experimental results show that our proposed method outperforms the baselines using utterance-level global speaker embedding, and significantly improves the similarity of fine-grained speaker characteristics for unseen speakers. Furthermore, the speaker embeddings with different granularity from reference audio impacts the intelligibility and similarity of synthesized speech.

# Subjective Evaluation 
To demonstrate that our proposed fine-grained method outperforms two baselines using utterance-level speaker embedding, some samples are provided for comparison. **GSE** means global speaker embedding and **CLS** means jointly-trained speaker classifier, which are described in detail in the paper. In SpeakerID, **(S)** means **seen speaker** in the training set and **(US)** means **unseen speaker**.  A reference audio is the only reference for zero-shot speaker adaptation TTS, thus we hope the synthesized speech is more similar to **the reference audio both in global timbre and local variations (speaking style or pronunciation habit).** *In addition, several samples synthesize the same content as the reference audio, for better comparison.*

| SpeakerID | Reference Audio | Target Chinese Text | GSE | CLS | CDFSE |
| :---- | :---- | :---- | :---- | :---- | :---- |
| SSB1108  (S) | <audio controls><source src="./wavs/reference/SSB11080300.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 夜空中最亮的星，张杰。 | <audio controls><source src="./wavs/gst/SSB1108R05.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cls/SSB1108R05.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB1108R05.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0112 (US) | <audio controls><source src="./wavs/reference/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 没有这么简单。 | <audio controls><source src="./wavs/gst/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cls/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0393 (US) | <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 你好。 | <audio controls><source src="./wavs/gst/SSB0393L0.wav" type="audio/wav">Your browser does not support the audio element.</audio> influenced by RefAudio length  | <audio controls><source src="./wavs/cls/SSB0393L0.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB0393L0.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0710 (US) | <audio controls><source src="./wavs/reference/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 白云出演的电视剧有什么。 | <audio controls><source src="./wavs/gst/SSB07100002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cls/SSB07100002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB07100002.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1630 (US) | <audio controls><source src="./wavs/reference/SSB16300375.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 宝安中心区，宝安、西乡两区，房价也出现微跌。 | <audio controls><source src="./wavs/gst/SSB16300002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cls/SSB16300002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB16300002.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1782 (US) | <audio controls><source src="./wavs/reference/SSB17820001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 我要知道那天发生的每一件事。 | <audio controls><source src="./wavs/gst/SSB17820006.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cls/SSB17820006.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB17820006.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1935 (US) | <audio controls><source src="./wavs/reference/SSB19350001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 为了观察不同长度的对齐现象，我们今天就来合成一句非常长的句子试试看。 |<audio controls><source src="./wavs/gst/SSB1935L9.wav" type="audio/wav">Your browser does not support the audio element.</audio>  influenced by RefAudio length | <audio controls><source src="./wavs/cls/SSB1935L9.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB1935L9.wav" type="audio/wav">Your browser does not support the audio element.</audio> |


* * *


# Ablation Study 
### Investigation on speaker embeddings with different granularity 
To investigate the impact of local speaker embeddings with different granularity, we adjust the kernel size of average pooling layer in the downsample encoder. The number after CDFSE- represents the **overall downsampling times** in the temporal resolution compared with the reference mel-spectrogram. It can be observed that, with smaller downsampling times, more fine-grained local speaker embeddings can be extracted from reference audio, which can improve speaker similarity but result in deterioration of intelligibility.

| SpeakerID | Reference Audio | Target Chinese Text | CDFSE-1 | CDFSE-4 | CDFSE-16 | CDFSE-64 |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| SSB0112 | <audio controls><source src="./wavs/reference/SSB01120001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 一三三三七零八零七八七。 | <audio controls><source src="./wavs/cdfse-1/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB01120002.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0393 | <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 如新兴区域的望京奥运村地区。 | <audio controls><source src="./wavs/cdfse-1/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB03930005.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB0710 | <audio controls><source src="./wavs/reference/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 甜心特工国语版。 | <audio controls><source src="./wavs/cdfse-1/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB07100001.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1020 | <audio controls><source src="./wavs/reference/SSB10200001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 将依据发行人的信息披露文件进行独立的投资判断。 | <audio controls><source src="./wavs/cdfse-1/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB10200009.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| SSB1630 | <audio controls><source src="./wavs/reference/SSB16300375.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 广州的电影有什么。 | <audio controls><source src="./wavs/cdfse-1/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-4/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-16/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-64/SSB16300008.wav" type="audio/wav">Your browser does not support the audio element.</audio> |


### Investigation on preprocessing operations
We have tried to remove the preprocessing operations (slice, shuffle & concatenate) mentioned in the paper 2.3 during training, and find it will result in synthesized speech with strange prosody and poor intelligibility for zero-shot inference.

| Reference Audio | Target Chinese Text | w preprocessing | w/o preprocessing |
| :---- | :---- | :---- | :---- |
| <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 看来我现在是个真正的作家了。 | <audio controls><source src="./wavs/cdfse-16/SSB03930007.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-woshuffle/SSB03930007.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| <audio controls><source src="./wavs/reference/SSB06060001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 智能硬件需要软件平台交互数据。 | <audio controls><source src="./wavs/cdfse-16/SSB06060003.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-woshuffle/SSB06060003.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| <audio controls><source src="./wavs/reference/SSB10200001.wav" type="audio/wav">Your browser does not support the audio element.</audio> | 私募债券的投资风险由投资者自行承担。 | <audio controls><source src="./wavs/cdfse-16/SSB10200104.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/cdfse-woshuffle/SSB10200104.wav" type="audio/wav">Your browser does not support the audio element.</audio> |


* * *


# Case Study
We have plotted some alignment samples from reference attention module. It can be observed that the reference attention module successfully learns the right content alignment between reference audio and text, providing the interpretability of our proposed method.

**Sample 1**

Reference Audio: <audio controls><source src="./wavs/reference/SSB03930001.wav" type="audio/wav">Your browser does not support the audio element.</audio>

Content: 仅在与之利益密切相关的特定事项上享有表决权。（jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 .）


| Target Chinese Text（Phoneme Sequence） | CDFSE | Reference Alignment |
| :---- | :---- | :---- |
| 你好。（ni2 hao3 .） | <audio controls><source src="./wavs/casestudy/L0.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L0.jpg" width="100%"> |
| 仅在表决权，仅在表决权。（jin3 zai4 biao3 jue2 quan2 , jin3 zai4 biao3 jue2 quan2 .） | <audio controls><source src="./wavs/casestudy/L1.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L1.jpg" width="100%"> |
| 仅在与之利益密切相关的特定事项上享有表决权。（jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 .） | <audio controls><source src="./wavs/casestudy/L2.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L2.jpg" width="100%"> |
| 仅在与之利益密切相关的特定事项上享有表决权，仅在与之利益密切相关的特定事项上享有表决权。（jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 , jin3 zai4 yu3 zhi1 li4 yi4 mi4 qie4 xiang1 guan1 de5 te4 ding4 shi4 xiang4 shang4 , xiang2 you2 biao3 jue2 quan2 .） | <audio controls><source src="./wavs/casestudy/L3.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L3.jpg" width="100%"> |
| 为了观察不同长度的对齐现象，我们今天就来合成一句非常长的句子试试看。（wei4 le2 guan1 cha2 bu4 tong2 chang2 du4 de5 dui4 qi2 xian4 xiang4 , wo3 men1 jin1 tian1 jiu4 lai2 he2 cheng2 yi2 ju4 fei1 chang2 chang2 de5 ju4 zi5 shi4 shi4 kan4 .） | <audio controls><source src="./wavs/casestudy/L4.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L4.jpg" width="100%"> |


**Sample 2**

Reference Audio: <audio controls><source src="./wavs/reference/SSB19350001.wav" type="audio/wav">Your browser does not support the audio element.</audio>

Content: 六十三万四千一百七十八。（liu4 shi2 san1 wan4 si4 qian1 yi1 bai3 qi1 shi2 ba1 .）

| Target Chinese Text（Phoneme Sequence） | CDFSE | Reference Alignment |
| :---- | :---- | :---- |
| 你好。（ni2 hao3 .） | <audio controls><source src="./wavs/casestudy/L5.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L5.jpg" width="80%"> |
| 六十三万。（liu4 shi2 san1 wan4 .） | <audio controls><source src="./wavs/casestudy/L6.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L6.jpg" width="80%"> |
| 六十三万四千一百七十八。（liu4 shi2 san1 wan4 si4 qian1 yi1 bai3 qi1 shi2 ba1 .） | <audio controls><source src="./wavs/casestudy/L7.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L7.jpg" width="80%"> |
| 八十七百一千四万三十六。（ba1 shi2 qi1 bai3 yi1 qian1 si4 wan4 san1 shi2 liu4 .） | <audio controls><source src="./wavs/casestudy/L8.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <img src="./wavs/casestudy/refalign_L8.jpg" width="80%"> |
| 为了观察不同长度的对齐现象，我们今天就来合成一句非常长的句子试试看。（wei4 le2 guan1 cha2 bu4 tong2 chang2 du4 de5 dui4 qi2 xian4 xiang4 , wo3 men1 jin1 tian1 jiu4 lai2 he2 cheng2 yi2 ju4 fei1 chang2 chang2 de5 ju4 zi5 shi4 shi4 kan4 .） | <audio controls><source src="./wavs/casestudy/L9.wav" type="audio/wav">Your browser does not support the audio element.</audio> |<img src="./wavs/casestudy/refalign_L9.jpg" width="80%">|





