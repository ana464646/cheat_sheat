# Penetration Testing Cheat Sheet

このリポジトリは、ペネトレーションテストで使用される様々なツールのコマンドリファレンスをまとめたものです。
教育目的でのみ使用してください。

## ディレクトリ構造

### Initial Phase (01-02)
- **01_Reconnaissance**: 偵察フェーズのツール群
  - nmap.md (Windows/Linux/macOS)
  - masscan.md (Linux)
  - dnsrecon.md (Linux/Python)
  - theharvester.md (Linux/Python)
  - gobuster.md (Linux)
  - wpscan.md (Linux/Ruby)
  - nikto.md (Linux/Perl)
  - smbmap.md (Linux/Python)
- **02_Initial_Access**: 初期アクセスフェーズのツール群
  - metasploit.md (Linux優先、Windows可)
  - set.md (Linux)
  - powersploit.md (Windows)

### Persistence Phase (03-06)
- **03_Privilege_Escalation**: 権限昇格のツール群
  - Linux/
    - linpeas.md
  - Windows/
    - winpeas.md
- **04_Persistence**: 永続化のツール群
  - Linux/
  - Windows/
- **05_Defense_Evasion**: 検知回避のツール群
  - Linux/
  - Windows/
- **06_Credential_Access**: 認証情報取得のツール群
  - Linux/
  - Windows/

### Movement Phase (07-08)
- **07_Lateral_Movement**: 横展開のツール群
  - Linux/
  - Windows/
    - mimikatz.md
- **08_Collection**: データ収集のツール群
  - Linux/
  - Windows/

### Advanced Techniques (09-20)
- **09_Active_Directory_Attacks**: Active Directory攻撃のツール群
  - Linux/
  - Windows/
    - bloodhound.md
- **15_Wireless_Attacks**: 無線攻撃のツール群
  - Linux/
  - Windows/
- **16_Web_Application**: Webアプリケーション攻撃のツール群
  - Linux/
  - Windows/
- **17_Mobile_Analysis**: モバイルアプリケーション解析のツール群
  - Linux/
  - Windows/
- **18_Reverse_Engineering**: リバースエンジニアリングのツール群
  - Linux/
  - Windows/
- **19_Malware_Analysis**: マルウェア解析のツール群
  - Linux/
  - Windows/
- **20_IoT_Security**: IoTセキュリティのツール群
  - Linux/
  - Windows/

## 使用方法

1. 各ツールのマークダウンファイルには以下の情報が含まれています：
   - 対応OS情報
   - 基本的な使用方法
   - よく使用するオプション
   - 高度な設定オプション
   - 注意事項

2. 必要なツールのドキュメントに移動し、目的の操作に関する情報を参照してください。

## 注意事項

- このリポジトリは教育目的でのみ使用してください
- 記載されているツールの使用は、許可された環境でのみ行ってください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのツールは自己責任で使用してください

## 貢献

- バグの報告や新しいツールの追加は、Issue/Pull Requestでお願いします
- ドキュメントの改善提案も歓迎します

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。
