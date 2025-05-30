# LinPEAS Command Reference

**対応OS**: Linux

## 基本的な使用方法
```bash
# 直接実行（curl経由）
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# ファイルをダウンロードして実行
wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```

## 実行オプション
```bash
# 全チェックを実行（デフォルト）
./linpeas.sh

# 特定のチェックのみ実行
./linpeas.sh -a # 自動化された全チェック
./linpeas.sh -s # SUIDバイナリチェック
./linpeas.sh -w # Webサーバー関連チェック
```

## 出力オプション
```bash
# 結果をファイルに保存
./linpeas.sh | tee results.txt

# HTMLレポート生成
./linpeas.sh -h

# JSONフォーマットで出力
./linpeas.sh -j
```

## 高度なオプション
```bash
# 特権昇格ベクトルのみ表示
./linpeas.sh -P

# 色なしで実行
./linpeas.sh -N

# デバッグモード
./linpeas.sh -D
```

## メモリ使用量の最適化
```bash
# 軽量モード
./linpeas.sh -l

# 最小限のチェック
./linpeas.sh -M
```

## 注意事項
- 実行前に必ずファイルの内容を確認してください
- 本番環境での実行は慎重に行ってください
- 結果には機密情報が含まれる可能性があります
- システムに影響を与える可能性があるため、テスト環境での実行を推奨します 