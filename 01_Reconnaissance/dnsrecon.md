# DNSrecon Command Reference

**対応OS**: Linux (Windows上ではWSL2/Python環境での実行が可能)

## 基本的なDNS列挙
```bash
# 標準的なDNS列挙
dnsrecon -d <domain>

# 詳細な出力
dnsrecon -d <domain> -v

# 結果をファイルに出力
dnsrecon -d <domain> -c output.csv
dnsrecon -d <domain> -j output.json
dnsrecon -d <domain> -x output.xml
```

## 高度な列挙オプション
```bash
# ブルートフォース
dnsrecon -d <domain> -t brt -D /path/to/wordlist.txt

# ゾーン転送
dnsrecon -d <domain> -t axfr

# Google検索を使用したサブドメイン列挙
dnsrecon -d <domain> -t goo

# サブドメインの逆引き
dnsrecon -d <domain> -t rvl
```

## 特殊な検索オプション
```bash
# SPFレコードの列挙
dnsrecon -d <domain> -t spf

# SRVレコードの列挙
dnsrecon -d <domain> -t srv

# MXレコードの列挙
dnsrecon -d <domain> -t mx

# 標準的なレコードタイプの列挙
dnsrecon -d <domain> -t std
```

## ネームサーバー指定
```bash
# 特定のネームサーバーを使用
dnsrecon -d <domain> -n <nameserver>

# 複数のネームサーバーを使用
dnsrecon -d <domain> -n <nameserver1>,<nameserver2>
```

## レンジスキャン
```bash
# IPレンジのPTRレコードスキャン
dnsrecon -r <ip-range> 

# CIDRレンジのスキャン
dnsrecon -r 192.168.1.0/24
```

## 注意事項
- DNSクエリの頻度は対象サーバーの負荷を考慮して調整してください
- ゾーン転送は許可された環境でのみ実行してください
- ブルートフォース攻撃は対象システムに負荷をかける可能性があります
- 実環境での使用は必ず許可を得てから行ってください 