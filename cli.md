```
curl --version
```
```
curl 8.5.0 (x86_64-pc-linux-gnu) libcurl/8.5.0 OpenSSL/3.0.13 zlib/1.3 brotli/1.1.0 zstd/1.5.5 libidn2/2.3.7 libpsl/0.21.2 (+libidn2/2.3.7) libssh/0.10.6/openssl/zlib nghttp2/1.59.0 librtmp/2.3 OpenLDAP/2.6.10
Release-Date: 2023-12-06, security patched: 8.5.0-2ubuntu10.7
Protocols: dict file ftp ftps gopher gophers http https imap imaps ldap ldaps mqtt pop3 pop3s rtmp rtsp scp sftp smb smbs smtp smtps telnet tftp
Features: alt-svc AsynchDNS brotli GSS-API HSTS HTTP2 HTTPS-proxy IDN IPv6 Kerberos Largefile libz NTLM PSL SPNEGO SSL threadsafe TLS-SRP UnixSockets zstd
```

最新版curlのインストール
```
wget https://github.com/curl/curl/releases/download/curl-8_21_0/curl-8.21.0.tar.gz
tar xzf curl-8.21.0.tar.gz
cd curl-8.21.0
./configure --with-openssl --without-libpsl
make
make install
```

WebSocket接続テスト
```
src/curl -v wss://echo.websocket.org
```
```
* Received 101, Switching to WebSocket
* [WS] Received 101, switch to WebSocket
```

WebSocketデータ送信
```
echo hello | src/curl -sS -T - wss://echo.websocket.org
```
```
Request served by 4d896d95b55478hello
```

MQTTパブリッシュ
```
src/curl -u public:public -d hi mqtt://public.cloud.shiftr.io/nodered -v
```
```
* Host public.cloud.shiftr.io:1883 was resolved.
* IPv6: (none)
* IPv4: 34.77.13.55
*   Trying 34.77.13.55:1883...
* Established connection to public.cloud.shiftr.io (34.77.13.55 port 1883) from 10.0.10.48 port 37464 
* Using client id 'curlDdV1teQm'
> (MQTT�<
         curlDdV1teQmpublicpublicmqtt_doing: state [0]
* mqtt_doing: state [0]
<  mqtt_doing: state [2]
< 0
   noderedhi�shutting down connection #0
```

MQTTサブスクライブ(受信すると停止してしまう)
```
src/curl -sS -N -u public:public mqtt://public.cloud.shiftr.io/nodered
```

```
curl -sS -N -T - ws://localhost:8000
curl -sS -N -T - wss://localhost:8443
curl -sS tftp://localhost
curl -sS imap://node:password@localhost:2143/INBOX
curl -sS pop3://node:password@localhost:2110
curl -sS sftp://demo:password@localhost:2223/readme.txt

cat <<'EOF' > /tmp/curl_smtp_message.txt
From: test@example.com
To: node@localhost
Subject: curl smtp test

hello
EOF
./src/curl -sS --url smtp://localhost:2525 --mail-from test@example.com --mail-rcpt node@localhost --upload-file /tmp/curl_smtp_message.txt
```

# mosquiitoコマンド
```
mosquitto_sub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -d

mosquitto_pub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -m "Hello" -d

{"movement":{"alpha":-311.62,"beta":104.9,"gamma":62.01},"acceleration":{"x":-0.12,"y":0.07,"z":-0.14}}
{"movement":{"alpha":-311.62,"beta":104.88,"gamma":62.28},"acceleration":{"x":-0.12,"y":0.09,"z":-0.02}}
{"movement":{"alpha":-311.62,"beta":104.96,"gamma":62.21},"acceleration":{"x":-0.1,"y":0.09,"z":-0.04}}
```

