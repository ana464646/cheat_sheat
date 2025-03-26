# enum4linux
enum4linuxの基本的な使い方を記載

# Overview
enum4linuxは、WindowsおよびSambaシステムから情報を列挙するためのツールです。このツールは、かつて
www.bindview.com
から提供されていたenum.exeと同様の機能を提供することを目的としています。enum4linuxは、主に以下の機能を持っています

RIDサイクリング（Windows 2000でRestrictAnonymousが1に設定されている場合）

ユーザーリストの取得（Windows 2000でRestrictAnonymousが0に設定されている場合）

グループメンバーシップ情報のリスト

共有の列挙

ホストがワークグループまたはドメインに属しているかの検出

リモートオペレーティングシステムの識別

パスワードポリシーの取得（polenumを使用）

このツールは、Perlで書かれており、smbclient、rpclient、net、およびnmblookupなどのSambaツールのラッパーとして機能します。Sambaパッケージが依存関係となります

https://www.kali.org/tools/enum4linux/

# Usage

共有情報を取得 -S

```
enum4linux -S 10.10.10.10
```

ユーザーの認証情報を取得している場合

```
enum4linux -u <ユーザー名> -p <パスワード> -a 10.10.10.10
```



