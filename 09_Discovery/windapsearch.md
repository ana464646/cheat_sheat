# windapsearch
windapsearchの基本的な使い方とオプションについて記載
LDAPに対して有用
https://github.com/
ropnop/windapsearch

# Usage

ダウンロード

```
git clone https://github.com/ropnop/windapsearch.git
pip install python-ldap #or apt-get install python-ldap
./windapsearch.py
```

ユーザ名列挙
書式
./
windapsearch.py -d <ドメイン名> --dc-ip [IP] -U

```
./windapsearch.py -d xxx.local --dc-ip 192.168.1.50 -U
```

ユーザ名列挙(認証情報が必要とエラーを吐かれた場合)
