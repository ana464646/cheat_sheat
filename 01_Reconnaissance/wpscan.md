# WPScan Command Reference

## 基本スキャン
```bash
# 基本的なスキャン
wpscan --url <url>

# 詳細な出力
wpscan --url <url> --verbose

# 出力ファイルの指定
wpscan --url <url> --output output.txt
```

## 列挙オプション
```bash
# すべての脆弱性をスキャン
wpscan --url <url> --enumerate vp

# ユーザー列挙
wpscan --url <url> --enumerate u

# プラグイン列挙
wpscan --url <url> --enumerate p

# テーマ列挙
wpscan --url <url> --enumerate t

# タイムリミットの設定
wpscan --url <url> --enumerate p,t,u --max-scan-duration 20m
```

## 認証オプション
```bash
# APIトークンの使用
wpscan --url <url> --api-token <token>

# パスワードブルートフォース
wpscan --url <url> --passwords /path/to/wordlist.txt --usernames admin

# Basic認証の使用
wpscan --url <url> --http-auth <username>:<password>
```

## 高度なオプション
```bash
# プロキシの使用
wpscan --url <url> --proxy <proxy_url>

# ユーザーエージェントの指定
wpscan --url <url> --user-agent "Mozilla/5.0"

# 特定のプラグインのみスキャン
wpscan --url <url> --plugins-detection aggressive

# キャッシュの無効化
wpscan --url <url> --disable-tls-checks
```

## レポート出力
```bash
# JSON形式で出力
wpscan --url <url> --format json --output scan.json

# HTML形式で出力
wpscan --url <url> --format html --output scan.html

# CLIとファイルの両方に出力
wpscan --url <url> --output scan.txt --format cli-no-color
```

## 注意事項
- APIトークンを使用することで、より詳細な脆弱性情報が取得できます
- 過度なスキャンはサーバーに負荷をかける可能性があります
- パスワードブルートフォースは対象システムのポリシーに違反する可能性があります
- 実環境での使用は必ず許可を得てから行ってください 