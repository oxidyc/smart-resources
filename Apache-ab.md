# Apache ab

##
Apache ab测试工具是模拟多线程并发请求，就是有n多请求同时向服务器发送，同时也使得ab成为某些网络攻击的工具。

## 
```tcl
Microsoft Windows [版本 10.0.17763.615]
(c) 2018 Microsoft Corporation。保留所有权利。

C:\WINDOWS\system32>
D:\Program Files\Apache24\bin>ab -n1000 -c10 http://127.0.0.1:88
ab: invalid URL
Usage: ab [options] [http://]hostname[:port]/path
Options are:
    -n requests     Number of requests to perform。用于指定压力测试总共的执行次数
    -c concurrency  Number of multiple requests to make at a time。用于指定压力测试的并发数
    -t timelimit    Seconds to max. to spend on benchmarking 等待相应的最大时间（单位：秒）
                    This implies -n 50000
    -s timeout      Seconds to max. wait for each response
                    Default is 30 seconds
    -b windowsize   Size of TCP send/receive buffer, in bytes。TCP发送/接收的缓冲大小（单位：字节）
    -B address      Address to bind to when making outgoing connections
    -p postfile     File containing data to POST. Remember also to set -T。发送POST请求时需要上传的文件，此外还必须设置-T参数。
    -u putfile      File containing data to PUT. Remember also to set -T。发送PUT请求时需要上传的文件，此外还必须设置-T参数
    -T content-type Content-type header to use for POST/PUT data, eg.
                    'application/x-www-form-urlencoded'
                    Default is 'text/plain'。用于设置content-type请求头信息
    -v verbosity    How much troubleshooting info to print。指定打印帮助信息的冗余级别
    -w              Print out results in HTML tables。以HTML表格形式打印结果
    -i              Use HEAD instead of GET。使用HEAD请求代替GET请求
    -x attributes   String to insert as table attributes。插入字符串作为table标签的属性
    -y attributes   String to insert as tr attributes。插入字符串作为tr标签的属性
    -z attributes   String to insert as td or th attributes。插入字符串作为td/th标签的属性
    -C attribute    Add cookie, eg. 'Apache=1234'. (repeatable)。添加cookie信息
    -H attribute    Add Arbitrary header line, eg. 'Accept-Encoding: gzip'
                    Inserted after all normal header lines. (repeatable) 添加任意的请求头
    -A attribute    Add Basic WWW Authentication, the attributes
                    are a colon separated username and password. 添加一个基本的网络认证信息，用户名和密码之间用英文冒号隔开
    -P attribute    Add Basic Proxy Authentication, the attributes
                    are a colon separated username and password. 添加一个基本的代理认证信息，用户名和密码之间用英文冒号隔开
    -X proxy:port   Proxyserver and port number to use 指定使用的代理服务器和端口号，例如：“10.10.10.3:88”
    -V              Print version number and exit 打印版本号并退出
    -k              Use HTTP KeepAlive feature 使用HTTP的keepAlive特性
    -d              Do not show percentiles served table. 不显示百分比
    -S              Do not show confidence estimators and warnings.  不显示预估和警告信息
    -q              Do not show progress when doing more than 150 requests
    -l              Accept variable document length (use this for dynamic pages)
    -g filename     Output collected data to gnuplot format file. 输出结果信息到gnuplot格式的文件中
    -e filename     Output CSV file with percentages served 输出结果信息到CSV格式的文件中
    -r              Don't exit on socket receive errors. 指定接收到错误信息时不退出程序
    -m method       Method name
    -h              Display usage information (this message)  显示用户信息，其实就是 ab -help

D:\Program Files\Apache24\bin>ab -n 1000 -c 10 http://localhost:88/
This is ApacheBench, Version 2.3 <$Revision: 1843412 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/
## 以上为apache的版本信息，与本次测试无关

Benchmarking localhost (be patient)
## 以上内容显示测试完成度，本次测试发起请求数量较少，完成较快，无中间过程显示。在请求数量很多时会分行显示当前完成数量。
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests


Server Software:        Jetty(9.2.13.v20150730)     ## 被测试的服务器所用的软件信息
Server Hostname:        localhost       ## 被测试主机
Server Port:            88              ## 被测试主机的服务端口号，一般http请求的默认端口号是80，https默认使用443端口
SSL/TLS Protocol:       TLSv1.2,ECDHE-RSA-AES128-GCM-SHA256,2048,128  ## 加密协议

Document Path:          /index.html       ## 请求的具体文件
Document Length:        0 bytes     ## 请求的文件index.html大小

Concurrency Level:      10      ## 并发级别，也就是并发数，请求中-c参数指定的数量
Time taken for tests:   0.186 seconds      ## 本次测试总共花费的时间
Complete requests:      1000        ## 本次测试总共发起的请求数量
Failed requests:        0       ## 失败的请求数量。因网络原因或服务器性能原因，发起的请求并不一定全部成功，通过该数值和Complete requests相除可以计算请求的失败率，作为测试结果的重要参考
Non-2xx responses:      1000        ## 
Total transferred:      281874 bytes    ## 总共传输的数据量，指的是ab从被测服务器接收到的总数据量，包括index.html的文本内容和请求头信息
HTML transferred:       22700 bytes ##从服务器接收到的index.html文件的总大小，等于Document Length*Complete requests=227 bytes*100 = 22700 bytes
Requests per second:    5376.14 [#/sec] (mean)      ## 平均（mean）每秒完成的请求数：QPS，这是一个平均值，等于Complete requests/Time taken for tests=100/0.186=5376.14
Time per request:       1.860 [ms] (mean)       ## 从用户角度看，完成一个请求所需要的时间（因用户数量不止一个，服务器完成10个请求，平均诶个用户才接受到一个完整的返回，所以该值是下一项数值的10倍）
Time per request:       0.186 [ms] (mean, across all concurrent requests)   ## 服务器完成一个请求的时间。
Transfer rate:          1479.88 [Kbytes/sec] received       ## 网络传输速度。对于大文件的请求测试，这个很容易成为系统瓶颈所在。要确定该值是不是瓶颈，需要了解客户端和被测服务器之间的网络情况，包括网络带宽和网卡速度等信息。

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.3      0       1
Processing:     0    2   0.8      2       7
Waiting:        0    1   0.8      1       7
Total:          0    2   0.8      2       7

## 这几行组成的表格主要是针对响应时间也就是第一个Time per request进行细分和统计。一个请求的响应时间可以分成网络链接（Connect），系统处理（Processing）和等待（Waiting）三个部分。表中min表示最小值； mean表示平均值；[+/-sd]表示标准差（Standard Deviation） ，也称均方差（mean square error），这个概念在中学的数学课上学过，表示数据的离散程度，数值越大表示数据越分散，系统响应时间越不稳定。 median表示中位数； max当然就是表示最大值了。

## 需要注意的是表中的Total并不等于前三行数据相加，因为前三行的数据并不是在同一个请求中采集到的，可能某个请求的网络延迟最短，但是系统处理时间又是最长的呢。所以Total是从整个请求所需要的时间的角度来统计的。这里可以看到最慢的一个请求花费了195ms，这个数据可以在下面的表中得到验证。

Percentage of the requests served within a certain time (ms)
  50%      2
  66%      2
  75%      2
  80%      2
  90%      3
  95%      3
  98%      4
  99%      5
 100%      7 (longest request)

## 这个表第一行表示有50%的请求都是在2ms内完成的，可以看到这个值是比较接近平均系统响应时间（第一个Time per request:       1.860 [ms] (mean) ）

##以此类推，90%的请求是小于等于3ms的。刚才我们看到响应时间最长的那个请求是7ms，那么显然所有请求（100%）的时间都是小于等于7毫秒的，也就是表中最后一行的数据肯定是时间最长的那个请求（longest request）。
```
> ab -n1000 -c100 http://127.0.0.1:88
说明
- -n1000：请求数1000个
- -c100： 并发数100



## Resources

- https://www.cnblogs.com/gumuzi/p/5617232.html
- https://www.cnblogs.com/leaf930814/p/6666290.html
- https://www.cnblogs.com/zengxiangzhan/archive/2012/12/07/2807141.html
- https://www.cnblogs.com/nulige/p/9370063.html