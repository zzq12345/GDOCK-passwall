* check_data_file_clashes: Package libgd-full wants to install file /home/zzq/x64/lede/build_dir/target-x86_64_musl/root-x86/usr/lib/libgd.so
	But that file is already provided by package  * libgd
 * check_data_file_clashes: Package libgd-full wants to install file /home/zzq/x64/lede/build_dir/target-x86_64_musl/root-x86/usr/lib/libgd.so.3
	But that file is already provided by package  * libgd
 * check_data_file_clashes: Package libgd-full wants to install file /home/zzq/x64/lede/build_dir/target-x86_64_musl/root-x86/usr/lib/libgd.so.3.0.8
	But that file is already provided by package  * libgd
 * opkg_install_cmd: Cannot install package libgd-full.
 * check_data_file_clashes: Package libgd-full wants to install file /home/zzq/x64/lede/build_dir/target-x86_64_musl/root-x86/usr/lib/libgd.so
	But that file is already provided by package  * libgd
 * check_data_file_clashes: Package libgd-full wants to install file /home/zzq/x64/lede/build_dir/target-x86_64_musl/root-x86/usr/lib/libgd.so.3
	But that file is already provided by package  * libgd
 * check_data_file_clashes: Package libgd-full wants to install file /home/zzq/x64/lede/build_dir/target-x86_64_musl/root-x86/usr/lib/libgd.so.3.0.8
	But that file is already provided by package  * libgd
 * opkg_install_cmd: Cannot install package php7-mod-gd.


# GDOCK
自动从lean的lede源码clone并生成竞斗云、newifi3和x86-64位固件

我把原作者的代码(https://github.com/ljk4160/GDOCK) 进行了部分修改：
##### 1. 添加了build-newifi3.yml文件，并且在build-newifi3.yml文件中增加了下面的代码

\- name: Clone passwall code

      run: |
        cd lede/package &&  git clone https://github.com/Lienol/openwrt-package.git

  用来把passwall的源代码，下载到package目录下。

##### 2. 添加了newifi3.config、banner-newifi3、diy-newifi3三个文件。
   newifi3.config是编译用的.config文件，在这个文件中也增加了下面的代码
```
CONFIG_PACKAGE_luci-app-passwall=y

#

# Configuration

#

CONFIG_PACKAGE_luci-app-passwall_INCLUDE_ipt2socks=y

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_Shadowsocks is not set

CONFIG_PACKAGE_luci-app-passwall_INCLUDE_ShadowsocksR=y

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_Shadowsocks_socks is not set

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_ShadowsocksR_socks is not set

CONFIG_PACKAGE_luci-app-passwall_INCLUDE_V2ray=y

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_Trojan is not set

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_Brook is not set

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_kcptun is not set

CONFIG_PACKAGE_luci-app-passwall_INCLUDE_haproxy=y

CONFIG_PACKAGE_luci-app-passwall_INCLUDE_ChinaDNS_NG=y

CONFIG_PACKAGE_luci-app-passwall_INCLUDE_pdnsd=y

# CONFIG_PACKAGE_luci-app-passwall_INCLUDE_dns2socks is not set

# CONFIG_PACKAGE_luci-app-polipo is not set
```
  用来把passwall编译到固件中。（这段代码是在本地编译环境中，用make menuconfig 命令生成的）


---


*将本项目fork到自己账号下,进行以下操作即可得到专属定制固件*

1.diy.sh
可以编辑自定义和修改的脚本,可以直接修改JK预留的脚本,也可以自己编写

2.gdockfull128.config
编辑自定义配置文件.

3.以上修改完后push一下,即可自动编译固件，就是把yml文件中

```
on:
     release:
       types: [published]
     # push:  
     #   branches:
     #     - master



上面3行的 # 都删除，就开始编译了。
```

如果你只想使用固件,可以在本项目的actions下下载最新编译的固件.

==============================================

![](/screenshots/r619ac1.png)

==============================================

部分脚本内容参考以下项目特此感谢:
https://github.com/P3TERX/Actions-OpenWrt/
