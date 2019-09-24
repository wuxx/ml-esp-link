# ml-esp-link 无线串口/烧录工具 用户手册
* [产品介绍](#产品介绍) 
* [产品特点](#产品特点)
* [使用场景](#使用场景)
* [使用步骤](#使用步骤)
* [LED状态](#led状态)
* [产品链接](#产品链接)
* [FAQ](#faq)
    * [在Keil中如何生成bin文件？](#q-在keil中如何生成bin文件)
    * [当前支持哪些目标芯片的无线烧录？](#q-当前支持哪些目标芯片的无线烧录)
    
# 产品介绍
ml-esp-link 是缪斯实验室推出的基于esp-link深度定制的的无线串口/烧录工具，使用wifi进行无线通信，信号稳定，数据包可靠传输。用户无需额外采购发射机/接收机，亦无需配对，仅一个ml-esp-link即可实现无线串口。ml-esp-link可工作在AP或者STA模式下，可使用PC或者手机通过网页浏览器进行配置，简单方便。ml-esp-link可实现最高波特率为460800的串口传输，且支持无线脱机烧录，用户只需将编译出的bin文件通过网页上传，即可将固件烧录至目标单板中，可有效提高产品的开发效率。
![ml-esp-link](https://github.com/wuxx/ml-esp-link/blob/master/doc/ml_esp_link.png)
# 产品特点
- 使用方便，只需将一个串口工具与目标板相连，PC侧打开串口软件，即可开始开发调试工作
- 通过web页面进行配置工作，使用PC或者手机打开浏览器即可进行配置
- 支持最高波特率为460800的无线串口传输
- 支持无线脱机烧录，和目标单板通过SWD接口连接，可用PC或者手机直接打开浏览器上传固件进行升级，当前支持stm32f0x全系列和stm32f1x全系列的芯片无线烧录
- 支持固件升级，更多新功能将会陆续支持


# 使用场景
1. 用于调试飞行器，小车，机器人，由于调试目标为通常处于移动状态，此时使用传统有线调试器下载、调试较为困难
2. 目标板已经组装好外壳，成为产品形态，此时传统的有线方式不便下载调试
3. 产品安装在高处，如路灯、高塔等位置，此时使用有线方式不便下载调试
4. 目标板带有强电，若使用有线方式和PC相连，则存在将PC USB口烧毁的风险，使用无线下载可规避此风险
4. 若产品已交付给客户，而后续需要进行固件更新，客户无需安装额外烧录软件，只需打开浏览器，将固件直接上传即可实现升级


# 使用步骤
1. 将ml-esp-link和目标单板相接并上电，若为首次上电，ml-esp-link会处于AP模式，此时打开wifi，可发现一个AP热点，名称为ESP_XXXXXX，如下图  
![ap_name](https://github.com/wuxx/ml-esp-link/blob/master/doc/ap_name.png)
2. 此热点无需输入密码，连接此wifi，连接成功后，在浏览器中输入IP地址 192.168.4.1并回车即可进入ml-esp-link主界面  
![main_page1](https://github.com/wuxx/ml-esp-link/blob/master/doc/main_page1.png)
3. 推荐以STA模式使用ml-esp-link，若以AP模式使用，则可直接跳过步骤4、5、6  
4. 切换到wifi station 菜单，将ml-esp-link切换到STA+AP模式  
![wifi_station1](https://github.com/wuxx/ml-esp-link/blob/master/doc/wifi_station1.png)
5. 连接到本地的wifi路由器，连接成功后，会出现本地路由器分配的新的IP地址  
![wifi_station2](https://github.com/wuxx/ml-esp-link/blob/master/doc/wifi_station2.png)
![wifi_station3](https://github.com/wuxx/ml-esp-link/blob/master/doc/wifi_station3.png)
6. 本地断开ESP_XXXXXX wifi热点，连接到wifi路由器，重新使用新的IP打开ml-esp-link  
![main_page2](https://github.com/wuxx/ml-esp-link/blob/master/doc/main_page2.png)
7. 连接成功后，即可开始正常使用，PC侧打开串口工具，推荐使用sscom、putty。打开ml-esp-link的23端口，即可开始正常使用无线串口，也可在网页上的MCU UART菜单中直接使用  
![sscom](https://github.com/wuxx/ml-esp-link/blob/master/doc/sscom.png)  
在网页端也可以直接使用串口
![mcu_uart](https://github.com/wuxx/ml-esp-link/blob/master/doc/mcu_uart.png)  
5. 若需要无线烧录，操作也同样简单，只需上传bin文件（当前只支持bin文件烧录，将来会支持hex文件烧录，如何将hex文件转换成bin文件请见FAQ），点击 flash the target，观察网页提示，即可正常烧录  
可检查IDCODE是否正确来判断目标单板是否已经正常连接。
![mcu_flash](https://github.com/wuxx/ml-esp-link/blob/master/doc/mcu_flash.png)

# LED状态
ml-esp-link上有两个led，标记为CON（绿色）和SER（蓝色），分别用来指示WiFi连接状态和串口数据传输状态  

LED | 说明
---|---
绿灯1秒闪烁一次 | 当前处于AP+STA模式，正在尝试连接网络
绿灯2秒闪烁一次 | 当前处于AP模式，未连接网络
绿灯3秒闪烁一次 | 当前处于AP+STA模式，网络已连接
蓝灯闪烁 | 串口正在发送/接收数据

# 产品链接
[ml-esp-link无线串口/烧录工具](https://item.taobao.com/item.htm?spm=a1z10.1-c-s.w4004-21349689053.3.4f8d20f8MryK8Q&id=596673065140)

# FAQ
### Q: 在Keil中如何生成bin文件？  
在编译自定义脚本中添加一行
```
fromelf --bin -o "$L@L.bin" "$L@L.axf"
```
即可在生成hex的同时生成bin文件，如下所示
![keil_bin](https://github.com/wuxx/ml-esp-link/blob/master/doc/keil_bin.png)

### Q: 当前支持哪些目标芯片的无线烧录？
当前支持STM32F0x和STM32F1x系列的所有芯片的烧录，以及STM32F4x系列部分芯片的烧录，将来会不断开发，增加更多平台的支持，可将您的平台告知我们，我们可优先为您的平台适配。

有任何问题或者建议，请在本仓库的[Issues](https://github.com/wuxx/ml-esp-link/issues)页面中提出，我们会持续跟进解决。
