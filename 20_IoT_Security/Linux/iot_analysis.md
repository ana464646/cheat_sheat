# IoT Device Analysis Techniques (Linux)

**対応OS**: Linux

## 概要
Linux環境でのIoTデバイスの解析手法について解説します。

## 基本的な手法

### ファームウェア解析
```bash
# ファームウェアの展開
dd if=firmware.bin of=firmware.img
fdisk -l firmware.img
mount -o loop,offset=<offset> firmware.img /mnt/firmware

# ファイルシステム解析
tree /mnt/firmware
find /mnt/firmware -type f -exec file {} \;

# バイナリ解析
for file in $(find /mnt/firmware -type f -executable); do
    strings $file | grep -i "password"
    readelf -a $file 2>/dev/null
done
```

### 通信解析
```python
# MQTT通信の監視
import paho.mqtt.client as mqtt

def on_connect(client, userdata, flags, rc):
    print(f"Connected with result code {rc}")
    client.subscribe("#")

def on_message(client, userdata, msg):
    print(f"Topic: {msg.topic}")
    print(f"Message: {msg.payload.decode()}")

client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message
client.connect("localhost", 1883, 60)
client.loop_forever()

# CoAP通信の監視
from coapthon.client.helperclient import HelperClient

client = HelperClient(server=("localhost", 5683))
response = client.get("/.well-known/core")
print(response.pretty_print())
client.stop()
```

### ハードウェアデバッグ
```bash
# GPIOの制御
echo "18" > /sys/class/gpio/export
echo "out" > /sys/class/gpio/gpio18/direction
echo "1" > /sys/class/gpio/gpio18/value

# I2Cバスのスキャン
i2cdetect -y 1

# SPIデバイスの確認
ls -l /dev/spidev*

# シリアル通信の監視
minicom -D /dev/ttyUSB0 -b 115200
```

## 検知回避テクニック
- カーネルモジュール検知回避
- デバイスドライバ改変
- ハードウェアデバッグ保護回避
- 通信プロトコル改変

## 防御策
- セキュアブート
- デバイスドライバ署名
- ハードウェアセキュリティ
- 通信の暗号化

## 検知方法
- システムコール監視
- デバイスドライバ監視
- 通信パターン分析
- ハードウェア改ざん検知

## 注意事項
- このテクニックは教育目的でのみ使用してください
- 実環境での使用は法的責任を伴う可能性があります
- すべてのテストは許可された環境でのみ行ってください 