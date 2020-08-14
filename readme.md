## A Golang Port Scanner from scratch, using TDD
This is a simple **port scanner** that is able to map a large range of protocols. Using good design patterns for concurrency, like **fan-in/fan-out**, fixtures, goldenfiles and test helpers for tests, we create nice unit tests and acquire good performance in scanning process. All pakcages are covered by **TDD**, even when using tcp protocol for tests.

* **UDP isn't implemented yet**

* **Build**
```sh
$ go build -v
```

* **Usage**
```sh
$ ./portscanner -h
Usage of ./portscanner:
  -end int
        -end is the end of port range (default 80)
  -host string
        -host is the target host to be scaned (default "127.0.0.1")
  -proto string
        -proto is the protocol used - tcp or udp (default "tcp")
  -start int
        -start is the start of port range (default 1)
  -t int
        -t is the value of connection timeout used (default 100)
  -workers int
        -workers is the number of concurrent process (default 1)
```

```sh
$ ./portscanner -host localhost -t 100 -end 10000 | grep open
135      <unknown>   open
445      samba       open
5040     <unknown>   open
5432     <unknown>   open
7680     <unknown>   open
```

```sh
$ ./portscanner -host www.google.com -t 100 -end 80
Generating report
................................................................................

Port     Service    Status
------   --------   ------
1                   closed
2                   closed
...
80       http       open
```