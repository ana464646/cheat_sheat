# DLL Hijacking Techniques

**対応OS**: Windows

## 概要
DLLハイジャックは、アプリケーションのDLL検索順序を悪用して不正なDLLを読み込ませる攻撃手法です。

## DLL検索順序
1. アプリケーションのディレクトリ
2. システムディレクトリ（System32）
3. 16ビットシステムディレクトリ
4. Windowsディレクトリ
5. カレントディレクトリ
6. PATH環境変数のディレクトリ

## 攻撃手法

### DLL Proxying
```cpp
#include <windows.h>

// オリジナルDLLの関数をエクスポート
__declspec(dllexport) void OriginalFunction()
{
    // マリシャスコードを実行
    // オリジナルの関数も呼び出す
}

BOOL APIENTRY DllMain(HMODULE hModule,
    DWORD  ul_reason_for_call,
    LPVOID lpReserved)
{
    switch (ul_reason_for_call)
    {
    case DLL_PROCESS_ATTACH:
        // 初期化コード
        break;
    }
    return TRUE;
}
```

### DLL Side-Loading
- 正規アプリケーションと同じディレクトリに悪意のあるDLLを配置
- アプリケーション起動時に自動的に読み込まれる

## 検知回避テクニック
- DLL名の偽装
- 正規DLLの機能を維持
- 遅延読み込みの利用
- 条件付き実行

## 防御策
- SafeDllSearchModeの有効化
- アプリケーションディレクトリの権限制限
- DLL読み込みパスの制限
- デジタル署名の検証

## 検知方法
- 不審なDLLファイルの監視
- DLL読み込みイベントの監視
- プロセスの挙動分析
- ファイルシステムの変更監視

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 