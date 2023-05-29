# Informer机制

## 什么是Informer机制？

一种降低Kubernetes各组件跟ETCD和APIServer通信压力的机制。

Kubernetes 中使用 http 进行通信，如何不依赖中间件的情况下保证消息的实时性，可靠性和顺序性等呢？

答案就是利用了 Informer 机制。Informer 的机制，降低了了 Kubernetes 各个组件跟 Etcd 与 Kubernetes API Server 的通信压力。



> 暂时记住一点
>
> Kubernetes使用Informer机制来解决组件通信压力，核心是一个DeltaFIFO以及一个Indexer存储。



## Informer机制架构设计



<img src="https://cqlwm-typora.oss-cn-chengdu.aliyuncs.com/img/202201112305086.png" style="zoom: 67%;" /> 

图片来源：https://github.com/kubernetes/sample-controller/blob/master/docs/controller-client-go.md

图中黄色部分需要由用户自己实现，而其余部分功能由client-go提供。



1. **Reflector**：用于 Watch 指定的 Kubernetes 资源，当 watch 的资源发生变化时，触发变更的事件，比如 Added，Updated 和 Deleted 事件，并将资源对象存放到本地缓存 DeltaFIFO；
2. **DeltaFIFO**：拆开理解，FIFO 就是一个队列，拥有队列基本方法（ADD，UPDATE，DELETE，LIST，POP，CLOSE 等），Delta 是一个资源对象存储，保存存储对象的消费类型，比如 Added，Updated，Deleted，Sync 等；
3. **Indexer**：Client-go 用来存储资源对象并自带索引功能的本地存储，Reflector 从 DeltaFIFO 中将消费出来的资源对象存储到 Indexer，Indexer 与 Etcd 集群中的数据完全保持一致。从而 client-go 可以本地读取，减少 Kubernetes API 和 Etcd 集群的压力。



> **DeltaFIFO**
>
> FIFO是一种先进先出的队列数据结构，生产者是Reflector，消费者是Pop。Deltas是Pod的单位，Delta是该Pod的某阶段的变更状态。我们可以将Delta理解为变更。

## 参考


深入了解 Kubernetes Informer

https://cloudnative.to/blog/client-go-informer-source-code/

DeltaFIFO

https://www.qikqiak.com/k8strain/k8s-code/client-go/deltafifo/



