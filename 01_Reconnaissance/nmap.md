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

# Nmap Command Reference

## 基本スキャン
```bash
# 基本的なTCPスキャン
nmap -sT -p- <target>

# ステルススキャン
nmap -sS -p- <target>

# バージョン検出
nmap -sV -p- <target>

# OS検出
nmap -O <target>

# 全スキャン（OS検出、バージョン検出、スクリプトスキャン）
nmap -A <target>
```

## スクリプトスキャン
```bash
# 脆弱性スキャン
nmap --script vuln <target>

# SMBスキャン
nmap --script smb-* <target>

# SSLスキャン
nmap --script ssl-* <target>
```

## 高度なオプション
```bash
# UDP スキャン
nmap -sU -p- <target>

# 特定ポートのスキャン
nmap -p 80,443,8080 <target>

# 出力オプション
nmap -oN output.txt <target>  # 通常出力
nmap -oX output.xml <target>  # XML出力
nmap -oG output.txt <target>  # Grepable出力
```

## ステルス設定
```bash
# タイミング設定（0-5）
nmap -T0 <target>  # 最も遅い
nmap -T5 <target>  # 最も速い

# パケット分割
nmap -f <target>

# デコイの使用
nmap -D RND:10 <target>
```

## 注意事項
- 過度なスキャンはターゲットシステムに負荷をかける可能性があります
- 実環境での使用は必ず許可を得てから行ってください
- ステルススキャンは検知される可能性があります
