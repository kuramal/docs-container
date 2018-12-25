# 资源限制-CPU

本文对Kubernetes和docker的cpu限制的参数进行了说明，并对其关系进行了总结

## Kubernetes

在k8s中对容器的资源限制是在pod.spec.containers.resources中配置，该配置中有两个字段分别为requests和limits。

```text
requests：用于k8s的容器调度，同时该参数会转换为linux系统在分配cpu时的权重
limits：用来限制该容器最大使用cpu的量
```

值：1 = 1000m， 1相当于1核，对应权重为1024，当requests为空时，默认权重为 2

## Docker

docker中cpu的参数

```text
--cpu-period        进行cpu调度时，统计的时间周期
--cpu-quota         最大使用的cpu quota，同--cpu-period关联
--cpu-rt-period     cpu realtime统计的周期                 
--cpu-rt-runtime    一个周期内使用cpu realtime的quota
--cpu-shares        cpu调度分配时的权重           
--cpus              效果同—cpu-period和 —cpu-quota搭配使用的效果相同，docker1.13后支持
--cpuset-cpus       限制容器可以使用具体哪些cpu
```

## 关联

k8s中的requests字段与docker中的--cpu-quota值对应

limits与docker中的--cpu-shares值对应

