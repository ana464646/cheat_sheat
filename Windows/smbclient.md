# smbclient
smbclientの基本的な使い方とオプションについて記載

# Usage

smbclientの書式とオプション

smbclient [オプション] //ホスト名/共有名

smbclient //ホスト名/共有名 [オプション]

オプション

・-L　ホスト名|--list=ホスト名　指定したホストで利用可能な共有リソースを一覧表示

・-N　認証を行わない

・-U ユーザ名|--user=ユーザ名　接続するユーザを指定

```
smbclient -L 192.168.1.53
```
