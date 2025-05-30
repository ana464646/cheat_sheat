# SMBMap Command Reference

## 基本的な列挙
```bash
# 共有の列挙
smbmap -H <target>

# ユーザー認証付き列挙
smbmap -H <target> -u <username> -p <password>

# ドメイン指定
smbmap -H <target> -d <domain> -u <username> -p <password>
```

## 詳細スキャン
```bash
# 再帰的リスト
smbmap -H <target> -R

# 特定の共有をリスト
smbmap -H <target> -R <share_name>

# ドライブタイプの表示
smbmap -H <target> -d <domain> -u <username> -p <password> --drive-type
```

## ファイル操作
```bash
# ファイルのダウンロード
smbmap -H <target> --download "sharename\path\to\file"

# ファイルのアップロード
smbmap -H <target> --upload "local_file" "sharename\remote_path"

# ファイルの削除
smbmap -H <target> --delete "sharename\path\to\file"
```

## 検索オプション
```bash
# ファイル名での検索
smbmap -H <target> -R -F "pattern"

# 特定の拡張子の検索
smbmap -H <target> -R -A "txt,pdf,doc"

# 最終更新日での検索
smbmap -H <target> -R -q
```

## 高度なオプション
```bash
# ポート指定
smbmap -H <target> -P <port>

# NULLセッションの使用
smbmap -H <target> -u "" -p ""

# コマンド実行（要管理者権限）
smbmap -H <target> -u <username> -p <password> -x "command"
```

## 出力オプション
```bash
# 出力ファイルの指定
smbmap -H <target> --output output.txt

# JSON形式で出力
smbmap -H <target> --json

# 詳細な出力
smbmap -H <target> -v
```

## 注意事項
- 認証情報の取り扱いには十分注意してください
- コマンド実行機能は慎重に使用してください
- 大量のファイル操作はサーバーに負荷をかける可能性があります
- 実環境での使用は必ず許可を得てから行ってください 