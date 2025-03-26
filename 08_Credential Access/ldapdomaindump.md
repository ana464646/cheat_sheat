# ldapdomaindump
ldapdomaindumpの基本的な使い方を記載

ldapdomaindumpは、Active Directoryの情報をLDAP（Lightweight Directory Access Protocol）を介して取得するためのツールです。このツールは、認証されたユーザー（またはマシン）がLDAPを使用して内部ネットワークの情報を収集する際に役立ちます。ldapdomaindumpは、LDAPから取得したデータを人間が読みやすいHTML形式や、機械が読み取れるJSON、CSV、TSV、greppableファイル形式で出力します。

主な機能は以下の通りです：

ドメイン内のすべてのユーザー、グループ、コンピュータ、ポリシーの概要を簡単に把握できる。
ユーザー名とパスワード、またはNTLMハッシュを使用して認証が可能（ldap3 >=1.3.1が必要）。
既存の認証済み接続を使用してLDAPサービスに接続し、リレーリングツール（例：impacketのntlmrelayx）と統合可能。
ldapdomaindumpは、以下のようなファイルを出力します：

domain_groups: ドメイン内のグループのリスト

domain_users: ドメイン内のユーザーのリスト

domain_computers: ドメイン内のコンピュータアカウントのリスト

domain_policy: パスワード要件やロックアウトポリシーなどのドメインポリシー

domain_trusts: ドメイン間の信頼関係とそのプロパティ

また、以下のようなグループ化されたファイルも出力します：

domain_users_by_group: グループごとのドメインユーザー

domain_computers_by_os: オペレーティングシステムごとに分類されたドメインコンピュータ

KaliLinuxに初めからインストールされている。

https://github.com/
dirkjanm/ldapdomaindump

https://www.kali.org/tools/python-ldapdomaindump/



# Usage

HTMLでdataフォルダにドメイン情報をダンプ

```
python3 
ldapdomaindump.py
 --user <ドメイン名\\ユーザー名> -p <パスワード> ldap://192.168.1.
50::389
 --no-json --no-grep -o data
```

