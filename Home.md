Welcome to the speedtest-cli wiki!

## Python API

```python
import speedtest

servers = []
# If you want to test against a specific server
# servers = [1234]

s = speedtest.Speedtest()
s.get_servers(servers)
s.get_best_server()
s.download()
s.upload()
s.share()

results_dict = s.results.dict()
```

### Set a mini server
```
s = speedtest.Speedtest()
s.get_best_server(s.set_mini_server("http://speedtest.test.fr/"))
s.download()
```

### Bind source
```
source = "192.168.1.100"
speedtest.SOURCE = source
s = speedtest.Speedtest()
s.get_best_server()
s.download()
s.upload()
```