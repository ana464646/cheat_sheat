# BloodHound Command Reference

**対応OS**: Windows, Linux (データコレクタはWindows、GUIはクロスプラットフォーム)

## データ収集（SharpHound）
```powershell
# 基本的なデータ収集
SharpHound.exe --CollectionMethods All

# 特定の収集メソッドを指定
SharpHound.exe --CollectionMethods Session,LoggedOn,Trusts

# ステルスモードでの収集
SharpHound.exe --CollectionMethods All --Stealth

# 特定ドメインの収集
SharpHound.exe --CollectionMethods All --Domain domain.local
```

## データ収集（Python版）
```bash
# 基本的なデータ収集
bloodhound-python -d domain.local -u username -p password -c All

# 特定の収集メソッドを指定
bloodhound-python -d domain.local -u username -p password -c Session,LoggedOn

# LDAP接続の指定
bloodhound-python -d domain.local -u username -p password -c All --dns-tcp
```

## BloodHound GUI
```bash
# Neo4jデータベースの起動
neo4j start

# BloodHoundの起動
bloodhound

# データのインポート
# GUIからドラッグ&ドロップ、または「Upload Data」ボタンを使用
```

## クエリ例
```cypher
# 最短パスの検索
MATCH (n:User),(m:Group),p=shortestPath((n)-[*1..]->(m)) WHERE m.name =~ ".*DOMAIN ADMINS.*" RETURN p

# 危険な権限を持つユーザーの検索
MATCH (n:User) WHERE n.highvalue=true RETURN n

# パスワードが変更されていないアカウントの検索
MATCH (n:User) WHERE n.pwdlastset < (datetime().epochseconds - 90*86400) RETURN n
```

## 高度な収集オプション
```powershell
# ACLの詳細な収集
SharpHound.exe --CollectionMethods ACL --LdapFilter "(objectClass=user)"

# GPOの詳細な収集
SharpHound.exe --CollectionMethods GPOLocalGroup

# コンテナ情報の収集
SharpHound.exe --CollectionMethods Container
```

## 出力オプション
```powershell
# 出力ディレクトリの指定
SharpHound.exe --OutputDirectory C:\Temp

# 圧縮の無効化
SharpHound.exe --NoZip

# キャッシュの保存
SharpHound.exe --CacheFileName cache.bin
```

## 注意事項
- データ収集はネットワークトラフィックを生成します
- 収集したデータには機密情報が含まれる可能性があります
- 実環境での使用は必ず許可を得てから行ってください
- 収集したデータの取り扱いには十分注意してください 