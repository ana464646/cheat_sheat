# Linux Reconnaissance Techniques

## ネットワークスキャン

### ポートスキャン
```bash
# Nmap を使用した詳細スキャン
nmap -sC -sV -p- -T4 <target-ip>
nmap -sU -p- <target-ip>  # UDPスキャン

# Masscan を使用した高速スキャン
masscan -p1-65535 <target-ip> --rate=1000
```

### ネットワーク探索
```bash
# ネットワーク内のホスト探索
netdiscover -r <network/cidr>
arp-scan --localnet

# traceroute を使用した経路探索
traceroute -I <target-ip>
```

## Webアプリケーション調査

### Web サーバー情報収集
```bash
# Webサイトの基本情報収集
whatweb <target-url>
curl -I <target-url>

# ディレクトリ列挙
gobuster dir -u <target-url> -w /usr/share/wordlists/dirb/common.txt
dirbuster -u <target-url> -l /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

### CMS 探索
```bash
# WordPress スキャン
wpscan --url <target-url> --enumerate p,t,u

# Drupal スキャン
droopescan scan drupal -u <target-url>
```

## DNS 情報収集

### DNS レコード
```bash
# DNS 情報の取得
dig <domain> ANY
dig axfr @<dns-server> <domain>

# サブドメイン列挙
sublist3r -d <domain>
amass enum -d <domain>
```

### リバース DNS
```bash
# リバース DNS ルックアップ
for ip in $(seq 1 254); do host <network>.$ip; done
dnsrecon -r <network>/24
```

## SSL/TLS 分析

### 証明書情報
```bash
# SSL/TLS 証明書の分析
sslscan <target>
testssl.sh <target>

# Heartbleed 脆弱性チェック
nmap -p 443 --script ssl-heartbleed <target>
```

## OSINT 収集

### Whois 情報
```bash
# Whois 情報の取得
whois <domain>
whois <ip-address>

# メールサーバー情報
dig <domain> MX
```

### メタデータ収集
```bash
# ドキュメントのメタデータ収集
exiftool <file>
metagoofil -d <domain> -t pdf,doc,xls -n 10
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- 過度なスキャンはターゲットシステムに負荷をかける可能性があります
- 実環境での使用は違法となる可能性があります 