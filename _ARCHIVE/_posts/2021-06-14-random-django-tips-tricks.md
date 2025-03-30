


1. In Django, localhost and 127.0.0.1 are viewed as entirely separate domains. This can cause all sorts of problems if you start routing between them in requests - for example, you'll have a different session token in 127.0.0.1 than localhost. Be careful!