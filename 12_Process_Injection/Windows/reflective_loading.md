# Reflective Loading Techniques

**対応OS**: Windows

## 概要
リフレクティブローディングは、ディスクに痕跡を残さずにメモリ上でDLLを直接ロードする手法です。

## 基本的な実装

### リフレクティブローダー
```cpp
typedef HMODULE (*REFLECTIVELOADER)(VOID);

HMODULE WINAPI ReflectiveLoader(VOID)
{
    // DLLのベースアドレスを取得
    ULONG_PTR uiBaseAddress = GetBaseAddress();
    
    // PEヘッダーの解析
    PIMAGE_NT_HEADERS pNtHeaders = GetNtHeaders(uiBaseAddress);
    
    // メモリの確保
    PVOID lpAddress = VirtualAlloc(NULL,
        pNtHeaders->OptionalHeader.SizeOfImage,
        MEM_RESERVE | MEM_COMMIT,
        PAGE_EXECUTE_READWRITE);
    
    // セクションのマッピング
    MapSections(lpAddress, uiBaseAddress);
    
    // 再配置の処理
    ProcessRelocations(lpAddress, uiBaseAddress);
    
    // インポートの解決
    ProcessImports(lpAddress);
    
    return (HMODULE)lpAddress;
}
```

### メモリ内実行
```cpp
// リフレクティブローダーの実行
LPVOID pReflectiveLoader = GetReflectiveLoader(lpBuffer);
HANDLE hThread = CreateThread(NULL, 0,
    (LPTHREAD_START_ROUTINE)pReflectiveLoader,
    NULL, 0, NULL);
```

## 高度なテクニック

### PEヘッダーの解析
```cpp
PIMAGE_NT_HEADERS GetNtHeaders(ULONG_PTR uiBaseAddress)
{
    PIMAGE_DOS_HEADER pDosHeader = (PIMAGE_DOS_HEADER)uiBaseAddress;
    return (PIMAGE_NT_HEADERS)((ULONG_PTR)uiBaseAddress + 
        pDosHeader->e_lfanew);
}
```

### インポート解決
```cpp
BOOL ProcessImports(PVOID lpAddress)
{
    // カーネル32のベースアドレス取得
    HMODULE hKernel32 = GetK32Base();
    
    // GetProcAddressの取得
    GETPROCADDRESS pGetProcAddress = GetGetProcAddress(hKernel32);
    
    // インポートの解決
    ResolveImports(lpAddress, hKernel32, pGetProcAddress);
    
    return TRUE;
}
```

## 検知回避テクニック
- PEヘッダーの難読化
- メモリパターンの偽装
- APIコールの隠蔽
- アンチデバッグ

## 防御策
- メモリスキャンの実施
- 不審なメモリ領域の検知
- APIフックの実装
- ヒューリスティック検知

## 検知方法
- 不審なメモリアロケーション
- PEシグネチャのスキャン
- APIコール監視
- メモリダンプ分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 