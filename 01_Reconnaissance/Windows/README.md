# Windows Reconnaissance Techniques

## ネットワークスキャン

### ポートスキャン
```powershell
# Nmap を使用した基本スキャン
nmap -sC -sV -p- -T4 <target-ip>

# PowerShell を使用したポートスキャン
1..1024 | % {echo ((New-Object Net.Sockets.TcpClient).Connect("<target-ip>",$_)) "Port $_ is open"} 2>$null
```

### ホスト探索
```powershell
# NetBIOS 探索
nbtstat -A <target-ip>
net view \\<target-ip>

# ARP スキャン
arp -a
```

## Active Directory 列挙

### ドメイン情報収集
```powershell
# ドメイン情報の取得
nltest /domain_trusts
nltest /dclist:<domain>
net group "Domain Admins" /domain

# PowerView を使用した列挙
Import-Module .\PowerView.ps1
Get-NetDomain
Get-NetUser
Get-NetGroup
Get-NetComputer
```

### LDAP クエリ
```powershell
# LDAP 検索
$domain = "LDAP://DC=domain,DC=com"
$searcher = New-Object DirectoryServices.DirectorySearcher([ADSI]$domain)
$searcher.filter = "(&(objectClass=user)(samAccountName=*))"
$searcher.FindAll()
```

## ファイル共有列挙

### SMB 共有探索
```powershell
# 共有の列挙
net view \\<target-ip>
dir \\<target-ip>\c$ /a

# PowerShell を使用した共有列挙
Get-WmiObject -Class Win32_Share
```

### アクセス権限チェック
```powershell
# AccessChk を使用した権限確認
accesschk.exe -uwdqs Users c:\
accesschk.exe -uwdqs "Authenticated Users" c:\
```

## サービス列挙

### 実行中のサービス
```powershell
# サービス一覧の取得
tasklist /svc
wmic service list brief
Get-Service | Where-Object {$_.Status -eq "Running"}

# 特定のポートをリッスンしているプロセス
netstat -ano | findstr "LISTENING"
```

### インストール済みソフトウェア
```powershell
# インストール済みアプリケーションの列挙
wmic product get name,version
Get-WmiObject -Class Win32_Product | Select-Object Name, Version
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- 過度なスキャンはターゲットシステムに負荷をかける可能性があります
- 実環境での使用は違法となる可能性があります 