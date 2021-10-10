---
layout: default
---
## Processing......
# Subjective Evaluation


| No. | Chinese Text | WRF | Proposed |
| :---- | :---- | :---- | :---- |
| 1 | 你猜我猜你猜不猜。 | <audio controls><source src="./wavs/wrf/wav-batch_7_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/bnm/wav-batch_7_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> |
| 2 | 家庭成员一般在除夕夜聚会吃年夜饭庆祝。 | <audio controls><source src="./wavs/wrf/wav-batch_8_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/bnm/wav-batch_8_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> |

* * *


# Ablation Study of Nulear-norm Maximization Loss 


| No. | Chinese Text | Without NML | With NML (Proposed) |
| :---- | :---- | :---- | :---- |
| 1 | 你猜我猜你猜不猜。 | <audio controls><source src="./wavs/withoutbnm/wav-batch_7_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/bnm/wav-batch_7_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> |

* * *


# Sentences with multiple different syntactic parse trees 
## (displayed as different word segmentation results)


| No. | Chinese Text | WRF | Proposed |
| :---- | :---- | :---- | :---- |
| 1 | 白天鹅 在湖上游泳。["白天鹅", "在", "湖上", "游泳"] | <audio controls><source src="./wavs/wrf/wav-batch_59_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> | <audio controls><source src="./wavs/bnm/wav-batch_59_sentence_0-linear.wav" type="audio/wav">Your browser does not support the audio element.</audio> |

