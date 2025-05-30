# Initial Access Techniques

## フィッシング攻撃

### 基本的なフィッシングメール送信
```bash
# SEToolkit を使用したフィッシングページの作成
setoolkit
1) Social-Engineering Attacks
2) Website Attack Vectors
3) Credential Harvester Attack Method
2) Site Cloner
```

## パスワードスプレー攻撃

### SMB パスワードスプレー
```bash
crackmapexec smb <target-ip> -u users.txt -p password.txt
```

### Office 365 パスワードスプレー
```bash
./o365spray.py --userlist users.txt --password Spring2024! --count 1 --lockout 1
```

## 公開サービスの脆弱性を利用した侵入

### Web アプリケーションスキャン
```bash
nikto -h <target-url>
```

### SSL/TLS 脆弱性スキャン
```bash
sslscan <target-domain>
```

## 注意事項
- これらのテクニックは、許可された環境でのペネトレーションテストでのみ使用してください
- 実際の攻撃に使用することは違法です
- ターゲットシステムに重大な影響を与える可能性があるため、慎重に実行してください 