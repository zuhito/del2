最新版curlのインストール
```
wget https://github.com/curl/curl/releases/download/curl-8_21_0/curl-8.21.0.tar.gz
tar xzf curl-8.21.0.tar.gz
cd curl-8.21.0
./configure --with-openssl --without-libpsl
make
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
mosquitto_sub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -d

mosquitto_pub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -m "Hello" -d

{"movement":{"alpha":-311.62,"beta":104.9,"gamma":62.01},"acceleration":{"x":-0.12,"y":0.07,"z":-0.14}}
{"movement":{"alpha":-311.62,"beta":104.88,"gamma":62.28},"acceleration":{"x":-0.12,"y":0.09,"z":-0.02}}
{"movement":{"alpha":-311.62,"beta":104.96,"gamma":62.21},"acceleration":{"x":-0.1,"y":0.09,"z":-0.04}}
```

