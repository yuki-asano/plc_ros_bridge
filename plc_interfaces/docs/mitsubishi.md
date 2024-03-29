# SLMP format generation
## SLMP伝文フォーマット (3Eフレーム = QnA互換3E方式)
- 通信プロトコルのこと
- データ交信
  - バイナリ ->  下位バイトから上位バイトの順で送信
  - ASCII    ->  上位バイトから下位バイトの順で送信
- 参照
  - SLMPリファレンスマニュアル
  - p18 4 伝文フォーマット

## 要求伝文
- sub_header   # サブヘッダ (5000 固定)
- network_id   # 要求先ネットワーク番号 (自局 -> 00)
- station_id   # 要求先局番 (自局 -> FF)
- unit_io      # 要求先ユニットI/O番号 (CPUユニット&自局 -> 03FF固定)
- multi_drop   # 要求先マルチドロップ局番号 (マルチドロップでない -> 00)
- data_length  # 要求データ長 (監視タイマ+要求データのバイト数)
- timer        # 監視タイマ (応答待ち時間. 無限待ち 0000, 0001-FFFF [250ms])

### [要求データ]
 - cmd          # コマンド 0401:一括読み出し
 - sub_cmd      # サブコマンド
 - device_id    # 先頭デバイス番号
 - device_code  # デバイスコード (00A8 -> データレジスタ(D))
 - device_num   # デバイス点数

 ## 応答伝文
 - sub_header  # サブヘッダ (D000 固定)
 - network_id  # 要求先ネットワーク番号 (要求と同様)
 - station_id  # 要求先局番 (〃)
 - unit_io     # 要求先ユニットI/O番号 (〃)
 - multi_drop  # 要求先マルチドロップ局番 (〃)
 - data_length # 応答データ長 (終了コードから応答データまでのバイト数)
 - end_code    # 終了コード
 - data        # 応答データ
