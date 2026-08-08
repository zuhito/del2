```
mosquitto_sub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered"

mosquitto_pub -h public.cloud.shiftr.io -u "public" -P "public" -t "nodered" -m "Hello"

{"movement":{"alpha":-311.62,"beta":104.9,"gamma":62.01},"acceleration":{"x":-0.12,"y":0.07,"z":-0.14}}
{"movement":{"alpha":-311.62,"beta":104.88,"gamma":62.28},"acceleration":{"x":-0.12,"y":0.09,"z":-0.02}}
{"movement":{"alpha":-311.62,"beta":104.96,"gamma":62.21},"acceleration":{"x":-0.1,"y":0.09,"z":-0.04}}
```
