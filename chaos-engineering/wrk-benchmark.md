# wrk
wrk is a modern HTTP benchmarking tool capable of generating significant load when run on a single multi-core CPU. It combines a multithreaded design with scalable event notification systems such as epoll and kqueue.  
* Basic Usage
```
wrk -t12 -c400 -d30s http://127.0.0.1:8080/index.html
```
This runs a benchmark for 30 seconds, using 12 threads, and keeping 400 HTTP connections open.  
Output:
```
Running 30s test @ http://127.0.0.1:8080/index.html
  12 threads and 400 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   635.91us    0.89ms  12.92ms   93.69%
    Req/Sec    56.20k     8.07k   62.00k    86.54%
  22464657 requests in 30.00s, 17.76GB read
Requests/sec: 748868.53
Transfer/sec:    606.33MB
```
The machine running wrk must have a sufficient number of ephemeral ports available and closed sockets should be recycled quickly. To handle the initial connection burst the server's listen(2) backlog should be greater than the number of concurrent connections being tested.  
* Here is wrk [github](https://github.com/wg/wrk) page.  

---
