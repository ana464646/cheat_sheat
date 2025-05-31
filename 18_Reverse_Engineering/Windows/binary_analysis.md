# Windows Binary Analysis Techniques

**対応OS**: Windows

## 概要
Windows環境でのバイナリ解析手法について解説します。

## 基本的な手法

### 静的解析
```powershell
# PEファイル情報の取得
dumpbin /headers target.exe

# 依存DLLの確認
dumpbin /imports target.exe

# 文字列の抽出
strings -a target.exe

# IDAを使用した解析
# 1. IDAでファイルを開く
# 2. 自動解析の完了を待つ
# 3. 関数グラフの生成
# 4. クロスリファレンスの確認
```

### 動的解析
```powershell
# デバッガのアタッチ
windbg -p <pid>

# ブレークポイントの設定
bp <address>

# メモリダンプの取得
.dump /f dump.dmp

# プロセスモニタリング
procmon /backingfile procmon.pml
```

### アンパッキング
```python
# UPXパッカーの検出と解除
upx -d target.exe

# カスタムパッカーの解析
# 1. エントリーポイントの特定
# 2. デコード/復号ルーチンの特定
# 3. OEPの特定
# 4. ダンプとIATの再構築
```

## 検知回避テクニック
- アンチデバッグ回避
- 仮想マシン検知回避
- タイムスタンプ改ざん
- コード難読化

## 防御策
- コード難読化
- アンチデバッグ
- パッキング
- 整合性チェック

## 検知方法
- デバッガの検知
- 仮想環境の検知
- ファイル改ざんの検知
- 異常な動作パターン

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 