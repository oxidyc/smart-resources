# DNS(Domain Name System)

## List
|   DNS服务商  |     主DNS      |    备用DNS    |     备注          | 
|---------    |---------    |---------    |---------    |
| IBM              | `9.9.9.9`、 `2620:fe::fe`                    | `149.112.112.112`、 `2620:fe::9`   |  IBM、Global Cyber Alliance和 Packet Clearing House三家联合推出的公共DNS  https://www.quad9.net   |
| Google          | `8.8.8.8`、 `2001:4860:4860:8888`   | `8.8.4.4`、 `2001:4860:4860:8844` | 2009年12月3日左右发布的 https://developers.google.com/speed/public-dns/ |
| Cloudflare     | `1.1.1.1`、 `2606:4700:4700::1111` 、 `2001:2001::` | `1.0.0.1`、 `2606:4700:4700::1001`、 `2001:2001:2001::` | 2018年4月1日，Cloudflare联合APNIC(亚太互联网信息中心，负责全亚太地区的IP地址分配的机构，全世界有5个这种机构)推出的公共DNS服务。https://1dot1dot1dot1.cloudflare-dns.com/ |
| AliDNS         | `223.5.5.5   `                               | `223.6.6.6`                                | 2014年6月6日上线 http://www.alidns.com/ |
| Baidu           | `180.76.76.76`、 `2400:da00::6666` |                                              | 2014年12月8日上线 http://dudns.baidu.com/intro/publicdns/ |
| 腾讯DNSPod | `119.29.29.29`                            |                                              | https://www.dnspod.cn/Products/Public.DNS |
| 114DNS       | `114.114.114.114`                       | `114.114.115.115`                    |  2010年 http://www.114dns.com |
| OpenDNS(Cisco) | `208.67.222.222` 、 `2620:119:35::35`                  | `208.67.220.220`、 `2620:119:53::53`                      | 2006年7月 https://www.opendns.com |
| DSDNS       | `1.2.4.8`                                       | `210.2.4.8`                               | 官方机构CNNIC(中国互联网中心)运营的公共DNS，比较低调。 http://public.sdns.cn |


## Resource
- https://www.dnsperf.com/