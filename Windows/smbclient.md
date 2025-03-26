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
