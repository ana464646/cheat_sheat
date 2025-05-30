# BloodHound Active Directory Analysis

## BloodHound セットアップ

### コレクターのインストール
```powershell
# SharpHound のダウンロードと実行
wget https://raw.githubusercontent.com/BloodHoundAD/BloodHound/master/Collectors/SharpHound.ps1
Import-Module .\SharpHound.ps1

# Python版コレクターのインストール
pip install bloodhound

# Neo4j のインストール（攻撃者マシン）
sudo apt install neo4j
sudo neo4j start
```

## データ収集

### SharpHound を使用したデータ収集
```powershell
# 全データの収集
Invoke-BloodHound -CollectionMethod All

# 特定のデータのみ収集
Invoke-BloodHound -CollectionMethod Session,LoggedOn
Invoke-BloodHound -CollectionMethod DCOnly
Invoke-BloodHound -CollectionMethod GPOLocalGroup

# ステルス性を高めた収集
Invoke-BloodHound -CollectionMethod All -Stealth

# 特定ドメインの収集
Invoke-BloodHound -CollectionMethod All -Domain target.local
```

### Python版コレクターの使用
```bash
# 基本的な収集
bloodhound-python -u username -p password -d domain.local -ns <dc-ip> -c All

# 特定のユーザーでの収集
bloodhound-python -u username -p password -d domain.local -c Session,LoggedOn

# Kerberos認証を使用
bloodhound-python -u username -k -d domain.local -c All
```

## 攻撃パスの分析

### 一般的なクエリ
```cypher
# Domain Adminsへの最短パス
MATCH (n:User),(m:Group {name:"DOMAIN ADMINS@DOMAIN.LOCAL"}),
p=shortestPath((n)-[*1..]->(m)) RETURN p

# キッティング可能なコンピュータ
MATCH (c:Computer)
WHERE c.haslaps=false
RETURN c.name

# 危険な委任設定
MATCH (c:Computer {unconstraineddelegation:true})
RETURN c.name
```

### 特権アカウントの列挙
```cypher
# ネストされた管理者グループ
MATCH p=(n:User)-[r:MemberOf*1..]->(m:Group)
WHERE m.name =~ ".*ADMIN.*"
RETURN p

# DCSync権限を持つアカウント
MATCH (n:User)
WHERE n.dcsync=true
RETURN n.name
```

## 攻撃シナリオ

### Kerberoastable アカウントの特定
```cypher
# SPNを持つアカウントの検索
MATCH (u:User)
WHERE u.hasspn=true
RETURN u.name, u.serviceprincipalnames

# 高権限Kerberoastableアカウント
MATCH (u:User)-[r:MemberOf*1..]->(g:Group)
WHERE u.hasspn=true AND g.name =~ ".*ADMIN.*"
RETURN u.name, g.name
```

### 委任の悪用
```cypher
# 制約のない委任設定
MATCH (c:Computer {unconstraineddelegation:true})
RETURN c.name, c.operatingsystem

# 制約付き委任の列挙
MATCH (c:Computer)
WHERE c.allowedtodelegate IS NOT NULL
RETURN c.name, c.allowedtodelegate
```

## OPSEC 考慮事項

### ステルス収集のベストプラクティス
```powershell
# 低帯域幅での収集
Invoke-BloodHound -CollectionMethod All -Stealth -LdapFilter "(objectClass=user)"

# セッション収集の制限
Invoke-BloodHound -CollectionMethod Session -SearchForest
```

### ログの削除
```powershell
# PowerShell ログの削除
Remove-Item (Get-PSReadlineOption).HistorySavePath
Clear-EventLog "Windows PowerShell"

# SharpHoundログの削除
Remove-Item C:\Users\*\AppData\Local\BloodHound -Recurse -Force
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- Active Directory環境に大きな負荷をかける可能性があります
- データ収集は監査ログを生成する可能性があります
- 実環境での使用は違法となる可能性があります 