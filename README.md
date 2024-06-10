# J-SpAW: Japanese speech corpus for speaker verification and anti-spoofing / 話者照合となりすまし検出のための日本語音声コーパス

J-SpAW コーパスは，話者照合と音声なりすまし検出を目的とした，人間の実発話音声と攻撃者によるなりすまし音声を含むコーパスです．


## Description / 内容
こちらのリポジトリでは、話者照合の評価のためのリストとLAタスクおよびPAタスクの評価のためのメタラベルを公開します。
内容は以下のとおりです。
* ASV_LIST.txt
    * 話者照合のためのリスト(本人：7600ペア、他人：30000ペア)
* metadata_LA.txt
    * LAタスクのためのメタデータ
* metadata_PA.txt
    * PAタスクのためのメタデータ


音声は情報科学研究データリポジトリ(-----)を通しての配布を予定しています。


## 音声ファイル名について
音声ファイルの命名規則は以下のようになっています。

### ASV
```sh
F001_R1_E1_M1_AA.wav
```
* `F001`:話者ID
* `R1`：収録場所(実収録)
* `E1`：収録環境(実収録)
* `M1`：収録機器(実収録)
* `AA`：発話内容
### LA
```sh
F001_R1_E1_L1_BT.wav
```
* `F001`:ターゲット話者ID
* `R1`：ターゲット音声収録場所
* `E1`：ターゲット音声収録環境
* `L1`：合成手法
* `AA`：発話内容
### PA
```sh
F001_R1_E1_M3_s1_r1_e1_m1_AA.wav
```
* `F001`:ターゲット話者ID
* `R1`：ターゲット音声収録場所
* `E1`：ターゲット音声収録環境
* `M3`：ターゲット音声収録機器
* `s1`：盗聴音声再生機器
* `r1`：なりすまし音声収録場所(PA)
* `e1`：なりすまし音声収録環境(PA)
* `m1`：なりすまし音声収録機器
* `AA`：発話内容


それぞれのIDの詳細は以下のようになっています。
* 収録場所：縦 (m) x 横 (m) x 高さ (m)
    * `R1,r1`: 00 x 00 x 00 
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
    * `s1`: BOSE Slink Micro 
    * `s2`: iPad mini (第5世代)
    * `s3`: MacBook Pro
    * `s4`: Sony SRS-ZR7


## メタラベルについて
metadata_LA.txt、metadata_PA.txtはASVspoof2021におけるメタラベルの書き方を参考にしています。
またこれらを利用することで、ASVspoof2021のeval-packageでEER、t-DCFの評価を行うことができます。
その際、J-SpAWの各環境ごとにEER,t-DCFの評価を行いたい場合はASVspoof2021/eval-package/config.pyを修正してください。

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
* 実発話収録環境
  * `R1 - R4`: 収録場所
  * `M1 - M3`: 収録機器
  * `E1 - E4`: 収録環境
* なりすまし音声収録環境
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
