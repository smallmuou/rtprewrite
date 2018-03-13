# rtprewrite

rtprewrite类似于tcprewrite，可修改包的源、目的IP及MAC，用于重放rtp数据，方便在vlc等媒体播放器上进行播放。

## 安装
请先安装tcprewrite、wireshark软件包

```bash
yum install -y tcprewrite
yum install -y wireshark
```

```bash
git clone https://github.com/smallmuou/rtprewrite.git
cd rtprewrite
sudo cp rtprewrite /usr/local/bin
```

## 使用

```bash
rtprewrite -a PCMU/8000 192.168.12.102 in.pcap
rtprewrite -v H264/90000 192.168.12.102 in.pcap
rtprewrite -v 96:H264/90000 192.168.12.102 in.pcap
```

## RTP包重放全过程

1. 抓包，可以使用tcpdump或wireshark
2. 过滤包，去除不要的包，确保不掺杂其他包
3. 使用rtprewrite重写
4. 保存rtprewrite输出的sdp
5. 执行`tcpreplay --intf1=ens33 'output.pcap'`，并在目的主机播放sdp文件
