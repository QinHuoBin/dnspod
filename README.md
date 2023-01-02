# 更新说明
首先感谢原作者共享的代码，由于原来的代码不支持Python3，在此fork后进行适配，以及添加一些使用笔记。
原地址:https://github.com/migege/dnspod.git

```
Change: 适配Python3
Change: 日志现在会同时打印并保存到文件中
Change: IP没有发生变化时打印提示
Fix: 修复GetIP方法超时的问题
```

# dnspod.py

```
@author migege
@version 0.0.2
```

dnspod.py 是基于 [DNSPod](http://www.dnspod.cn/docs/records.html#dns) 服务的动态 DNS 脚本，用于检测 IP 变化并更新至 DNSPod，支持多域名解析。支持 Linux 设备，包括树莓派（[Raspberry Pi](https://www.raspberrypi.org/)）。

# Prerequisites

1. python
1. pyyaml
1. requests

python 的模块可通过 ```pip install``` 命令安装。如果未安装 [pip](https://pip.pypa.io/)，请先安装 pip。

# Installation

安装 [git](https://git-scm.com/) 客户端，通过本命令获取 dnspod.py

<pre>
git clone https://github.com/migege/dnspod.git dnspod
</pre>

然后到 dnspod 目录下新建 ```conf.yaml``` 文件，根据您的 DNSPod 设置，填入以下内容：

<pre>
token: &lt;your_api_token&gt;
sub_domains:
  &lt;your_first_sub_domain_name&gt;:
    domain_id: &lt;your_domain_id&gt;
    record_id: &lt;your_record_id&gt;
  &lt;your_second_sub_domain_name&gt;:
    domain_id: &lt;your_domain_id&gt;
    record_id: &lt;your_record_id&gt;
</pre>

最后设置 crontab 定时任务

<pre>
*/10 * * * * cd &lt;path_to_dnspod&gt;; /usr/bin/python dnspod.py conf.yaml &gt; /dev/null 2&gt;&1 &
</pre>

# Tips

1. */10 表示每 10 分钟执行一次 dnspod.py
1. 如果 python 可执行路径不是 /usr/bin/python，请自行替换
1. 获取domain_id与record_id请参阅[DNSPod 如何查看域名解析的 domain_id 和 record_id](https://migege.com/post/dnspod-api-domain_id-record-id)
1. api_token的组成是 `token_ID,token`，例如`888888,123456789abcdef`
