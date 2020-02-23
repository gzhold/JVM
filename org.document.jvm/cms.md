
CMS的trade-off
优势：
低延迟，垃圾回收过程并发执行

劣势：
1 内存碎片问题
2 需要预留空间，用来分配收集阶段产生的"浮动垃圾"。
3 使用更多的CPU资源


CMS 垃圾回收器分为四个阶段：
1. 初始标记
2. 并发标记
3. 重新标记
4. 并发清除


CMS中都有哪些停顿（STW）
1. 初始标记，这部分的停顿时间较短；
2. Minor GC，在预处理阶段对年轻代的回收，停顿由年轻代确定；
3. 重新标记，由于preclean 阶段的介入，这部分停顿也较短；
4. Serial-Old 收集老年代的停顿，主要发生在预留空间不足的情况下，时间会持续较长；
5. Full GC，永久代空间耗尽时的操作，由于会有整理阶段，持续时间较长。

参数配置
-XX:+CMSScavengeBeforeRemark 进入重新标记之前强制进行一次minor gc。
-XX:CMSInitiatingOccupancyFraction=70% (老年代达到70%比例，触发gc)
-XX:+UseCMSInitiatingOccupancyOnly


