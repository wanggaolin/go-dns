## go-dns 
###轻量级GO DNS服务

### 特点
* 支持域名劫持(自定义域名&支持自动热加载)
* 支持域名缓存
* 支持并发限制
* 支持域名转发(上层dns越多越好，随机打散请求)

### 配置文件
| Key                | Value              |Describe                 |
|  ----------        | :-----------:      |   :-----------:         |                    
| HOST               | 0.0.0.0            |   监听地址                |
| PORT               | 53                 |   监听端口                |
| MIN_CACHE          | 10                 |   最小缓存ttl，如果ttl小于(MIN_CACHE),按照MIN_CACHE缓存 |
| LOG_LEVEL          | info               |   日志等级/info/debug/...../error |
| LOG_FILE           | go-dns.log         |   日志文件                |
| MAX_PROCEED        | 20000              |   dns请求并发限制          |
| RECORD_FILE        | record.txt         |   劫持域名解析记录文本      |
| FORWARDERS/TIMEOUT | 3                  |   转发上层dns超时时间(秒)   |
| FORWARDERS/DNS     | 223.5.5.5          |   转发上层dns             |

### 使用(启动服务)
```shell
git clone https://github.com/wanggaolin/go-dns.git
cd go-dns/bin
./go-dns -f config.yaml
```

### 测试
```shell
[root@local-test ~]# dig @127.0.0.1 baidu.com

; <<>> DiG 9.10.6 <<>> @127.0.0.1 baidu.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 9017
;; flags: qr rd; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;baidu.com.			IN	A

;; ANSWER SECTION:
baidu.com.		600	IN	A	192.168.1.1
baidu.com.		600	IN	A	192.158.1.2

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Wed Mar 30 19:04:02 CST 2022
;; MSG SIZE  rcvd: 70

[root@local-test ~]#
```
