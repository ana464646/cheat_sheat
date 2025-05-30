# Masscan Command Reference

**対応OS**: Linux (Windows上ではWSL2での実行を推奨)

## 基本スキャン
```bash
# 全ポートスキャン
masscan -p1-65535 <target> --rate=1000

# 特定ポートのスキャン
masscan -p80,443,8080 <target> --rate=1000

# 結果をファイルに出力
masscan -p1-65535 <target> --rate=1000 -oJ output.json
```

## 高度なオプション
```bash
# スキャン速度の調整
masscan -p1-65535 <target> --rate=10000  # 高速
masscan -p1-65535 <target> --rate=100    # 低速

# 出力フォーマット
masscan -p1-65535 <target> --rate=1000 -oX output.xml  # XML形式
masscan -p1-65535 <target> --rate=1000 -oL output.list # リスト形式
masscan -p1-65535 <target> --rate=1000 -oG output.grep # Grepable形式

# 特定のIPレンジをスキャン
masscan -p80,443 192.168.0.0/16 --rate=1000

# 除外IPの指定
masscan -p80,443 <target> --excludefile exclude.txt --rate=1000
```

## バナー取得
```bash
# バナー情報の取得
masscan -p80,443 <target> --rate=1000 --banners

# バナー取得タイムアウトの設定
masscan -p80,443 <target> --rate=1000 --banners --wait=5
```

## 注意事項
- 高速スキャンはネットワークに負荷をかける可能性があります
- 実環境での使用は必ず許可を得てから行ってください
- スキャン速度は環境に応じて適切に設定してください
- 大規模なネットワークスキャンは慎重に行ってください 