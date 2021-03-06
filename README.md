## Native Nim MQTT client library, work in progress

## Examples

```nim
import nmqtt, asyncdispatch

let ctx = newMqttCtx("hallo")

ctx.set_host("test.mosquitto.org", 1883)
#ctx.set_auth("username", "password")

await ctx.start()
proc on_data(topic: string, message: string) =
echo "got ", topic, ": ", message

await ctx.publish("test1", "hallo", 2)
await ctx.subscribe("#", 0, on_data)

asyncCheck flop()
runForever()
```


# Procs

## newMqttCtx*

```nim
proc newMqttCtx*(clientId: string): MqttCtx =
```

Initiate a new MQTT client


____

## set_host*

```nim
proc set_host*(ctx: MqttCtx, host: string, port: int=1883, doSsl=false) =
```

Set the MQTT host


____

## set_auth*

```nim
proc set_auth*(ctx: MqttCtx, username: string, password: string) =
```

Set the authentication for the host


____

## start*

```nim
proc start*(ctx: MqttCtx) {.async.} =
```

Connect to the host.

 You might want to insert a `await sleepAsync 3000`, to let the first pings through before sending.


____

## publish*

```nim
proc publish*(ctx: MqttCtx, topic: string, message: string, qos=0) {.async.} =
```

Publish a message


____

## subscribe*

```nim
proc subscribe*(ctx: MqttCtx, topic: string, qos: int, callback: PubCallback) {.async.} =
```

Subscribe to a topic


____

