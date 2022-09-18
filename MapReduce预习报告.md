# MapReduce预习报告

标签（空格分隔）： 未分类

---

## 1、MapReduce的核心思想
&emsp;&emsp;MapReduce的核心思想是"分而治之"。所谓"分而治之"就是把一个复杂的问题，按照一定的"分解"方法分为大家的规模较小的若干部分，然后逐个解决，分别找出各部分的结果，把各部分的结果组成整个问题的结果。
## 2、MapReduce编程模型
&emsp;&emsp;MapReduce是一种思想或是优质编程模型。编程模型主要有两个抽象类组成，即Mapper和Reducer类，Mapper用以对切分过的原始数据进行处理，Reducer则对Mapper的结果进行汇总，得到最后的输出结果。
## 3、MapReduce数据流
### 3.1分片、格式化数据源
&emsp;&emsp;InputFormat主要有两个任务，一个是对源文件进行分片，并确定Mapper的数量;另一个是对各分片进行格式化处理成键值形式的数据流并传给Mapper。
### 3.2Map过程
&emsp;&emsp;Mapper接收&lt;key,value&gt;形式的数据，并处理成&lt;key,value&gt;形式的数据，具体的处理过程可由用户定义。在WorldCount中，Mapper会解析传过来的key值，并以1作为当前key的value值，形成&lt;word,1&gt;的形式。
### 3.3Combiner过程
&emsp;&emsp;每一个map()过程都可能会产生大量的本地输出，Combine()的作用就是对map()端的输出先做一次合并，以减少在map()和Reduce结点之间的数据传输量，提高网络I/O性能，是MapReduce的一种优化手段之一。
### 3.4Shuffle过程
&emsp;&emsp;Shuffle过程是指从Mapper产生的直接输出结果，经过一系列的处理，成为最终的Reduce 直接输入数据为止的整个过程，这一过程也是MaoReduce的核心过程。
### 3.5Reduce过程
&emsp;&emsp;Reduce接收&lt;key,{value list}&gt;形式的数据流，形成&lt;key,value&gt;形式的数据输出，输出数据直接写入HDFS，具体的处理过程可由用户定义。在WordCount中,Reducer会将相同key的value list进行累加，得到这个单词出现的总次数，然后输出。
## 4.MapReduce任务运行过程
&emsp;&emsp;MapReduce的任务流程是从客户端提交任务开始，知道任务运行结束的一些列流程。MRv2是Hadoop2中的MapReduce任务运行流程。在MRv2中，MapReduce运行时环境由Yarn提供，所以需要MapReduce相关任务和Yarn相关服务进行协同工作。
### 4.1MRv2基本组成
&emsp;&emsp;MRv2舍弃了MRV1中的JobTrack和TaskTrack，而采用一种新的MRAppMaster进行单一任务管理，并与Yarn中的ResourceManger和NodeMage协同调度与控制任务，避免了由单一服务管理和调度所有任务而产生的负载过重的问题。MRv2由客户端、MPAppMaster、Map Task 和Reduce Task。
### 4.2Yarn的基本组成
&emsp;&emsp;Yarn是一个资源管理平台，它监控和调度整个集群资源，并负责管理集群所有任务的运行和任务资源的分配，由Resource Manager和Application Manager组成。
### 4.3任务流程
&emsp;&emsp;在Yarn中，资源管理由ResourceManage和NodeManager共同完成，其中ResourceManager中的那个调度器负责资源分配，NodeManager负责资源的供给和隔离。ResourceManager将某个NodeManager上资源分配给任务h后，NodeManager需按照要求为任务提供相应的资源，并保证这些资源具有独占性，为任务运行提供基础的保证。






