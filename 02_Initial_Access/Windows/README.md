# Windows Initial Access Techniques

## フィッシング攻撃

### フィッシングメール作成
```powershell
# SEToolkit を使用したフィッシングページの作成
setoolkit
1) Social-Engineering Attacks
2) Website Attack Vectors
3) Credential Harvester Attack Method
2) Site Cloner
```

## パスワードスプレー攻撃

### SMB パスワードスプレー
```powershell
# CrackMapExec を使用したSMBパスワードスプレー
crackmapexec smb <target-ip> -u users.txt -p password.txt

# Spray365 を使用したOffice365パスワードスプレー
Spray365.ps1 -UserList .\users.txt -Password Spring2024! -Count 1 -Delay 300
```

## 公開サービス攻撃

### RDP ブルートフォース
```powershell
# Hydra を使用したRDPブルートフォース
hydra -L users.txt -P passwords.txt rdp://target-ip

# NCredを使用したRDPブルートフォース
ncrack -v -U users.txt -P passwords.txt rdp://target-ip
```

### SMB 脆弱性スキャン
```powershell
# Nmap SMBスキャン
nmap -p445 --script smb-vuln* <target-ip>

# SMBMap 共有列挙
smbmap -H <target-ip> -u anonymous -p anonymous
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- 実際の攻撃に使用することは違法です
- ターゲットシステムに重大な影響を与える可能性があるため、慎重に実行してください 