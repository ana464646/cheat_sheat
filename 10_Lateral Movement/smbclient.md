# smbclient
smbclientの基本的な使い方とオプションについて記載

# Usage

smbclientの書式とオプション

smbclient [オプション] //ホスト名/共有名

smbclient //ホスト名/共有名 [オプション]

smbclient -m [最高位のSMBプロトコル] //[接続先のIPアドレス]/[接続する共有フォルダ] -U [ドメイン]\\[ユーザ名]%[パスワード]

オプション

・-L　ホスト名|--list=ホスト名　指定したホストで利用可能な共有リソースを一覧表示

・-N　認証を行わない

・-U ユーザ名|--user=ユーザ名　接続するユーザを指定

```
smbclient -L 192.168.1.53
```

```
# 例
smbclient -m SMB2 //192.168.1.10/share -U domainA\\userA%password
smbclient \\\\192.168.1.53\\AD

コネクションが確立すると以下のようにプロンプトが表示される。
smb: \>
```

# 接続後の主なコマンド

ディレクトリ移動（cd）

ファイル・ディレクトリ一覧表示（dir）

ファイルのダウンロード（get）

指定した条件に一致するファイルをダウンロード（mget）
```
#OS\Linux\ML8ディレクトリ内のファイルを全てダウンロード
prompt
recurse
mget "OS\Linux\ML8"
```

ファイルのアップロード（put）
```
#ml8.8.isoをOS\Linux\ML8\MIRACLELINUX-8.8-rtm-x86_64.isoとしてアップロード
put "ml8.8.iso" "OS\Linux\ML8\MIRACLELINUX-8.8-rtm-x86_64.iso"
```

ディレクトリの作成（mkdir）（md）

ファイルの削除（del）

条件に一致したファイルやディレクトリの削除（deltree）
