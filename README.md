# shadowsocks


标签（空格分隔）： shadowsocks

---

## Debian / Ubuntu:

```shell
apt-get install python-pip
apt-get install python-setuptools m2crypto supervisor
pip install git+https://github.com/shadowsocks/shadowsocks.git@master
ssserver -p 443 -k password -m aes-256-cfb
```

```javascript
var text;
$("#speedtest_v4 tr").each(
	function(i,item){
		var href = $(this).children('td:eq(1)').text()
		text += href+' ';
	}
)
console.log(text)
```

## 优化

- 开启`tcp_fastopen`

```shell
echo 3 > /proc/sys/net/ipv4/tcp_fastopen
```

- 创建 `/etc/sysctl.d/local.conf` 文件输入以下内容

```shell
# max open files
fs.file-max = 51200
# max read buffer
net.core.rmem_max = 67108864
# max write buffer
net.core.wmem_max = 67108864
# default read buffer
net.core.rmem_default = 65536
# default write buffer
net.core.wmem_default = 65536
# max processor input queue
net.core.netdev_max_backlog = 4096
# max backlog
net.core.somaxconn = 4096

# resist SYN flood attacks
net.ipv4.tcp_syncookies = 1
# reuse timewait sockets when safe
net.ipv4.tcp_tw_reuse = 1
# turn off fast timewait sockets recycling
net.ipv4.tcp_tw_recycle = 0
# short FIN timeout
net.ipv4.tcp_fin_timeout = 30
# short keepalive time
net.ipv4.tcp_keepalive_time = 1200
# outbound port range
net.ipv4.ip_local_port_range = 10000 65000
# max SYN backlog
net.ipv4.tcp_max_syn_backlog = 4096
# max timewait sockets held by system simultaneously
net.ipv4.tcp_max_tw_buckets = 5000
# turn on TCP Fast Open on both client and server side
net.ipv4.tcp_fastopen = 3
# TCP receive buffer
net.ipv4.tcp_rmem = 4096 87380 67108864
# TCP write buffer
net.ipv4.tcp_wmem = 4096 65536 67108864
# turn on path MTU discovery
net.ipv4.tcp_mtu_probing = 1

# for high-latency network
net.ipv4.tcp_congestion_control = hybla

# for low-latency network, use cubic instead
# net.ipv4.tcp_congestion_control = cubic
```

```
sysctl --system
ulimit -n 51200
```

## 启动
`/etc/shadowsocks.json`
```
{
    "server":"XXXX",
    "server_port":8388,
    "local_port":1080,
    "password":"XXXX",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": true
}
```

```
ssserver -c /etc/shadowsocks.json -d start
ssserver -c /etc/shadowsocks.json -d stop
```

## 参考链接

https://www.tennfy.com/1978.html
https://fatesinger.com/76137
https://yq.aliyun.com/articles/137280?commentId=11711
https://teddysun.com/486.html?spm=a2c4e.11153940.blogcont137280.15.369775c6UNNEY5
http://www.joryhe.com/2016-05-31-shadowsocks_serices_speeder_optmime.html



