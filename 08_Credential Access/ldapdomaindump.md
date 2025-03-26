# ldapdomaindump
ldapdomaindumpの基本的な使い方を記載

ldapdomaindumpは、Active Directoryの情報をLDAP（Lightweight Directory Access Protocol）を介して取得するためのツールです。このツールは、認証されたユーザー（またはマシン）がLDAPを使用して内部ネットワークの情報を収集する際に役立ちます。ldapdomaindumpは、LDAPから取得したデータを人間が読みやすいHTML形式や、機械が読み取れるJSON、CSV、TSV、greppableファイル形式で出力します1。

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

ポート指定をする場合
Portスキャンに時間がかかることがある為、ポート指定をする。

```
nmap 192.168.1.50-55 -p 4000-5000
```

ファイアウォールでICMPをブロックする為、それを回避するために-Pnオプションを使用。
時間がかかる為注意が必要。

```
nmap -Pn 192.168.1.50-55 -p 4000-5000
```

ターゲットのOSを確認する場合 -o
```
nmap -Pn 192.168.1.50-55 -p 4000-5000 -O
```

動作しているサービスのバージョンを確認 -sV
```
nmap -Pn 192.168.1.50-55 -p 4000-5000 -sV
```

# 補足
nmapのスクリプト(NSEスクリプト)は
下記に書かれており、grepで使えそうなスクリプトを見てみるのも良い
/usr/share/nmap/scripts/

例えばSMBポートが空いてる場合どういったNSEスクリプトが使えるか確認したい場合
```
ls /usr/share/nmap/scripts/ | grep smb
```

SMBに対して、NSEスクリプトを使って脆弱性を見つけたい場合
```
nmap --script smb-vuln* -p 445 192.168.1.53 -Pn
```

ファイル共有の一覧を列挙 smb-enum-shares.nse

リモートの Windows システム上のユーザーを列挙 smb-enum-users.nse
```
nmap -p 445 --script smb-enum-shares.nse,smb-enum-users.nse 192.168.1.53 -Pn
```
