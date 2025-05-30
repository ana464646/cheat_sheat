# Reconnaissance Tools Command Reference

## Nmap

### 基本スキャン
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

### スクリプトスキャン
```bash
# 脆弱性スキャン
nmap --script vuln <target>

# SMBスキャン
nmap --script smb-* <target>

# SSLスキャン
nmap --script ssl-* <target>
```

## Masscan

### 高速スキャン
```bash
# 全ポートスキャン
masscan -p1-65535 <target> --rate=1000

# 特定ポートのスキャン
masscan -p80,443,8080 <target> --rate=1000

# 結果をファイルに出力
masscan -p1-65535 <target> --rate=1000 -oJ output.json
```

## DNSrecon

### DNS列挙
```bash
# 基本的なDNS列挙
dnsrecon -d <domain>

# ブルートフォース
dnsrecon -d <domain> -t brt -D /path/to/wordlist.txt

# ゾーン転送
dnsrecon -d <domain> -t axfr
```

## theHarvester

### OSINT収集
```bash
# 基本検索
theHarvester -d <domain> -b all

# 特定のソースから検索
theHarvester -d <domain> -b google,linkedin

# メールアドレス収集
theHarvester -d <domain> -b all -f output.html
```

## Gobuster

### ディレクトリ列挙
```bash
# 基本的なディレクトリスキャン
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt

# 拡張子指定
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -x php,html,txt

# DNSサブドメイン列挙
gobuster dns -d <domain> -w /usr/share/wordlists/dns.txt
```

## WPScan

### WordPress列挙
```bash
# 基本スキャン
wpscan --url <url>

# 脆弱性スキャン
wpscan --url <url> --enumerate vp

# ユーザー列挙
wpscan --url <url> --enumerate u

# プラグイン列挙
wpscan --url <url> --enumerate p
```

## Nikto

### Webサーバースキャン
```bash
# 基本スキャン
nikto -h <target>

# SSL使用
nikto -h <target> -ssl

# プロキシ使用
nikto -h <target> -useproxy http://proxy:port
```

## SMBMap

### SMB列挙
```bash
# 共有列挙
smbmap -H <target>

# ユーザー指定
smbmap -H <target> -u "username" -p "password"

# 再帰的リスト
smbmap -H <target> -R
```

## 注意事項
- これらのツールは許可された環境でのみ使用してください
- 過度なスキャンはターゲットシステムに負荷をかける可能性があります
- 実環境での使用は違法となる可能性があります 