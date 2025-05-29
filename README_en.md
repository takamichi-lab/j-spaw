# J-SpAW: Japanese corpus for speaker verification and spoofing attack detection, recorded in the wild
[日本語版はこちら](https://github.com/takamichi-lab/j-spaw/blob/main/README.md)

The J-SpAW (pronounced j-spou) corpus is designed for speaker verification and anti-spoofing verification, containing both bona fide speech and spoofing attacks.

## Download speech files
[Link](https://ss-takashi.sakura.ne.jp/corpus/j-spaw/j-spaw_ver1.zip) (zip, 4.9 GB)

## Contents
This repository provides lists for evaluating speaker verification (ASV) and meta-labels for evaluating logical attack (LA) and physical attack (PA) tasks in spoofing detection. The contents are as follows:

- `wav/`: Directory of speech files (download from the above URL, unzip, and place data into `wav/`.)
  - `ASV/*.wav`: Speaker verification (ASV)
  - `LA/*.wav`: Spoofing detection (LA task)
  - `PA/*.wav`: Spoofing detection (PA task)
- `eval_package/`
  - `ASV_trial.txt`: Trial list for ASV task (7600 genuine pairs, 30000 impostor pairs)
  - `metadata_LA.txt`: Metadata for LA task (800 genuine trials, 1600 spoofed trials)
  - `metadata_PA.txt`: Metadata for PA task (800 genuine trials, 6300 spoofed trials)
  - `config.py`: Configuration file to apply the ASVspoof2021 eval-package to this corpus

## Meta-labels
`metadata_LA.txt` and `metadata_PA.txt` follow the meta-label format of [ASVspoof2021](https://www.asvspoof.org/index2021.html). Using these, you can evaluate EER (equal error rate) and [t-DCF](https://arxiv.org/abs/1804.09618) (tandem detection cost function) with the ASVspoof2021 [eval-package](https://github.com/asvspoof-challenge/2021/tree/main/eval-package). To evaluate EER and t-DCF for each environment in J-SpAW, replace the ASVspoof2021 [config.py](https://github.com/asvspoof-challenge/2021/blob/main/eval-package/config.py) with the one included in this package. The meanings of the symbols used in the meta-labels are as follows:

### ASV Task (ASV_trial.txt)
```sh
1 F001_R1_E2_M2_BT.wav F001_R1_E2_M2_BU.wav
```
* `1`: Correct label
  * `1`: Genuine pair (speakers of two speech are the same)
  * `0`: Impostor pair (speakers of two speech are NOT the same)
* `F001_R1_E2_M2_BT.wav`: Enrollment speech
* `F001_R1_E2_M2_BU.wav`: Test speech

### LA Task (metadata_LA.txt)
```sh
F001 F001_R1_E2_L1_BT - E2 L1 spoof notrim eval
```
* `F001`: Speaker ID or target speaker ID
* `F001_R1_E2_L1_BT`: Trial ID
* `-`: Adjustment to match the number of columns in ASVspoof2021 meta-labels (ignore this)
* `E2`: Recording environment of the bona fide speech used to generate the spoofed speech
  * `E1`: Quiet indoor
  * `E2`: Indoor with air conditioning
  * `E3`: Indoor with background music
  * `E4`: Outdoor
* `L1`: Speech synthesis method
  * `L1`: VALL-E X [1]
  * `L2`: FastSpeech2 [2]
* `spoof`: Correct label
  * `bonafide`: bona fide speech
  * `spoof`: Spoofed speech
* `notrim`: Whether non-speech segments are trimmed
  * `notrim`: No trimming (only `notrim` is used in this database)
* `eval`: Subset type
  * `eval`: Evaluation data (only `eval` is used in this database)

### PA Task (metadata_PA.txt)
```sh
F001 F001_R1_E2_M3_s1_r1_e1_m1_AA R1 M3 E2 r1 m1 s1 e1 spoof notrim eval
```
* `F001`: Speaker ID or target speaker ID
* `F001_R1_E2_M3_s1_r1_e1_m1_AA`: Trial ID
* Bona fide speech recording of the target speaker
  * `R1 - R4`: Recording room ID
  * `M1 - M3`: Recording microphone ID
  * `E1 - E4`: Recording environment ID
* Spoofed speech recording by the attacker
  * `r1 - r4`: Recording room ID
  * `m1 - m3`: Recording microphone ID
  * `s1 - s4`: Playback loudspeaker ID
  * `e1 - e4`: Recording environment ID
* `spoof`: Correct label
  * `bonafide`: bona fide speech
  * `spoof`: Spoofed speech
* `notrim`: Whether non-speech segments are trimmed
  * `notrim`: No trimming (only notrim is used in this database)
* `eval`: Subset type
  * `eval`: Evaluation data (only eval is used in this database)

## Naming Format for Speech Files
### ASV Task
```sh
{spkr_id}_{room_id}_{env_id}_{mic_id}_{sent_id}.wav
```
* `{spkr_id}`: Speaker ID (40 speakers: F001--F019, M001--M021)
* `{room_id}`: Recording room ID (for bona fide speech, R1--R4)
* `{env_id}`: Recording environment ID (for bona fide speech, E1--E4)
* `{mic_id}`: Recording microphone ID (for bona fide speech, M1--M3)
* `{sent_id}`: Sentence ID (50 sentences: AA--BX)

### LA Task
```sh
{spkr_id}_{room_id}_{env_id}_{LA_method_id}_{sent_id}.wav
```
* `{spkr_id}`: Speaker ID (40 speakers: F001--F019, M001--M021)
* `{room_id}`: Recording room ID (for bona fide speech, R1--R4)
* `{env_id}`: Recording environment ID (for bona fide speech, E1--E4)
* `{LA_method_id}`: Speech synthesis method (L1--L2)
* `{sent_id}`: Sentence ID (5 sentences: BT--BX)

### PA Task
```sh
{spkr_id}_{room_id}_{env_id}_{mic_id}_{loudspeaker_id}_{room_id_replay}_{env_id_replay}_{mic_id_replay}_{sent_id}.wav
```
* bona fide speech recording of the target speaker
  * `{spkr_id}`: Speaker ID (40 speakers: F001--F019, M001--M021)
  * `{room_id}`: Recording room ID (for bona fide speech, R1--R4)
  * `{env_id}`: Recording environment ID (for bona fide speech, E1--E4)
  * `{mic_id}`: Recording microphone ID (for bona fide speech, M1--M3)
* Spoofed speech recording by the attacker
  * `{loudspeaker_id}`: Playback loudspeaker ID (for re-recording, s1--s4)
  * `{room_id_replay}`: Recording room ID (for re-recording, only r1)
  * `{env_id_replay}`: Recording environment ID (for re-recording, e1--e3)
  * `{mic_id_replay}`: Recording microphone ID (for re-recording, m1--m2)
  * `{sent_id}`: Sentence ID (25 sentences: AA--AY)

## Common Details Across Tasks
* Recording room ID: Dimensions (length x width x height in meters)
  * `R1`: 00 x 00 x 00 
  * `r1`: 11.0 x 8.0 x 2.6
  * `R2, r2`: Outdoor 1
  * `R3, r3`: 10.8 x 2.0 x 2.8
  * `R4, r4`: Outdoor 2
* Recording microphone ID:
  * `M1, m1`: Pixel3 
  * `M2, m2`: iPhone8
  * `M3, m3`: iPad mini (5th generation)
* Recording environment ID:
  * `E1, e1`: Quiet indoor
  * `E2, e2`: Indoor with air conditioning
  * `E3, e3`: Indoor with music
  * `E4, e4`: Outdoor
* Playback loudspeaker ID:
  * `s1`: Bose Soundlink Micro Bluetooth Speaker Bundle
  * `s2`: iPad mini (5th generation)
  * `s3`: MacBook Pro (13-inch, M2, 2022)
  * `s4`: Sony SRS-ZR7

## License
- For non-commercial use only

## Authors
- Suzuka Horie (Tokyo Metropolitan University)
- Kouta Kanno (Tokyo Metropolitan University)
- Shinnosuke Takamichi (Keio University)
- Sayaka Shiota (Tokyo Metropolitan University)

## Papers
- 菅野 滉大, 高道 慎之介, 塩田 さやか, "J-SpAW：話者照合となりすまし検出のための日本語音声コーパス," 情報処理学会 音声言語処理研究会, 2024
- Sayaka Shiota, Suzuka Horie, Kouta Kanno, Shinnosuke Takamichi, "Japanese speaker verification and spoofing attacks recorded in-the-wild dataset," Interspeech, 2025.

## References
[1] Ziqiang Zhang, Long Zhou, et al, ”speak foreign languages with your own voice: Cross-lingual neural codec language modeling,” arXiv:2303.03936(2023)

[2] Kenntaro Seki, Shinnosuke Takamichi, Takaaki Saeki, and Hiroshi Saruwatari, ”text-to-speech synthesis from dark data with evaluation-in-the-loop data selection,” Proc. 2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP).
