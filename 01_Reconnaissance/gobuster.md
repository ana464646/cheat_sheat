# Gobuster Command Reference

## ディレクトリ列挙（dir モード）
```bash
# 基本的なディレクトリスキャン
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt

# 拡張子指定
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -x php,html,txt

# ステータスコードの指定
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -s 200,204,301,302,307,401,403

# 出力ファイルの指定
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -o output.txt
```

## DNS列挙（dns モード）
```bash
# サブドメイン列挙
gobuster dns -d <domain> -w /usr/share/wordlists/dns.txt

# 特定のDNSサーバーを指定
gobuster dns -d <domain> -w /usr/share/wordlists/dns.txt -r <dns_server>

# ワイルドカードDNSの処理
gobuster dns -d <domain> -w /usr/share/wordlists/dns.txt -i
```

## VHOSTの列挙（vhost モード）
```bash
# 基本的なVHOST列挙
gobuster vhost -u <url> -w /usr/share/wordlists/vhost.txt

# ポート指定
gobuster vhost -u <url> -w /usr/share/wordlists/vhost.txt -p 80,443
```

## 高度なオプション
```bash
# ユーザーエージェントの指定
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -a "Mozilla/5.0"

# Basic認証の使用
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -U <username> -P <password>

# プロキシの使用
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt --proxy <proxy_url>

# スレッド数の指定
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -t 50
```

## パターンマッチング
```bash
# 特定の文字列を含むレスポンスをフィルタ
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -b "Error,404,Not Found"

# レスポンスの文字数でフィルタ
gobuster dir -u <url> -w /usr/share/wordlists/dirb/common.txt -l 100
```

## 注意事項
- 過度なスキャンはサーバーに負荷をかける可能性があります
- ワードリストは対象に応じて適切なものを選択してください
- スレッド数は対象サーバーの性能を考慮して設定してください
- 実環境での使用は必ず許可を得てから行ってください 