最新版curlのインストール
```
wget https://github.com/curl/curl/releases/download/curl-8_21_0/curl-8.21.0.tar.gz
tar xzf curl-8.21.0.tar.gz
cd curl-8.21.0
./configure --with-openssl --without-libpsl
make
```

接続テスト
```
src/curl -v wss://echo.websocket.org
```
```
* Received 101, Switching to WebSocket
* [WS] Received 101, switch to WebSocket
```

データ送信
```
echo hello | src/curl -sS -T - wss://echo.websocket.org
```
```
Request served by 4d896d95b55478hello
```

```
mosquitto_sub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -d

mosquitto_pub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -m "Hello" -d

{"movement":{"alpha":-311.62,"beta":104.9,"gamma":62.01},"acceleration":{"x":-0.12,"y":0.07,"z":-0.14}}
{"movement":{"alpha":-311.62,"beta":104.88,"gamma":62.28},"acceleration":{"x":-0.12,"y":0.09,"z":-0.02}}
{"movement":{"alpha":-311.62,"beta":104.96,"gamma":62.21},"acceleration":{"x":-0.1,"y":0.09,"z":-0.04}}
```

