---
layout: pattern
title: Async Method Invocation
folder: async-method-invocation
permalink: /patterns/async-method-invocation/
pumlid: TSdB3SCW303GLTe1mFTkunWhk0A3_4dKxTi5UdlIUuhIoCPfuz4Zjhy03EzwIlGyqjbeQR16fJL1HjuOQF362qjZbrFBnWWsTPZeFm3wHwbCZhvQ4RqMOSXIuA1_LzDctJd75m00
categories: Concurrency
tags:
 - Java
 - 中等难度
---
## 意图
异步方法调用是在等待任务结果时调用线程未被阻塞的模式。 
该模式提供多个独立任务的并行处理，并通过回调检索结果，或等待一切完成。 

## 适用性
使用异步方法调用模式时

* 您有多个可以并行运行的独立任务
* 您需要改善一组连续任务的性能
* 您的处理能力或长时间运行的任务数量有限，主任务不应该等待所有的任务完成

## 示例

* [FutureTask](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/FutureTask.html), [CompletableFuture](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletableFuture.html) and [ExecutorService](http://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html) (Java)
* [Task-based Asynchronous Pattern](https://msdn.microsoft.com/en-us/library/hh873175.aspx) (.NET)
