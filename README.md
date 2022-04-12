# pepperl_fuchs

## 安装

首次要安装好cartographer_ros

然后在src下

	$ git clone https://github.com/AIRS-TJ/pepperl_fuchs.git
	
再编译

## 倍加福激光使用

### 接线通电

**a、接线：**

激光信号线： M12 接头应拧入激光传感器 LAN 接口，RJ45 接头应当接入核心控制器六口交换机任意一个;

激光电源线 ：M12 接头应当拧入传感器 POWER 接口，另一头接入合适的电源，注意，棕色线为 24+, 蓝色线为 GND（棕正蓝负）

**b、通电：**

使用DC 10-30V供电，信号线连接电脑与激光，正常情况下激光运行，PWR绿灯亮，LAN口绿灯亮，黄灯闪几下，玻璃面上显示fp字样，伴有运行噪声。

### 网络配置

**a、本机ip和子网掩码查询：**

	$ ifconfig
	
          inet 10.60.75.241  netmask 255.255.255.0  broadcast 10.60.75.255

**b、配置有线网络:**

新建一个名为pepperl的有线网络,IPV4手动设置ip和子网掩码跟本地的一样，选择此有线网络

**c、配置激光的ip：**

 注意：激光IP的配置要保证和有线网络IP在一个子网范围内，且与有线网络IP不能相同

IP:10.60.75.242; Netmask: 255.255.250.0

使用按钮调整传感器参数：

1.左侧“三角”按钮为【选择】按钮，右侧“回车”为【菜单/确定】按钮

2.分别按动【菜单/确定】按钮与【选择】按钮，调整页面至【Ethernet setup】-【Address mode】选择static;

3.分别按动【菜单/确定】按钮与【选择】按钮，调整页面至【Ethernet setup】-【IP address】将其调整为10.60.75.242;

4.分别按动【菜单/确定】按钮与【选择】按钮”，调整页面至【Ethernet setup】-【Subnet mask】将其调整为255.255.255.0;

5.对激光传感器进行断电重启，即可完成设置;

6.激光设备配置完成后需要对激光设备进行重启， 命令行进行 Ping 通测试：

	$ ping 10.60.75.242

测试通过，则说明激光设备 IP 已经配置正确;

注：激光设备配置完成后，必须对设备进行重启。

### ROS驱动

将pepperl_fuchs文件->pepperl_fuchs_r2000文件->launch文件->gui_example.launch,改成：

	<param name="scanner_ip" value="10.60.75.242"/>

运行：

	$ roslaunch pepperl_fuchs_r2000 gui_example.launch 
	
### 只用r2000 2d激光没有imu运行cartographer建图
	
	$ roslaunch cartographer_pepperl_fuchs demo_pepperl_fuchs_2d.launch
	
