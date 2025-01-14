Welcome to the speedtest-cli wiki!

## Python API

```python
import speedtest

servers = []
# If you want to test against a specific server
# servers = [1234]

threads = None
# If you want to use a single threaded test
# threads = 1

s = speedtest.Speedtest()
s.get_servers(servers)
s.get_best_server()
s.download(threads=threads)
s.upload(threads=threads)
s.results.share()

results_dict = s.results.dict()
```

### Units

* download - bits/s
* upload - bits/s

### To avoid `MemoryError`

```python
s.upload(pre_allocate=False)
```

### Set a mini server
```python
s = speedtest.Speedtest()
s.get_best_server(s.set_mini_server("http://speedtest.test.fr/"))
s.download()
```

### Bind source

#### v2.x

```python
source = "192.168.1.100"
s = speedtest.Speedtest(source_address=source)
s.get_best_server()
s.download()
s.upload()
```

#### v1.x
```python
source = "192.168.1.100"
speedtest.SOURCE = source
socket.socket = speedtest.bound_socket
s = speedtest.Speedtest()
s.get_best_server()
s.download()
s.upload()
```