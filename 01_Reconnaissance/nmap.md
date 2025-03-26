# nmap
nmapの基本的な使い方とオプションについて記載

# Usage

レンジでの検索
192.168.1.50-55

```
nmap 192.168.1.50-55
```

ポート指定をする場合
Portスキャンに時間がかかることがある為、ポート指定をする。

```
nmap 192.168.1.50-55 -p 4000-5000
```

ファイアウォールでICMPをブロックする為、それを回避するために-Pnオプションを使用。
時間がかかる為注意が必要。

```
nmap -Pn 192.168.1.50-55 -p 4000-5000
```

ターゲットのOSを確認する場合 -o
```
nmap -Pn 192.168.1.50-55 -p 4000-5000 -O
```

動作しているサービスのバージョンを確認 -sV
```
nmap -Pn 192.168.1.50-55 -p 4000-5000 -sV
```

# 補足
nmapのスクリプト(NSEスクリプト)は
下記に書かれており、grepで使えそうなスクリプトを見てみるのも良い
/usr/share/nmap/scripts/

例えばSMBポートが空いてる場合どういったNSEスクリプトが使えるか確認したい場合
```
ls /usr/share/nmap/scripts/ | grep smb
```

SMBに対して、NSEスクリプトを使って脆弱性を見つけたい場合
```
nmap --script smb-vuln* -p 445 192.168.1.53 -Pn
```

ファイル共有の一覧を列挙 smb-enum-shares.nse

リモートの Windows システム上のユーザーを列挙 smb-enum-users.nse
```
nmap -p 445 --script smb-enum-shares.nse,smb-enum-users.nse 192.168.1.53 -Pn
```
