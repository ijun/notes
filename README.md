# Gen8 FAQ
## 在esxi里查看raid rebuild进度
 1 打开esxi的ssh服务
 2 用root登录ssh，执行 /opt/hp/hpssacli/bin/hpssacli ctrl slot=0 ld 2 show detail
 3 参考 https://kallesplayground.wordpress.com/useful-stuff/hp-smart-array-cli-commands-under-esxi/
## raid 1坏了一块硬盘怎么办
 1 先定位：从iLO的storage页面，看看哪块坏了
 2 gen8关机，用新硬盘替换旧硬盘
 3 选择重建
## raid 1坏了一块，想直接拷另外一个硬盘的文件
 1 好硬盘接外置硬盘盒
 2 外置硬盘盒接到ubuntu，可以笔记本上新装个，新一点的server版本
 3 执行 sfdisk -l ，看看有没有警告，有可能分区表会损坏
 4 直接 sfdisk /dev/sdX ，会自动用backup table，记得写回硬盘
 5 此时一般ubuntu会自动识别出raid分区；如果是dsm，还会自动识别lvm，设备为 /dev/vg1000/lv
 6 可以mount挂载了 。 参考 https://unix.stackexchange.com/questions/126553/problem-mounting-gpt-disk-partition
