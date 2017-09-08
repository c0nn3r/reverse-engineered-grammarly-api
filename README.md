# Reverse Engineering the Grammarly API

My attempt to reverse engineer the Grammarly API.

First, you need to find a way to look at the web requests when you write. You can't do this just on the page you are using Grammarly on, you need to go to the extention page and inspect the `forge.html` view.

I'm going to ignore the tracking request to `f-log-extension.grammarly.io` for now, but here it is for later:
```json
{
    "message": "init in the field",
    "logger": "usage.session.init",
    "level": "INFO",
    "application": "extensionChrome",
    "version": "14.800.1159",
    "env":"prod", 
    "extra_usage":
    {
        "domain": "mail.google.com",
        "accountType": "Free",
        "fieldType": "contenteditable",
        "fieldSupported": true,
        "groupInfo": 328246984
    }
}
```

Grammarly then opens a connection to `wss://capi.grammarly.com/freews`.

sent
```
{
    "token": null,
    "docid": "e769a7d9-37cb-f4e9-c25a-38b24d045c81",
    "client":"extension_chrome",
    "protocolVersion":"1.0",
    "clientVersion":"14.800.1159",
    "extDomain":"mail.google.com",
    "action":"start",
    "id":0
}
```

sent
```
{
    "ch": ["+0:0:\n:0"],
    "rev":0,
    "action":"submit_ot",
    "id":1
}
```

got
```
{
    "sid":0,
    "action": "start",
    "id":0
}
```

got
```
{
    "rev": 0,
    "action": "submit_ot",
    "id": 1
}
```

sent
```
{
    "name":"gnar_containerId",
    "value":"r88N2V1wqvv8",
    "action":"option","id":2
}
```

got
```
{
    "action": "option",
    "id": 2
}
```

got
```
{
    "sid": 1,
    "rev": 0,
    "score": 100,
    "removed": [],
    "errors": 0,
    "interrupts": 0,
    "skipped":0,
    "rejected":0,
    "blocked":0,
    "dialect":"undefined",
    "action":"finished"
}
```

sent
```
"ping"
```

got
```
{
    "action": "pong"
}
```

sent
```
{
    "ch": ["-0:1:\n:0+0:1:o:0"],
    "rev": 1,
    "action": "submit_ot",
    "id": 3
}
```

got
```
{
    "rev":1,
    "action": "submit_ot",
    "id": 3
}
```

got
```
{"sid":1,"rev":1,"score":100,"removed":[],"errors":0,"interrupts":0,"skipped":0,"rejected":0,"blocked":0,"dialect":"undefined","action":"finished"}
```
