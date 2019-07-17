# Honest profiler vs Async profiler

|   | Honest profiler Async profiler  |   |
| ------------ | ------------ | ------------ |
| 应用项目  |  java |   |
|  数据采样范围 | java  |  Java + native, JVM and even kernel函数 |
| 数据采集方式  |  · java agent $java -agentpath:/path/to/location/liblagent.so=interval=7,logPath=/path/to/output/log.hpl· 提供tcp接口启停agent，且可以实现动态的调整采样的参数 echo command param - nc host port [数据收集到本地文件，路径通过logPath指定]· java agent $ java -agentpath:/path/to/libasyncProfiler.so=start,svg,file=profile.svg | · command: profile.sh 可以控制采集数据的启停时间点或者采集时长  |
|   数据格式 | type data  | 直接生成svg文件，无法持续收集数据  |
|  火焰图生成 |  步骤 1.honestprofiler : 生成hpl文件； 2.stackcollapse-hpl：解析hpl文件成folded stacks; 3.flamegraph : create svg from folded stacks [最新代码里提供dump-flamegraph] |   直接生成svg |
|  GUI | 有，单机版的小工具  | 无  |
| 容器内使用  | https://hub.docker.com/r/sscaling/java-flamegraph  |   |
| 火焰图demo  |   |   |
| 局限性  |  [https://github.com/jvm-profiling-tools/honest-profiler/wiki/AsyncGetCallTrace-errors-and-what-they-mean] [It has workarounds for annoying AsyncGetCallTrace bugs. Async-profiler can show correct stack traces in the cases when other tools just fail with "AGCT::Unknown Java[ERR=-5]"] |   |
