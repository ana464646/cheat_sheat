# Office Template Attacks

**対応OS**: Windows

## 概要
Microsoft Officeのテンプレート機能を悪用した攻撃手法について解説します。

## テンプレートの種類

### Normal.dotm
```
%APPDATA%\Microsoft\Templates\Normal.dotm
```
- Wordのデフォルトテンプレート
- 新規文書作成時に自動的に読み込まれる
- マクロやスタイルの永続化に使用可能

### カスタムテンプレート
```
%APPDATA%\Microsoft\Templates\Custom.dotx
```
- ユーザー定義テンプレート
- 特定の文書タイプに対して使用
- マクロやカスタム設定を含むことが可能

## 攻撃テクニック

### テンプレートの置換
```vb
' テンプレートファイルのパスを取得
Dim templatePath As String
templatePath = Application.StartupPath & "\Templates\Normal.dotm"
```

### 自動実行マクロ
```vb
Sub AutoNew()
    ' 新規文書作成時に実行
End Sub

Sub AutoOpen()
    ' 文書を開く時に実行
End Sub
```

## 検知回避
- テンプレートファイルの難読化
- マクロコードの分割
- 条件付き実行
- 遅延実行

## 防御策
- テンプレートフォルダの監視
- 不審なテンプレートファイルの検出
- マクロセキュリティ設定の強化
- アプリケーションの制限付き実行

## 検知方法
- テンプレートファイルの変更監視
- 不審なマクロの検出
- 異常なプロセス生成
- ファイルシステムの変更監視

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 