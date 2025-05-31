# Linux Binary Analysis Techniques

**対応OS**: Linux

## 概要
Linux環境でのバイナリ解析手法について解説します。

## 基本的な手法

### 静的解析
```bash
# ELFファイル情報の取得
readelf -h target

# シンボル情報の取得
nm target

# 共有ライブラリの依存関係
ldd target

# 逆アセンブル
objdump -d target

# Ghidraを使用した解析
# 1. プロジェクトの作成
# 2. バイナリのインポート
# 3. 自動解析の実行
# 4. デコンパイル結果の確認
```

### 動的解析
```bash
# GDBの起動
gdb ./target

# ブレークポイントの設定
b *main
b *0x4005f0

# メモリの確認
x/10x $rsp
x/s $rdi

# バックトレース
bt

# プロセストレース
strace ./target
```

### バイナリ解析フレームワーク
```python
# Radareを使用した解析
r2 ./target
[0x004005d0]> aaa    # 解析
[0x004005d0]> afl    # 関数一覧
[0x004005d0]> pdf @main  # main関数の逆アセンブル

# Angr使用例
import angr

# バイナリの読み込み
proj = angr.Project('./target', load_options={'auto_load_libs': False})

# シンボリック実行
state = proj.factory.entry_state()
simgr = proj.factory.simulation_manager(state)
simgr.explore(find=0x4005f0)
```

## 検知回避テクニック
- ptrace検知回避
- タイムスタンプ検知回避
- ファイルシステム監視回避
- メモリ改ざん検知回避

## 防御策
- ASLR有効化
- スタック保護
- PIE有効化
- セクション保護

## 検知方法
- システムコール監視
- ファイル整合性チェック
- メモリ改ざん検知
- デバッガ検知

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 