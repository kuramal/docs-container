---
description: kube-proxy config 参数
---

# kube-proxy config

## clusterCIDR（--cluster-cidr）

该参数在kube-proxy生成iptable规则的时候，会生成如下规则

example：--cluster-cidr=10.254.0.0/16

```
0  0 KUBE-MARK-MASQ tcp  --  *  *  !10.254.0.0/16  10.254.178.99  /* default/tt: cluster IP */ tcp dpt:80
```

该规则的作用，将目的地址是10.254.178.99\(service ip\)，且源地址非10.254.0.0/16的流量标记MASQ，之后该流量会被SNAT。

