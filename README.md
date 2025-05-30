# Penetration Testing Cheat Sheet

**DO NOT ABUSE - FOR EDUCATIONAL PURPOSES ONLY**

A comprehensive collection of penetration testing commands and techniques organized by attack phases. This repository follows the MITRE ATT&CK framework structure.

## Categories Description

### Initial Phase (01-02)
- **Reconnaissance**: ネットワークスキャン、情報収集、脆弱性スキャン
- **Initial Access**: エクスプロイト、フィッシング、初期侵入手法

### Persistence Phase (04-06)
- **Persistence**: バックドア、永続化手法、自動実行
- **Defense Evasion**: アンチウイルス回避、ログ削除、痕跡隠蔽
- **Credential Access**: パスワード取得、ハッシュ取得、認証情報窃取

### Movement Phase (07-08)
- **Discovery**: ネットワーク探索、ホスト列挙、サービス特定
- **Command And Control**: C2通信、遠隔操作、通信制御

### Advanced Techniques (15-20)
- **Active Directory**: ドメイン攻撃、Kerberos攻撃、DCSync
- **Cloud Infrastructure**: クラウドサービス攻撃、コンテナ攻撃
- **Lateral Movement**: 内部移動、リモート実行、アカウント利用
- **Network Pivoting**: トンネリング、プロキシ、中継攻撃
- **Data Exfiltration**: データ窃取、隠れチャネル、ステガノグラフィ
- **Wireless Attacks**: WiFi攻撃、Bluetooth攻撃、無線LAN攻撃

## Usage Guidelines

### 基本的な使用方法
1. 各ディレクトリには詳細な技術解説とコマンド例が含まれています
2. Windows/Linuxそれぞれの環境に特化した手法を参照できます
3. コマンドは実行前に内容を理解し、影響を確認してください
4. テスト環境での実行を強く推奨します

### 注意事項
- このリポジトリは教育目的でのみ使用してください
- 記載された技術の不正使用は違法となる可能性があります
- 実環境での使用は必ず許可を得てから行ってください
- システムに重大な影響を与える可能性のある操作が含まれています

## Contribution

以下の形での貢献を歓迎します：
- 新しい攻撃手法の追加
- 既存のドキュメントの改善
- エラーや誤字の修正
- 実例やユースケースの追加

プルリクエストを通じて貢献してください。

## License

This project is licensed under MIT License - see the LICENSE file for details.
