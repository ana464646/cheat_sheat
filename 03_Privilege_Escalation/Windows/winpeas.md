# WinPEAS Command Reference

**対応OS**: Windows

## 基本的な使用方法
```powershell
# EXEバージョンの実行
winPEASx64.exe

# バッチファイルバージョンの実行
winPEAS.bat
```

## 実行オプション
```powershell
# すべてのチェックを実行
winPEASx64.exe

# 特定のチェックを実行
winPEASx64.exe windowscreds
winPEASx64.exe fileinfo
winPEASx64.exe servicesinfo

# 管理者権限で実行
winPEASx64.exe debug
```

## 出力設定
```powershell
# 結果をファイルに保存
winPEASx64.exe > results.txt

# 詳細度の設定
winPEASx64.exe quiet   # 最小限の出力
winPEASx64.exe nocolor # 色なしで出力
```

## 特定の検査項目
```powershell
# システム情報
winPEASx64.exe systeminfo

# ユーザー情報
winPEASx64.exe userinfo

# プロセス情報
winPEASx64.exe processinfo

# サービス情報
winPEASx64.exe servicesinfo
```

## 高度な検査
```powershell
# ネットワーク情報
winPEASx64.exe networkinfo

# ブラウザ情報
winPEASx64.exe browserinfo

# アプリケーション情報
winPEASx64.exe applicationsinfo

# セキュリティ製品情報
winPEASx64.exe windowsdefender
```

## バッチファイルバージョンの特別オプション
```batch
# 基本実行
winPEAS.bat

# 特定のチェックを実行
winPEAS.bat notcolor domain
winPEAS.bat notcolor all
```

## 注意事項
- アンチウイルスソフトに検知される可能性があります
- 実行前にファイルの安全性を確認してください
- 本番環境での実行は慎重に行ってください
- 結果には機密情報が含まれる可能性があります 