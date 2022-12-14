# Thinkpad E14 for Monterey
在ThinkPad E14 i5 10th 上用 OpenCore 引导安装 Mac OS，驱动相关硬件

## 配置
|  规格 | 型号  |
| ------------- | ------------- |
| CPU | Intel  i5-10210U |
| 主板 | Intel 400 series |
| 内存 | 威刚 32 GB 2667 MHz DDR4 |
| 硬盘 | 256G（NVME）+ 2T（SATA）|
| 显卡 | Intel UHD 620 |
| 网卡 | dw 1820a（无线）+  RTL8111（有线）|

| 软件 | 版本 |
| ------------- | ------------- |
| OpenCore | 0.84 |
| Mac OS | Monterey 12.4 |

## 已驱动
+ CPU变频
+ 显卡 、 HDMI输出
+ USB、触摸板
+ 电池信息
+ 网卡、蓝牙
+ 摄像头
+ 声卡

## 未解决
~~+ 睡眠唤醒后触摸板和USB有时候不正常~~

~~+ 系统默认S3睡眠，改成S0就可以正常睡眠唤醒，就是耗电一点，数据存在内存里~~
```
sudo pmset -a hibernatemode 0
sudo pmset -a proximitywake 0
sudo pmset -a standbydelayhigh 0
sudo pmset -a ttyskeepawake 0   
sudo pmset -a gpuswitch 0    
sudo pmset -a halfdim 0  
sudo pmset -a womp 0      
sudo pmset -a acwake 0
sudo pmset -a networkoversleep 0
sudo pmset -a tcpkeepalive 0
```
插上电源开机会出现```_Q24```报错，不接电源用电池没问题，打印日志发现是```GBST```有问题，具体原因未知，所以把```_Q24```里面的```Notify```去掉，这样唤醒后不正常，所以禁用睡眠
```
            Method (_Q24, 0, NotSerialized)  // _Qxx: EC Query, xx=0x00-0xFF
            {
                CLPM ()
                Notify (BAT0, 0x80) // Status Change
            }
```
```
sudo pmset -a sleep 0
sudo pmset -a disablesleep 1
```

## 截图
![](https://github.com/pangzhen/ThinkPad-E14-Hackintosh/blob/main/PNG/system.png)

