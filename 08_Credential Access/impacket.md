# impacket
impacketの基本的な使い方を記載

# Overview
Impacketは、ネットワークプロトコルを操作するためのPythonクラスのコレクションです。主にセキュリティテストやエクスプロイトに使用され、低レベルのプログラムインターフェースを提供します。Impacketは、ペネトレーションテストやセキュリティ研究で広く使用されています

Impacketの主な特徴は以下の通りです:

広範なプロトコルサポート: IP、UDP、TCPなどの低レベルプロトコルから、NMBやSMBなどの高レベルプロトコルまでサポートしています。

柔軟なAPI: 高レベルおよび低レベルのAPIを提供し、柔軟な操作が可能です。

豊富なサンプルスクリプト: 一般的なタスクのためのサンプルスクリプトが含まれています。

Impacketの使用例として、SMB接続の作成、NTLM認証の実行、DCE/RPCリクエストの送信などがあります。

https://github.com/fortra/impacket

# Usage

インストール方法

```
python3 -m pipx install impacket
```

ユーザーの認証情報を取得している場合

```
enum4linux -u <ユーザー名> -p <パスワード> -a 10.10.10.10
```
