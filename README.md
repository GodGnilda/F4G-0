# FINAL FANTASY IV 改造サウンドドライバ F4G-0

## 概要
F4G-0 は FINAL FANTASY IV のシーケンスコマンドをそのまま利用可能な改造サンドドライバです。  
音楽演奏速度の安定を重視しています。  
若干ですが、データ転送やコピーに要する時間がオリジナルよりも短縮されます。  
[シーケンスコマンド](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html)が 14 追加されています。既存のコマンドの動作を変更することが可能になりました。  
後期の SNES AKAO ドライバとほぼ同じピッチ計算 (微調整) が可能です。

## 仕様
- 音楽ヘッダとシーケンスデータ
  - データサイズ
    |サウンドドライバ|効果音|サイズ|
    |:-:|:-:|:--|
    |オリジナル|✔|$1000 (4096) バイト|
    |F4G-0|✔|$1050 (4176) バイト|
    |F4G-0||$1250 (4688) バイト|
- 常駐圧縮波形データ
	- 波形番号 0 ～ 6
- 非常駐圧縮波形データ
	- 波形番号 7 ～ 31
	- データサイズ
      |サウンドドライバ|効果音|常駐圧縮波形データ|サイズ|
      |:-:|:-:|:-:|:--|
      |オリジナル|✔|✔|$8300 (33536) バイト|
      |オリジナル||✔|$9A70 (39536) バイト|
      |オリジナル|||$A000 (40960) バイト|
      |F4G-0|✔|✔|$9074 (36980) バイト|
      |F4G-0||✔|$A07B (41083) バイト|
      |F4G-0|||$A600 (42496) バイト|
- ハードウェア ADSR モード
  - 設定を変更可能  
FINAL FANTASY V や Romancing Sa·Ga 2 などの ROM データの値を使用可能 (シーケンスコマンド [$FE](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#FE))
- ピッチ計算 (キーオン・ピッチスライド)
  - 二つの微調整値を使用してピッチを計算  
FINAL FANTASY V や Romancing Sa·Ga 2 などの ROM データの値を使用可能 (シーケンスコマンド [$FE](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#FE))
- オリジナルと異なる仕様
  - エコーディレイ変化  
  サウンドドライバファンクション等で変化した場合、待機時間がオリジナルよりも若干長い場合がある (通常は起動・リセット・初回音楽データ読み込み時に変化)。  
  - シーケンスコマンド [$D2](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#D2)  
  効果音から設定可能 (-4 バイト, -4 サイクル)
  - シーケンスコマンド [$D4](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#D4)  
  効果音から設定可能 (-4 バイト, -4 サイクル)
  - シーケンスコマンド [$DC](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#DC)  
    - xx = $11 :  無効 → 音量倍率 200
    - xx = $12 :  無効 → 音量倍率 180
    - xx = $13 :  無効 → 音量倍率 160
    - xx = $19 :  無効 → 音量倍率 150
    - xx = $1A :  無効 → 音量倍率 140
    - xx = $1B :  無効 → 音量倍率 100
    - xx = $1C :  無効 → 音量倍率 80
    - xx = $1D :  無効 → 音量倍率 75
    - xx = $1F :  無効 → 音量倍率 70
  xx に $11 ～ $13, $19 ～ $1D のいずれかを設定した場合、キーオン時に音量の倍率が 0 に変化しない (-2 バイト, -5 サイクル)
  - シーケンスコマンド [$DF](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#DF)  
  xx に不正な値を設定可能 (-2 バイト, -2 サイクル)
  - シーケンスコマンド [$F4](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F4)  
  効果音トラックの キーオフ予約を実行するか判定する処理 で何もしないコマンドとして処理される (-16 バイト)

## サウンドドライババージョン
APU RAM $FE70 ～ $FE7F の 16 バイトをご確認ください。
  <details>
  <summary>以前のバージョンの APU RAM アドレス</summary>

  |バージョン|APU RAM アドレス|
  |:----:|:----:|
  |20211122-0|$B5F0 ～ $B5FF|
  |20211124-0|$B5F0 ～ $B5FF|
  |20211224-0|$B5F0 ～ $B5FF|
  |20220124-0|$B5F0 ～ $B5FF|
  </details>

## 使用方法
- IPS ファイルを適用します。
  - ROM イメージファイルに IPS ファイルを適用
	  - **日本語**かつ**イージータイプではない** FINAL FANTASY IV (**初期版**) の ROM イメージファイル (1,048,576 バイト) に **Final Fantasy IV (F4G-0 20220222-0).ips** を適用します。
	  - [Snes9x](https://github.com/snes9xgit/snes9x) などで SPC ファイルを保存します。
  - SPC ファイルに IPS ファイルを適用
	  - [FINAL FANTASY IV : IPS パッチ適用元 BIN ファイル生成ツール](https://gnilda.rosx.net/SPC/F4G/spc2bin.html)で BIN ファイルをダウンロードし、**F4G-0 20220222-0.ips** を適用します。
- [FINAL FANTASY IV 改造サウンドドライバ : 音楽シーケンスデータ生成ツール](https://gnilda.rosx.net/SPC/F4G/spcseq.html)で音楽データファイルを作成します。
- 音楽データと波形データを[スクリプトファイル](https://github.com/GodGnilda/Script700/tree/main/F4G)で転送し、スナップショットを作成します。

## 演奏可能な曲 (ROM データ)
最新版 (F4G-0 20220222-0) の[スクリプトファイル](https://github.com/GodGnilda/Script700/tree/main/F4G)で演奏可能なデータです。  
[FINAL FANTASY IV 改造サウンドドライバ で ROM のデータを使用して音楽を演奏するスクリプト](https://github.com/GodGnilda/Script700/blob/main/F4G/F4G_F4G.700)でスナップショットを保存しお楽しみください。  
データに不備等がございましたらお手数ですが [Issue](https://github.com/GodGnilda/F4G-0/issues) にてご指摘のほどよろしくお願いいたします。

  |ID|曲名|遅延 (初期)|遅延 (修正)|
  |--:|:--|:-:|:-:|
  |$01|オープニング|1|0|
  |$04|チョコボ|0|0|
  |$08|勝利のファンファーレ|0|0|
  |$09|街のテーマ|0|0|
  |$0A|少女リディア|0|0|
  |$0D|ファイナルファンタジー IV メインテーマ|4|0|
  |$0F|哀しみのテーマ 2 ?|0|0|
  |$10|宿屋|0|0|
  |$12|ギルバートのリュート|0|0|
  |$13|愛のテーマ|0|0|
  |$14|バロン王国|1|0|
  |$15|プレリュード|0|0|
  |$1A|バトル 2|2|0|
  |$1D|ボムの指輪|0|0|
  |$1F|驚嘆|0|0|
  |$23|脱出|3|0|
  |$25|ダンジョン|2|0|
  |$26|踊り子|0|0|
  |$27|バトル 1|1|0|
  |$28|ダムシアン城|2|0|
  |$29|ファンファーレ 1|0|0|
  |$2A|哀しみのテーマ ?|0|0|
  |$2B|チョコボの森|0|0|
  |$2C|赤い翼 (ニューゲーム)|4|0|
  |$2D|疑惑のテーマ|0|0|
  |$31|もう一つの月|**0**, **1**, 2|**0** ～ 1|
  |$33|ミシディア国|1|0|
  |$3E|飛空挺 (ダムシアン城)|?|?|
  |$42|地震 (ミストの村)|0|0|
  |$44|地下に通じる滝|?|?|
  |$45|エコー設定のみ (地下水脈 : 初めてのセーブポイント)|?|?|

初期 : 波形番号とジャンプ系のアドレスのみ変更したデータを使用して SNESAPU.DLL で演奏  
修正 : 遅延を低減したデータを使用して SNESAPU.DLL で演奏

## 既知の不具合
- ゲームプレイ中に音楽が正しく演奏されない  
演奏不可能な曲を APU メモリに転送しているため発生します。  
アントリオンの洞窟直前までは安全にプレイ可能です。
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
- ----/--/-- [F4G-0 20220222-2]
  - 初期化処理を 10 サイクル高速化。
  - メインループの処理を 3 サイクル高速化。
  - 音楽トラック DE コマンド待機終了時の ADSR モード → GAIN モード 処理を 4 サイクル高速化。
  - キーオン予約処理を 1 サイクル高速化。
  - DC 音量倍率変化終了時の ADSR モード → GAIN モード 処理を 3 サイクル高速化。
  - エコーディレイが変化した場合の処理を 8 サイクル高速化。
- ----/--/-- [F4G-0 20220222-1] [効果音データ]
  - メインループの処理を 1 サイクル高速化。
  - 効果音データを更新。
    - 修正
      - $1B
      - $48
    - 無限ループ処理を F4 で実行
      - $2F
      - $32
      - $3C
      - $46
      - $47
      - $50
      - $51
      - $54
      - $5E
      - $60
      - $7D
      - $7F
- 2022/02/22 [F4G-0 20220222-0] [音楽データ] [効果音データ]
  - **仕様を変更**。
    - シーケンスコマンド
      - [$DB](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#DB)
        - xx : 2 ～ 33 → 0 ～ 31
      - [$DC](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#DC)
        - xx = $11 :  無効 → 音量倍率 200
        - xx = $12 :  無効 → 音量倍率 180
        - xx = $13 :  無効 → 音量倍率 160
        - xx = $19 :  無効 → 音量倍率 150
        - xx = $1A :  無効 → 音量倍率 140
        - xx = $1B :  無効 → 音量倍率 100
        - xx = $1C :  無効 → 音量倍率 80
        - xx = $1D :  無効 → 音量倍率 75
        - xx = $1F :  無効 → 音量倍率 70
      - [$FC](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#FC)
        - xx : 0, 2, 4 → 0 ～ 2
    - サウンドドライバファンクション $02
      - データサイズを小さくするためにファンクション実行時に一部のシーケンスコマンドを実行。
      - 効果音番号が $00 の場合のみ DSP チャネル 7 と 8 を強制的にキーオフする。
      - **効果音が DSP チャネル 7 を使用していない状態**でサウンドドライバファンクション $02 を使用し、**DSP チャネル 7 を使用しない効果音を演奏する**場合、DSP チャネル 7 をキーオフしない。
    - サウンドドライバファンクション $10 ～ $1F
      - データサイズを小さくするためにファンクション実行時に一部のシーケンスコマンドを実行。
    - 効果音データの仕様変更。
  - 音楽トラックの処理を 3 サイクル以上高速化。
  - シーケンスコマンドの処理を高速化。
    - キーオン : 9 サイクル以上
    - 休符・タイ : 7 サイクル
    - [$D2](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D2) (変化) : ? ～ 約 ? サイクル
    - [$D6](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D6) : 10 サイクル
    - [$D7](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D7) : 14 サイクル
    - [$D8](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#D8) : 10 サイクル
    - [$D9](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D9) : 10 サイクル
    - [$DF](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#DF) : 11 サイクル
    - [$F1](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F1) (音楽) : 4 サイクル
    - [$F1](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F1) (効果音) : 11 サイクル
    - [$F2](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F2) (変化) : 25 ～ 約 300 サイクル
    - [$F3](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F3) (変化) : 25 ～ 約 300 サイクル
    - [$F6](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F6) : 10 サイクル
    - [$FB](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#FB) : 10 サイクル
    - 他 (引数無し) : 10 サイクル
    - 他 (引数有り) : 8 サイクル
  - シーケンスコマンド [$D8](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#D8) のピッチ変化計算処理を高速化。
    - 初回 (0) : 8 サイクル
    - 初回 (1, 2) : 4 サイクル
    - 初回を除く奇数回 (0, 1, 2) : 9 サイクル
    - 偶数回 (0) : 11 サイクル
    - 偶数回 (1) : 13 サイクル
    - 偶数回 (2) : 22 サイクル
  - シーケンスコマンド [$DE](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#DE) の待機時間計算処理で、シーケンスコマンド [$D3](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D3) を使用したタイを正しく処理できない不具合を修正 (12 サイクル低速化)。
  - 音楽データを修正。
	- データサイズ優先
	  - $01 : オープニング [遅延なし → 遅延なし]
	  - $08 : 勝利のファンファーレ [遅延なし → 遅延なし]
	  - $09 : 街のテーマ [遅延なし → 遅延なし]
	  - $0D : ファイナルファンタジー IV メインテーマ [遅延なし → 遅延なし]
	  - $15 : プレリュード [遅延なし → 遅延なし]
	  - $26 : 踊り子 [遅延なし → 遅延なし]
	  - $33 : ミシディア国 [遅延なし → 遅延なし]
	- 処理速度優先
	  - $14 : バロン王国 [ループ 1 回あたり 1 回遅延 → 遅延なし]
	  - $27 : バトル 1 [ループ 1 回あたり 4 回遅延 → 遅延なし]
	  - $2C : 赤い翼 (ニューゲーム) [ループ 1 回あたり 1 回遅延 → 遅延なし]
	  - $31 : もう一つの月 [ループ 2 回あたり 1 回程度遅延 → 約 1040 秒ごとに 1 回]
	- 演奏可能
	  - $0A : 少女リディア [遅延なし]
	  - $0F : 哀しみのテーマ 2 ? [遅延なし]
	  - $10 : 宿屋 [遅延なし]
	  - $12 : ギルバートのリュート [遅延なし]
	  - $1A : バトル 2 [遅延なし]
	  - $1D : ボムの指輪 [遅延なし]
	  - $1F : 驚嘆 [遅延なし]
	  - $23 : 脱出 [遅延なし]
	  - $25 : ダンジョン [遅延なし]
	  - $28 : ダムシアン城 [遅延なし]
	  - $29 : ファンファーレ 1 [遅延なし]
	  - $2A : 哀しみのテーマ ? [遅延なし]
	  - $3E : 飛空挺 (ダムシアン城)
	  - $42 : 地震 (ミストの村) [遅延なし]
	  - $44 : 地下に通じる滝
	  - $45 : エコー設定のみ (地下水脈 : 初めてのセーブポイント)
- 2022/01/24 [F4G-0 20220124-0]
  - 効果音を正しく演奏できない不具合を修正。
- 2021/12/24 [F4G-0 20211224-0] [効果音データ]
  - メインループの処理が 4 サイクル低速化。
  - キーオン予約時の処理を高速化。
    - 音楽 : 約 24 サイクル
    - 音楽 [$D6](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D6) 処理 : 約 30 サイクル
    - 音楽 [$D8](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#D8) 処理 : 2 サイクル
    - 効果音 : 約 12 サイクル
    - 効果音 [$D6](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D6) 処理 : 約 16 サイクル以上
    - 効果音 [$D8](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#D8) 処理 : 2 サイクル
  - キーオフ予約時の処理を高速化。
    - 音楽・効果音 : 5 サイクル
  - シーケンスコマンド [$DE](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#DE) の待機時間計算処理を高速化。
    - 音楽 [$F1](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F1) : 5 サイクル
  - タイ・休符の処理を高速化。
    - 音楽 3 サイクル
  - トラックのコマンドを処理しない場合の処理を高速化。
    - 音楽・効果音 : 約 5 サイクル
    - 音楽・効果音 [$D6](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#D6) 処理 : 約 8 サイクル
  - シーケンスコマンドの処理を高速化。
    - [$E1](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#E1) : 2 サイクル
    - [$F1](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F1) : 3 サイクル
  - 音楽・効果音処理切り替え時のペナルティ増加。
  - 効果音を修正。
    - $3B
    - $48
- 2021/11/24 [F4G-0 20211124-0]
  - サウンドドライバファンクション $03 を使用すると音楽データを正しく転送できない不具合を修正。
  - シーケンスコマンドの処理を高速化。
    - [$DF](https://gnilda.rosx.net/SPC/F4/sequence_commands.html#DF) : 2 サイクル (処理を一部省略)
    - [$F1](https://gnilda.rosx.net/SPC/F4G/sequence_commands_0.html#F1) : 2 サイクル
- 2021/11/22 [F4G-0 20211122-0]
  - 公開。
