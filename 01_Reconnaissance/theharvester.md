# theHarvester Command Reference

## 基本的な使用方法
```bash
# 基本検索
theHarvester -d <domain> -b all

# 特定のソースから検索
theHarvester -d <domain> -b google,linkedin

# メールアドレス収集
theHarvester -d <domain> -b all -f output.html
```

## 検索ソースの指定
```bash
# Google検索
theHarvester -d <domain> -b google

# LinkedIn検索
theHarvester -d <domain> -b linkedin

# Twitter検索
theHarvester -d <domain> -b twitter

# Shodan検索
theHarvester -d <domain> -b shodan

# DNS逆引き
theHarvester -d <domain> -b dnsdumpster
```

## 出力オプション
```bash
# HTML形式で出力
theHarvester -d <domain> -b all -f output.html

# XML形式で出力
theHarvester -d <domain> -b all -x output.xml

# JSON形式で出力
theHarvester -d <domain> -b all -J output.json
```

## 高度なオプション
```bash
# 検索結果の制限
theHarvester -d <domain> -b all -l 100

# プロキシの使用
theHarvester -d <domain> -b all --proxy <proxy_url>

# DNS解決の無効化
theHarvester -d <domain> -b all -n

# アクティブ検証の実行
theHarvester -d <domain> -b all -v
```

## 検索の絞り込み
```bash
# 特定のサブドメインの検索
theHarvester -d <domain> -b all -s

# メールアドレスのみの検索
theHarvester -d <domain> -b all -e

# ホスト名のみの検索
theHarvester -d <domain> -b all -h
```

## 注意事項
- APIキーが必要なソース（Shodan等）は事前に設定が必要です
- 過度な検索リクエストは各サービスのレート制限に抵触する可能性があります
- 収集した情報の取り扱いには十分注意してください
- 実環境での使用は必ず許可を得てから行ってください 