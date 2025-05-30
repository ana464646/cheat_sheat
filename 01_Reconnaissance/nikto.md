# Nikto Command Reference

**対応OS**: Linux (Windows上ではWSL2/Perl環境での実行が可能)

## 基本スキャン
```bash
# 基本的なスキャン
nikto -h <target>

# SSL/TLSを使用
nikto -h <target> -ssl

# 特定のポートをスキャン
nikto -h <target> -port 80,443
```

## 出力オプション
```bash
# テキスト形式で出力
nikto -h <target> -o report.txt -Format txt

# HTML形式で出力
nikto -h <target> -o report.html -Format html

# CSV形式で出力
nikto -h <target> -o report.csv -Format csv

# XML形式で出力
nikto -h <target> -o report.xml -Format xml
```

## 高度なオプション
```bash
# プロキシの使用
nikto -h <target> -useproxy http://proxy:port

# Basic認証
nikto -h <target> -id <username>:<password>

# カスタムヘッダーの追加
nikto -h <target> -vhost "example.com"

# タイムアウトの設定
nikto -h <target> -timeout 30
```

## チューニングオプション
```bash
# 特定のテストを実行
nikto -h <target> -Tuning 1,2,3

# すべてのテストを実行
nikto -h <target> -Tuning x

# 特定のプラグインを使用
nikto -h <target> -Plugins "@@default,apache_expect"
```

## スキャン制御
```bash
# 詳細な出力
nikto -h <target> -Display V

# エラーのみ表示
nikto -h <target> -Display E

# リダイレクトを無視
nikto -h <target> -nofollow

# 更新チェックをスキップ
nikto -h <target> -noupdate
```

## 高度なスキャンオプション
```bash
# 複数ホストのスキャン
nikto -h <target1>,<target2>

# ファイルからホストを読み込み
nikto -h host.txt

# ミューテーションスキャン
nikto -h <target> -mutate 1
```

## 注意事項
- 過度なスキャンはサーバーに負荷をかける可能性があります
- 誤検知の可能性があるため、結果は手動で確認することを推奨します
- 一部のテストは対象システムに影響を与える可能性があります
- 実環境での使用は必ず許可を得てから行ってください 