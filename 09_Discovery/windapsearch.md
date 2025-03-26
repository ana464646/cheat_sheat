# windapsearch
windapsearchの基本的な使い方とオプションについて記載

https://github.com/ropnop/windapsearch

# Overview
windapsearchは、Windowsドメインからユーザー、グループ、およびコンピュータを列挙するためのPythonスクリプトです。LDAPクエリを通じてこれを実行します。デフォルトでは、Windowsドメインコントローラーはポート389/tcpを介して基本的なLDAP操作をサポートしています。任意の有効なドメインアカウント（特権に関係なく）を使用して、ドメインコントローラーに対してLDAPクエリを実行し、AD関連情報を取得することが可能です

windapsearchの主な機能には以下が含まれます

ユーザー、グループ、コンピュータの列挙

グループメンバーの取得

制約のないコンピュータの検索（通常はドメインコントローラー）

制約のないユーザーの検索

特権ユーザーの取得

ドメイン管理者のメンバーの取得

保護されたACL（管理者）の列挙

サービスプリンシパル名（SPN）を持つすべてのユーザーオブジェクトの列挙（Kerberoasting用）

グループポリシーオブジェクトの列挙

すべてのLDAPエントリのファジー検索

完全な属性データの取得

# Usage

ダウンロード

```
git clone 
https://github.com/ropnop/windapsearch.git
pip install python-ldap #or apt-get install python-ldap
./
windapsearch.py
```

ユーザ名列挙
書式
./
windapsearch.py
 -d <ドメイン名> --dc-ip [IP] -U

```
./
windapsearch.py
 -d xxx.local --dc-ip 192.168.1.50 -U
```

ユーザ名列挙(認証情報が必要とエラーを吐かれた場合)
```
./
windapsearch.py
 -d xxx.local -u <ドメイン名\\ユーザー名> -p <パスワード> --dc-ip 192.168.1.50 -U
```
