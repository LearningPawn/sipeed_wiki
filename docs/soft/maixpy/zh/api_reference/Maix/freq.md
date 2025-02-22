---
title: Maix.freq
keywords: maixpy, k210, AIOT, 边缘计算
desc: maixpy  Maix.freq
---


频率模块，支持程序修改 cpu 和 kpu 频率

## 方法



### freq.set(cpu, pll1, kpu_div)

设置 cpu 或者 kpu 频率，设置完后会自动重启生效

请注意在频率设置完毕后可能会导致某些外设性能改变

```python
from Maix import freq
freq.set(cpu = 400, kpu = 400)
```

配置文件将会保存在文件系统的`/flash/freq.conf`文件下，请勿修改这个文件，如果文件不存在则会自动创建

#### 参数

不设置的参数会保持之前的值

**注意**： 如果`cpu`频率设置小于`60MHz`， 默认的`REPL`串口波特率会设置为`9600`

* `cpu`： 想要设置的cpu频率，范围[26,600]（芯片最高`800`但对电压有要求，`MaixPy`支持的系列不支持最高到`800`，默认`400`, 不同的板子可能表现不同，为了稳定性不建议过高

* `pll1`: `pll1`输出的频率，取值范围[26,1200]（芯片最高1800，MaixPy限制到1200），默认 `400`

* `kpu_div`：`kpu`时钟频率分频，取值范围[1,16]，默认`1`。 `kpu`频率=`pll1`/`kpu_div`， 比如想设置`kpu`频率为`400`，则只需设置`pll1`为`400`， `kpu_div`为`1`即可。 注意`kpu`频率范围：[26,600]

#### 返回值

如果频率没有变化，则返回空。
如果频率有变化，将会自动重启机器。在使用该接口之前请确认当前情况能能否重启


### freq.get()

获取当前设置的频率参数

#### 返回值

`cpu`频率和`kpu`的频率，一个元组的形式返回，比如`(400,400)`

### freq.get_cpu()

获取当前`cpu`的频率

#### 返回值

`cpu`频率


### freq.get_kpu()

获取当前设置的 `kpu` 频率

#### 返回值

当前`kpu`频率


