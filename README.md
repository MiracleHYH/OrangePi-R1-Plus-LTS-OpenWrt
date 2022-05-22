# OrangePi-R1-Plus-LTS-OpenWrt
Modified OpenWrt for R1-Plus-LTS from official source code (OpenWrt 21.02 Kernel 5.4)
## 说明
### 硬件信息
- Xunlong Orange Pi R1 Plus LTS
  - CPU: Rockchip RK3328, 四核 ARM Cortex-A53 64 位处理器
  - GPU: Mali-450MP2, Supports OpenGL ES 1.0/2.0
  - 内存: 1GB LPDDR3（与 GPU 共享）
  - 板载以太网: 
    - 10M/100M/1000M 以太网（YT8531C）
    - 10M/100M/1000M USB 以太网（RTL8153B）
- Sandisk Tf卡 A1 Class10 32G
### 本次编译主要目的是适配
- 学校Dr.Com认证上网
- 有科学上网需求
### 删减
- docker
- 及其他不必要插件
### 新增
- [Argon主题](https://github.com/jerrykuku/luci-theme-argon)
- 科学上网[SSR-Plus](https://github.com/fw876/helloworld)
- Dr.Com客户端上网认证[dogcom](https://github.com/mchome/openwrt-dogcom)
## 编译流程
```shell
# 获取源码
git clone https://github.com/orangepi-xunlong/openwrt.git -b openwrt-21.02
cd openwrt/
git pull
# 添加插件
mkdir package/my_addons
# Dr.com C语言 OpenWrt客户端
git clone https://github.com/mchome/openwrt-dogcom.git package/my_addons/openwrt-dogcom
git clone https://github.com/mchome/luci-app-dogcom.git package/my_addons/luci-app-dogcom
# Argon主题
git clone https://github.com/jerrykuku/luci-theme-argon.git package/my_addons/luci-theme-argon
# SSR-Plus
git clone --depth=1 https://github.com/fw876/helloworld.git package/my_addons/helloworld
git -C package/my_addons/helloworld pull
# SSR-Plus 依赖
for i in "dns2socks" "microsocks" "ipt2socks" "pdnsd-alt" "redsocks2"; do \ 
  svn checkout "https://github.com/immortalwrt/packages/trunk/net/$i" "package/my_addons/helloworld/$i"; \ 
done
# 后面就是标准流程了
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make download V=s -j1
make V=s -j1
```
## 预览
![openwrt](https://user-images.githubusercontent.com/71177584/169695945-c2533e5b-5904-41bf-8bea-39e797521821.png)
![SSR-Plus](https://user-images.githubusercontent.com/71177584/169695948-f64405b3-5906-4d93-b3fb-ecfa7071b9da.png)
![dogcom](https://user-images.githubusercontent.com/71177584/169695951-701c2fd1-0ccd-443c-85db-e3dc7f84957c.png)
