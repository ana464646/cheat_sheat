# impacket
impacketの基本的な使い方を記載
88/tcpが空いている場合、ユーザー名やパスワード、ブルートフォース可否の列挙が可能

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

ASREPRoast攻撃
ASREPRoast攻撃は、Kerberos認証プロトコルの脆弱性を悪用する攻撃手法です。この攻撃は、Kerberosの事前認証が無効になっているユーザーアカウントを対象とします

通常、Kerberos認証では、ユーザーが認証サーバーリクエスト（AS-REQ）をドメインコントローラー（DC）に送信し、ユーザーのパスワードハッシュで暗号化されたタイムスタンプを含めます。DCはこのタイムスタンプを復号し、成功すると認証サーバーレスポンス（AS-REP）を返します。このAS-REPには、キー配布センター（KDC）によって発行されたチケットグラントチケット（TGT）が含まれています。

しかし、事前認証が無効になっている場合、DCはAS-REQを受信するとすぐにAS-REPを送信します。このAS-REPには、ユーザーのパスワードハッシュで暗号化されたデータが含まれており、攻撃者はこのデータを取得してオフラインでブルートフォース攻撃や辞書攻撃を行うことができます。

ASREPRoast攻撃は、事前認証が無効になっているアカウントを標的にするため、攻撃者はこれを利用してドメインリソースへの不正アクセスを試みます。この攻撃を防ぐためには、Kerberosの事前認証を有効にすることが推奨されます。

オプション
-usersfile: enum4linuxコマンドにて列挙したユーザーリストファイルusernames.txtを使用します。

-format: パスワードハッシュのフォーマットとして、john形式にて出力させます。

-outputfile: 結果をhtb-forest.txtファイルに出力させます。

```
python3 GetNPUsers.py <domain_name>/ -usersfile <users_file> -format <AS_REP_responses_format [hashcat | john]> -outputfile <output_AS_REP_responses_file>
```

ドメインユーザーの列挙
```
python3 GetNPUsers.py -all -dc-ip 10.10.10.10 <ドメイン名>/<ユーザー名>
```



ドメインの委任関係を見つけるためにfindDelegation.pyを使用します。
findDelegation.pyは、Impacketツールの一部で、ドメイン内の委任関係を見つけるために使用されます。このスクリプトは、無制限の委任、制約付き委任、およびリソースベースの制約付き委任のタイプをクエリして表示します

以下は、findDelegation.pyの主なオプションとその説明です

-h, --help: ヘルプメッセージを表示します。

-u, --username: 認証に使用するユーザー名を指定します。

-p, --password: 認証に使用するパスワードを指定します。

-d, --domain: 認証に使用するドメインを指定します。

-td, --target-domain: ターゲットドメインを指定します。

-k, --kerberos: Kerberos認証を使用する場合に指定します。

-aesKey: AESキーを指定します。

-dc-ip: ドメインコントローラーのIPアドレスを指定します。

-dc-host: ドメインコントローラーのホスト名を指定します。

-hashes: LMハッシュとNTハッシュを指定します（形式：LMHASH:NTHASH）

これらのオプションを使用することで、findDelegation.pyはドメイン内の委任関係を詳細に調査し、特定のユーザーやシステムへのアクセス権を確認することができます。

```
python3 findDelegation.py -dc-ip 10.10.10.10 <ドメイン名>/<ユーザー名>
```
