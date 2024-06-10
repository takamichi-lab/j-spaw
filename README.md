# J-SpAW: Japanese speech corpus for speaker verification and anti-spoofing / 話者照合となりすまし検出のための日本語音声コーパス
The Coco-Nut corpus is a corpus including Japanese voice and free-form texts describing the voice characteristics (hereinafter, characteristics prompt.)

J-SpAW コーパスは，話者照合と音声なりすまし検出を目的とした，人間の実発話音声と攻撃者によるなりすまし音声を含むコーパスです．


## Description / 内容
こちらのリポジトリでは、話者照合の評価のためのリストとLAタスクおよびPAタスクの評価のためのメタラベルを公開します。

音声は情報科学研究データリポジトリ(-----)を通しての配布を予定しています。


## On meta-labels

metadata_LA.txt、metadata_PA.txtはASVspoof2021におけるメタラベルの書き方を参考にしています。
最初の行を使用してメタラベルの意味を説明します。

### LA
```sh
F001 F001_R1_E2_L1_BT - E2 L1 spoof notrim eval
```
* `F001`: 話者IDまたはターゲット話者ID
* `F001_R1_E2_L1_BT`: トライアルID
* `-`：ASVspoof2021におけるメタラベルとの調整
* `E2`：合成に用いた実発話の収録環境(実収録)
    * `E1`: 静かな室内
    * `E2`: 空調が動作している室内
    * `E3`: 音楽が流れている室内
    * `E4`: 屋外
* `L1`：合成手法
    * `L1`：VALL-E X
    * `L2`：TTS
* `spoof`：キー
    * `bonafide`：実発話
    * `spoof`：なりすまし音声
* `notrim`：非発話区間のトリミングなし
* `eval`：サブセットの種類


### PA
```sh
F001 F001_R1_E2_M3_s1_r1_e1_m1_AA R1 M3 E2 r1 m1 s1 e1 spoof notrim eval
```


* `F001`: 話者IDまたはターゲット話者ID
* `F001_R1_E2_M3_s1_r1_e1_m1_AA`: トライアルID
* 実発話収録環境:
  * `R1 - R4`: 収録場所
  * `M1 - M3`: 収録機器
  * `E1 - E4`: 収録環境
* なりすまし音声収録環境:
  * `r1 - r4`: 収録場所
  * `m1 - m3`: 収録機器
  * `s1 - s4`: 再生機器
  * `e1 - e4`: 収録環境
* `spoof`：キー
    * `bonafide`：実発話
    * `spoof`：なりすまし音声
* `notrim`：非発話区間のトリミングなし
* `eval`：サブセットの種類


## Terms of use / 使い方
- Non-commercial purpose only / 非商用利用に限る

## Contributors / 作成者
- Kouta Kanno / 菅野 滉大 (Tokyo Metropolitan University / 東京都立大学)
- Shinnosuke Takamichi / 高道 慎之介 (Keio University / 慶應義塾大学)
- Sayaka Shiota / 塩田 さやか (Tokyo Metropolitan University / 東京都立大学)


## Paper / 論文
- 菅野 滉大, 高道 慎之介, 塩田 さやか, "J-SpAW:話者照合となりすまし検出のための日本語音声コーパス" 情報処理学会 音声言語処理研究会 , 2024
