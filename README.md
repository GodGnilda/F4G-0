# FINAL FANTASY IV 改造サウンドドライバ F4G-0

## 概要
F4G-0 は FINAL FANTASY IV のシーケンスコマンドをそのまま利用可能な改造サンドドライバです。  
音楽演奏速度の安定を重視しています。  
若干ですが、データ転送やコピーに要する時間がオリジナルよりも短縮されます。  
[シーケンスコマンド](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html)が 14 追加されています。既存のコマンドの動作を変更することが可能になりました。  
後期の SNES Akao ドライバとほぼ同じピッチ計算 (微調整) が可能です。

## 仕様
- 音楽ヘッダとシーケンスデータ
  - データサイズ
    |サウンドドライバ|効果音|サイズ|
    |:-:|:-:|:--|
    |オリジナル|✔|$1000 (4096) バイト|
    |F4G-0|✔|$1050 (4176) バイト|
    |F4G-0||$1250 (4688) バイト|
- 常駐圧縮波形データ
	- 波形番号 2 ～ 8
- 非常駐圧縮波形データ
	- 波形番号 9 ～ 33
	- データサイズ
      |サウンドドライバ|効果音|常駐圧縮波形データ|サイズ|
      |:-:|:-:|:-:|:--|
      |オリジナル|✔|✔|$8300 (33536) バイト|
      |オリジナル||✔|$9A70 (39536) バイト|
      |オリジナル|||$A000 (40960) バイト|
      |F4G-0|✔|✔|$8C00 (35840) バイト|
      |F4G-0||✔|$A37B (41851) バイト|
      |F4G-0|||$A900 (43264) バイト|
- ハードウェア ADSR モード
  - 設定を変更可能  
FINAL FANTASY V や Romancing Sa·Ga 2 などの ROM データの値を使用可能 (シーケンスコマンド [$FE](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#FE))
- ピッチ計算 (キーオン・ピッチスライド)
	- 二つの微調整値を使用してピッチを計算  
FINAL FANTASY V や Romancing Sa·Ga 2 などの ROM データの値を使用可能 (シーケンスコマンド [$FE](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#FE))

## サウンドドライババージョン
APU RAM $B5F0 ～ $B5FF の 16 バイトをご確認ください。

## 使用方法
- **日本語**かつ**イージータイプではない** FINAL FANTASY IV の ROM イメージファイル (1,048,576 バイト) に IPS ファイルを適用します。
- [Snes9x](https://github.com/snes9xgit/snes9x) などで SPC ファイルを保存します。
- [FINAL FANTASY IV 改造サウンドドライバ : 音楽シーケンスデータ生成ツール]()で音楽データを作成します。
- 音楽データと波形データを[スクリプトファイル](https://github.com/GodGnilda/Script700/tree/main/F4G)で転送し、スナップショットを作成します。

## 演奏可能な曲 (ROM データ)
最新版 (F4G-0 20211122-0) の[スクリプトファイル](https://github.com/GodGnilda/Script700/tree/main/F4G)で演奏可能なデータです。  
[FINAL FANTASY IV 改造サウンドドライバ で ROM のデータを使用して音楽を演奏するスクリプト](https://github.com/GodGnilda/Script700/blob/main/F4G/F4G_F4G.700)でスナップショットを保存しお楽しみください。  
データに不備等がございましたらお手数ですが [Issue](https://github.com/GodGnilda/F4G-0/issues) にてご指摘のほどよろしくお願いいたします。

  |ID|曲名|[bsnes](https://github.com/bsnes-emu/bsnes)|[Snes9x](https://github.com/snes9xgit/snes9x)|[スクリプトファイル](https://github.com/GodGnilda/Script700/tree/main/F4G)|
  |--:|:--|:-:|:-:|:-:|
  |$01|オープニング|✔|✔|✔|
  |$04|チョコボ|✔|✔|✔|
  |$08|勝利のファンファーレ|✔|✔|✔|
  |$09|街のテーマ|✔|✔|✔|
  |$0D|ファイナルファンタジー IV メインテーマ|✔|✔|✔|
  |$13|愛のテーマ|✔|✔|✔|
  |$14|バロン王国|✔|✔|✔|
  |$15|プレリュード|✔|✔|✔|
  |$26|踊り子|✔|✔|✔|
  |$27|バトル 1|✔|✔|✔|
  |$2B|チョコボの森|✔|✔|✔|
  |$2C|赤い翼 (ニューゲーム)|✔|✔|✔|
  |$2D|疑惑のテーマ|✔|✔|✔|
  |$31|もう一つの月|?|?|✔|
  |$33|ミシディア国|?|?|✔|

## 既知の不具合
- ゲームプレイ中に音楽が正しく演奏されない  
演奏不可能な曲 <!--または 転送に失敗する曲-->を APU メモリに転送しているため発生します。  
オープニングロール後のバロン城周辺 (フィールドマップとバロンの町) までは安全にプレイ可能です。
- ゲームがフリーズする。  
正しく演奏されない曲を APU メモリに転送した場合、サウンドドライバがフリーズする可能性があります。

## 免責事項
本パッチは無償で提供されるものであり、現状有姿の状態で提供され、明示的/暗黙的かどうかに拘らずあらゆる保証はないものとします。ここでの保証とは、市販性、特定用途への適合性、権利の侵害がないことなどを含みますが、これらに限定されません。作成者または著作権保持者は、契約行為、不正行為、またはそれ以外の行為において、本パッチに起因または関連する事項、本パッチの使用、またはその扱いによって生じる一切の請求、損害、その他の義務について責任を負わないものとします。

## 動画
- [F4G-0 20210922-0 | FINAL FANTASY IV : もう一つの月 (Another Moon),Romancing Sa·Ga 2 : バトル 1 (Battle 1)](https://www.youtube.com/watch?v=QpJulN7gBzc)
- [F4G-0 20211001-0 | FINAL FANTASY IV : ミシディア国 (Mystic Mysidia),FINAL FANTASY V : ビッグブリッヂの死闘 (Battle at the Big Bridge)](https://www.youtube.com/watch?v=t1yGqDoEdcM)
- [F4G-0 20211122-0 | クイックタイム状態でのオリジナルとの演奏速度の比較。](https://twitter.com/god_gnilda/status/1462795616036089858)
- [F4G-0 20211122-0 | クイックタイム状態での Romancing Sa·Ga 2 との演奏速度の比較。](https://twitter.com/god_gnilda/status/1462796898905968647)

## 更新履歴
- 2021/11/24 [F4G-0 20211124-0]
  - サウンドドライバファンクション $03 を使用すると音楽データを正しく転送できない不具合を修正。
  - シーケンスコマンド $DF の処理を一部省略し 2 サイクル高速化。
  - シーケンスコマンド $F1 の処理を 2 サイクル高速化。
- 2021/11/22 [F4G-0 20211122-0]
  - 公開。
