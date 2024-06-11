# J-SpAW: Japanese corpus for speaker verification and spoofing attack detection, recorded in the wild / 話者照合となりすまし音声検出のための日本語音声コーパス
English follows Japanese.

J-SpAW (ジェイ・スポウ) コーパスは，話者照合となりすまし音声検出を目的とした，人間の実発話音声と攻撃者によるなりすまし音声を含むコーパスです．

The J-SpAW (pronounced j-spo) is a corpus aiming at speaker verification and anti-spoofing verification. This includes bona fide speech and spoofing attacks.

## Download / ダウンロード
[Link](https://google.co.jp) (zip, xx GB)

## Description / 内容
こちらのリポジトリでは，話者照合 (ASV) の評価のためのリストと，なりすまし音声検出における LA (logical attack) タスクおよび PA (physical attack) タスクの評価のためのメタラベルを公開します．
内容は以下のとおりです．

- wav/ ... 音声ファイルのディレクトリ
    - ASV/*.wav ... 話者照合 (ASV)
    - LA/*.wav ... なりすまし音声検出 LA タスク
    - PA/*.wav ... なりすまし音声検出 PA タスク
- eval_package/
    - ASV_trial.txt ... 話者照合のためのトライアルリスト(本人同士：7600ペア, 他人同士：30000ペア)
    - metadata_LA.txt ... LAタスクのためのメタデータ(実発話：800トライアル, なりすまし：1600トライアル)
    - metadata_PA.txt ... PAタスクのためのメタデータ(実発話：800トライアル, なりすまし：6300トライアル)
    - config.py ... ASVspoof2021のeval-packageを本データベースに適用させるためのconfigファイル


英語


## メタラベルについて
metadata_LA.txt, metadata_PA.txtはASVspoof2021におけるメタラベルの書き方を参考にしています．
これらを利用することで, ASVspoof2021のeval-packageでEER, t-DCFの評価を行うことができます．
その際, J-SpAWの各環境ごとにEER, t-DCFの評価を行いたい場合はASVspoof2021のeval-packageのconfig.pyを, 本パッケージに含まれているconfig.pyと差し替えてください．

メタラベルで使われている各記号の意味を説明します．

### LAタスク
```sh
F001 F001_R1_E2_L1_BT - E2 L1 spoof notrim eval
```
* `F001`: 話者IDまたはなりすまし対象話者ID
* `F001_R1_E2_L1_BT`: トライアルID
* `-`：ASVspoof2021におけるメタラベルと列数を合わせるための調整
* `E2`：なりすまし音声を生成する際に用いた実発話の収録環境
    * `E1`: 静かな室内
    * `E2`: 空調が動作している室内
    * `E3`: 背景音楽が流れている室内
    * `E4`: 屋外
* `L1`：音声合成手法
    * `L1`：VALL-E X [1]
    * `L2`：TTS [2]
* `spoof`：正解ラベル
    * `bonafide`：実発話
    * `spoof`：なりすまし音声
* `notrim`：非発話区間のトリミングの有無
    * `notrim`：トリミングなし(本データベースではnotrimのみ)
* `eval`：サブセットの種類
    * `eval`：評価データ(本データベースではevalのみ)

[1] Ziqiang Zhang, Long Zhou, et al, ”speak foreign languages with your own voice: Cross-lingual neural codec language modeling,” arXiv:2303.03936(2023)

[2] Kenntaro Seki, Shinnosuke Takamichi, Takaaki Saeki, and Hiroshi Saruwatari, ”text-to-speech synthesis from dark data with evaluation-in-the-loop data selection,” Proc. 2023 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP).

### PAタスク
```sh
F001 F001_R1_E2_M3_s1_r1_e1_m1_AA R1 M3 E2 r1 m1 s1 e1 spoof notrim eval
```


* `F001`: 話者IDまたはなりすまし対象話者ID
* `F001_R1_E2_M3_s1_r1_e1_m1_AA`: トライアルID
* なりすまし対象話者の実発話収録
  * `R1 - R4`: 収録場所ID
  * `M1 - M3`: 収録機器ID
  * `E1 - E4`: 収録環境ID
* 攻撃者によるなりすまし音声収録
  * `r1 - r4`: 収録場所ID
  * `m1 - m3`: 収録機器ID
  * `s1 - s4`: 再生機器ID
  * `e1 - e4`: 収録環境ID
* `spoof`：正解ラベル
    * `bonafide`：実発話
    * `spoof`：なりすまし音声
* `notrim`：非発話区間のトリミングの有無
    * `notrim`：トリミングなし(本データベースではnotrimのみ)
* `eval`：サブセットの種類
    * `eval`：評価データ(本データベースではevalのみ)
    --------------------------------------改行入れる
各IDの詳細は以下の音声ファイルの命名規則に記述してあります．

## 音声ファイルの命名規則
音声ファイルの命名規則は以下のようになっています．

### ASV
```sh
{spkr_id}_{room_id}_{env_id}_{mic_id}_{sent_id}.wav
```
* `{spkr_id}`:話者ID (F001--F019, M001--M021 の 40 話者)
* `{room_id}`：収録場所ID (実発話収録, R1--R4 の 4 場所)
* `{env_id}`：収録環境ID (実発話収録, E1--E4 の 4 環境)
* `{mic_id}`：収録機器ID (実発話収録, M1--M3 の 3 種類)
* `{sent_id}`：発話テキストID (AA--BX の 50 文)

### LA
```sh
{spkr_id}_{room_id}_{env_id}_{LA_method_id}_{sent_id}.wav
```
* `{spkr_id}`:話者ID (F001-F019, M001-M021 の 40 話者)
* `{room_id}`：収録場所ID (実発話収録, R1--R4 の 4 場所)
* `{env_id}`：収録環境ID (実発話収録, E1--E4 の 4 環境)
* `{LA_method_id}`：音声合成手法 (L1--L2 の 2 種類)
* `{sent_id}`：発話テキストID (BT--BX の 5 文)

### PA
```sh
{spkr_id}_{room_id}_{env_id}_{mic_id}_{loudspeaker_id}_{room_id_replay}_{env_id_replay}_{mic_id_replay}_{sent_id}.wav
```
```sh
F001_R1_E1_M3_s1_r1_e1_m1_AA.wav
```
* なりすまし対象話者の実発話収録
    * `{spkr_id}`：話者ID (F001--F019, M001--M021 の 40 話者)
    * `{room_id}`：収録場所ID (実発話収録, R1--R4 の 4 場所)
    * `{env_id}`：収録環境ID (実発話収録, E1--E4 の 4 環境)
    * `{mic_id}`：収録機器ID (実発話収録, M1--M3 の 3 種類)
* 攻撃者によるなりすまし音声収録
    * `{loudspeaker_id}`：再生機器ID (再収録, s1--s4 の 4 種類)
    * `{room_id_replay}`：収録場所ID (再収録, r1 のみ)
    * `{env_id_replay}`：収録環境ID (再収録, e1--e3 の 3 種類)
    * `{mic_id_replay}`：収録機器ID (再収録, m1--m2 の 2種類)
    * `{sent_id}`：発話テキストID (AA--xx の 25 文)


それぞれのIDの詳細は以下のようになっています．
* 収録場所：縦 (m) x 横 (m) x 高さ (m)
    * `R1`: 00 x 00 x 00 
    * `r1`：11.0 x 8.0 x 2.6
    * `R2,r2`: 屋外1
    * `R3,r3`: 10.8 x 2.0 x 2.8
    * `R4,r4`: 屋外2
* 収録機器
    * `M1,m1`: Pixel3
    * `M2,m2`: iPhone8
    * `M3,m3`: iPad mini (第5世代)
* 収録環境
    * `E1,e1`: 静かな室内
    * `E2,e2`: 空調が動作している室内
    * `E3,e3`: 音楽が流れている室内
    * `E4,e4`: 屋外
* 再生機器
    * `s1`: Bose Soundlink Micro Bluetooth Speaker Bundle
    * `s2`: iPad mini (第5世代)
    * `s3`: MacBook Pro (13インチ, M2, 2022)
    * `s4`: Sony SRS-ZR7





## Terms of use / 使い方
- Non-commercial purpose only / 非商用利用に限る

## Contributors / 作成者
- Kouta Kanno / 菅野 滉大 (Tokyo Metropolitan University / 東京都立大学)
- Shinnosuke Takamichi / 高道 慎之介 (Keio University / 慶應義塾大学)
- Sayaka Shiota / 塩田 さやか (Tokyo Metropolitan University / 東京都立大学)


## Paper / 論文
- 菅野 滉大, 高道 慎之介, 塩田 さやか, "J-SpAW:話者照合となりすまし検出のための日本語音声コーパス" 情報処理学会 音声言語処理研究会 , 2024
