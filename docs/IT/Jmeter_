#### 一、Web服务器启动
```
@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody User user) {
        // 处理业务逻辑，例如保存到数据库
        // 这里简单返回传入的User对象
        System.out.println(user.toString());
        return new ResponseEntity<>(user, HttpStatus.CREATED);
}
```
#### 二、Jmeter压测流程
##### 1.创建Test Plan

##### 2.创建Thread Group
######  线程组
 添加一个“线程组” (Add > Threads (Users) > Thread Group)。

###### 配置线程组的参数：
- Number of Threads: 模拟的用户数量。
- Ramp-Up Period:所有用户完全启动所需的时间。
- Loop count:测试脚本执行次数，可以选择“Forever”来进行持续的压力测试。

###### 添加HTTP请求:
在线程组下添加一个或多个“HTTP请求” (Add > Sampler > HTTP Request)。
配置HTTP请求的URL、Method等参数。


##### 3.创建Http Request
```
Protocol=http
Server Name or IP :localhost
port Number : 8080
Http Request : POST
Paht: /api/users
```
bady data使用Jmeter内建函数创建随机数,其他还有${__time(yyyyMMhh HHmmss)}
```
{
  "id": "${__Random(1000000000000,9000000000000)}",
  "username": "${__RandomString(8,abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789,)}",
  "password": "${__RandomString(12,abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789,)}"
}
```


##### 4.创建Http Header Mannager

```
Content-Type：application/json
```
#### 三、压测和监控运行情况
##### 添加监听器:
为了监控TPS，需要添加一个监听器“Graph Results”

#### 运行测试
运行测试计划:
点击工具栏上的绿色三角形按钮开始测试。
观察测试的执行情况。


### 查看汇总报告:
在“汇总报告”中，你会看到“Samples/sec”列，这代表每秒钟处理的样本数。如果样本数等于你定义的一个事务，则此值就是TPS。
也可以关注“Throughput”列，它提供了每秒通过的请求数量，通常与TPS类似，但可能还包括其他类型的请求。
#### 查看图形结果:
在“Graph Results”监听器中，你可以查看TPS随时间变化的趋势图。
##### 0. 吞吐量 (Throughput)
> 描述:吞吐量是指系统在单位时间内处理的工作量。对于TPS图表，吞吐量代表每秒事务数。对于其他图表，吞吐量代表相应的每秒处理量。

> 用途:评估系统的处理能力。分析系统的最大吞吐量。

##### 1. 数据 (Data)
> 描述:
数据列显示了每个样本的具体测量值。
对于响应时间图表，数据列中的值代表每个样本的响应时间。
对于TPS图表，数据列中的值代表每秒事务数。
对于其他图表，数据列显示相应指标的具体值。

> 用途:
用于查看每个样本的具体测量值。
分析单个样本的表现。

##### 2. 平均值 (Average)
> 描述:平均值是指所有样本的测量值相加后的总和除以样本数量。对于响应时间图表，平均值代表所有样本响应时间的平均值。对于TPS图表，平均值代表测试期间的平均每秒事务数。对于其他图表，平均值代表相应指标的平均值。

> 用途:提供了一个整体表现的概览。评估系统的平均性能。
##### 3. 中位数 (Median)
> 描述:中位数是指将所有样本的测量值按顺序排列后位于中间位置的值。对于响应时间图表，中位数代表所有样本响应时间排序后的中间值。对于其他图表，中位数代表相应指标排序后的中间值。

> 用途:
提供了一个不受极端值影响的整体表现的概览。
评估系统的典型性能。
##### 4. 标准偏差 (Deviation)
> 描述:标准偏差是一个统计学概念，用来衡量样本测量值与平均值之间的差异程度。
对于响应时间图表，标准偏差代表所有样本响应时间与平均响应时间之间的差异程度。
对于其他图表，标准偏差代表相应指标与平均值之间的差异程度。

> 用途:评估数据的波动性。较低的标准偏差表明数据点相对集中，较高的标准偏差表明数据点分散较大。
