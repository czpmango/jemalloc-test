# jemalloc 内存统计对 nebula 性能的影响测试

*该测试的目的是衡量 `https://github.com/vesoft-inc/nebula-graph/pull/1116` 的可行性及性能影响*

*本测试提供两种测试方法(单条语句重复执行测平均时延以及 jmeter 压力测试)，对 jemalloc 编译选项以及内存统计函数开销进行测试*

目录说明
  - jtl/jtl-disable-stats  jemalloc 用 --disable-stats 编译压力测试结果
  - jtl/jtl-enable-stats  jemalloc 用 --enable-stats 编译压力测试结果
  - jtl/jtl-epoch-m-m  jemalloc 用 --enable-stats 编译并且加入 epoch 内存统计信息收集压力测试结果  (统计间隔/大query判定:max/max)
  - jtl/jtl-epoch-10-100  jemalloc 用 --enable-stats 编译并且加入 epoch 内存统计信息收集压力测试结果  (统计间隔/大query判定:10ms/100ms)
  - jemalloc-stats-test.md 压力测试结果整理文档
  - conf 本测试使用到的一些配置文件模版
  - script/statistics.py python 工具脚本，用于从 jtl 文件解析测试结果

本测试参考的链接
 - 测试数据集(ldbc sf1) : https://github.com/ldbc
 - 数据导入 : https://github.com/vesoft-inc/nebula-importer.git
 - nebula 压力测试框架 : https://github.com/vesoft-inc/nebula-bench
 - nebula console : https://github.com/vesoft-inc/nebula-console (方法二用了 nebula-console 提供的 Local Command `:repeat N`)
 - jemalloc 源码编译 : https://github.com/jemalloc/jemalloc.git
 - jemalloc 文档 : http://jemalloc.net/jemalloc.3.html
 - jemalloc issue : https://github.com/jemalloc/jemalloc/issues/2077
 - jmeter : https://github.com/apache/jmeter.git