# Penetration Testing Cheat Sheet

**DO NOT ABUSE - FOR EDUCATIONAL PURPOSES ONLY**

A comprehensive collection of penetration testing commands and techniques organized by attack phases. This repository follows the MITRE ATT&CK framework structure.

## Structure

```
├── 01_Reconnaissance/          # 情報収集技術
│   ├── Windows/               # Windows環境での情報収集
│   └── Linux/                 # Linux環境での情報収集
├── 02_Initial_Access/         # 初期アクセス手法
│   ├── Windows/               # Windows環境での初期アクセス
│   └── Linux/                 # Linux環境での初期アクセス
├── 03_Privilege_Escalation/   # 権限昇格技術
│   ├── Windows/               # Windows権限昇格
│   └── Linux/                 # Linux権限昇格
├── 04_Persistence/            # 永続化手法
│   ├── Windows/               # Windows永続化
│   └── Linux/                 # Linux永続化
├── 05_Defense_Evasion/        # 防御回避技術
│   ├── Windows/               # Windows防御回避
│   └── Linux/                 # Linux防御回避
├── 06_Credential_Access/      # 認証情報取得
│   ├── Windows/               # Windows認証情報
│   └── Linux/                 # Linux認証情報
├── 07_Discovery/              # システム探索
│   ├── Windows/               # Windows探索
│   └── Linux/                 # Linux探索
├── 08_Lateral_Movement/       # 横展開手法
│   ├── Windows/               # Windows横展開
│   └── Linux/                 # Linux横展開
├── 09_Command_And_Control/    # C2通信手法
│   ├── Windows/               # WindowsでのC2
│   └── Linux/                 # LinuxでのC2
├── 10_Active_Directory/       # Active Directory攻撃
│   ├── Enumeration/          # AD列挙
│   ├── Exploitation/         # AD脆弱性攻撃
│   └── Post_Exploitation/    # AD権限維持
├── 11_Cloud_Infrastructure/   # クラウド環境攻撃
│   ├── AWS/                  # AWS攻撃手法
│   ├── Azure/                # Azure攻撃手法
│   └── GCP/                  # GCP攻撃手法
├── 12_Network_Pivoting/       # ネットワークピボット
│   ├── Tunneling/            # トンネリング手法
│   └── Proxy_Chains/         # プロキシチェーン
├── 13_Data_Exfiltration/     # データ窃取手法
│   ├── Covert_Channels/      # 隠れチャネル
│   └── Staging/              # データステージング
└── 14_Wireless_Attacks/      # 無線ネットワーク攻撃
    ├── WiFi/                 # WiFi攻撃手法
    └── Bluetooth/            # Bluetooth攻撃手法
```

## Categories Description

### Initial Phase (01-03)
- **Reconnaissance**: ネットワークスキャン、情報収集、脆弱性スキャン
- **Initial Access**: エクスプロイト、フィッシング、初期侵入手法
- **Privilege Escalation**: 権限昇格、脆弱性悪用、特権取得

### Persistence Phase (04-06)
- **Persistence**: バックドア、永続化手法、自動実行
- **Defense Evasion**: アンチウイルス回避、ログ削除、痕跡隠蔽
- **Credential Access**: パスワード取得、ハッシュ取得、認証情報窃取

### Movement Phase (07-09)
- **Discovery**: ネットワーク探索、ホスト列挙、サービス特定
- **Lateral Movement**: 内部移動、リモート実行、アカウント利用
- **Command And Control**: C2通信、遠隔操作、通信制御

### Advanced Techniques (10-14)
- **Active Directory**: ドメイン攻撃、Kerberos攻撃、DCSync
- **Cloud Infrastructure**: クラウドサービス攻撃、コンテナ攻撃
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
