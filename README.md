# BD-Upload
Automatic Blu-ray Disk Upload Toolkit  

A Script used for scanning BDinfo and take screenshots for BDISO or BDMV on Linux  
Note that UltraHD Blu-ray is not supported yet  

转发蓝光原盘（不支持 UHD）时可以使用的一个脚本，支持对 BDISO,BDMV 扫描 BDinfo、截图、生成缩略图、重新制作种子  
  

### Installation

Dedicated Server or VPS  
```
wget -qO /usr/local/bin/bdupload https://github.com/Aniverse/bdupload/raw/master/bdupload
chmod +x bdupload
```

Shared Seedbox with SSH access  
```
cd ; git clone https://github.com/Aniverse/bdupload
echo "PATH=~/bdupload:$PATH" > ~/.bashrc ; PATH=~/bdupload:$PATH
```

### Guide

![检查是否缺少软件](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.01.png)

一开始脚本会检查是否缺少脚本需要用到的软件；如有缺少，你可以选择
1. 用 root 权限安装所需软件  
2. 无需 root 权限，使用脚本内置的软件库来继续运行  

![正常运行界面](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.02.png)

注意：路径里即使带空格也不需要双引号  

目前可以实现以下功能：  

- **判断是 BDISO 还是 BDMV**  
输入一个**完整的路径**，若该路径是文件夹且内含名为 BDMV 的文件夹的话则认为该资源是 BDMV
不是文件夹且文件扩展名是 ISO 的则认为是 BDISO（但事实上 DVDISO 也会被认为是 BDISO）  

- **自动挂载镜像**  
如果是 BDISO，会挂载成 BDMV，并问你是否需要对这个挂载生成的文件夹重命名（有时候 BDISO 的标题就是 DISC1 之类的，重命名下可能更好）  
全部操作完成后 BDISO 会自动解除挂载  

- **截图**  
自动寻找 BD 里体积最大的 m2ts 截 10 张 png 图。默认用 1920x1080 的分辨率，也可以手动填写分辨率  
指定 1920×1080 分辨率是因为某些原盘用 ffmepg 直接截图的话截出来的图是 1440 ×1080 的，不符合某些站的要求  
自定义分辨率主要是考虑到有些原盘的分辨率不是 1920x1080 （有些蓝光原盘甚至是 480i ）  

- **扫描 BDinfo**  
默认是自动扫描第一个最长的 mpls；也可以手动选择扫描哪一个 mpls  
BDinfo 会输出三个报告，一个是原版的，一个是 Main Summary，一个是 Quick Summary  
一般而言发种写个 Quick Summary 就差不多了  

- **生成缩略图**  
这个功能默认不启用；其实一般也用不上；用内置库运行可能会卡住  

- **制作种子**  
针对 BDISO，默认选择重新制作种子；针对 BDMV，默认选择不重新制作种子 

![输出结果](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.03.png)

![h5ai](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.04.png)
安装了 `h5ai` 的话可以在网页上预览、下载生成的截图、BDinfo、种子  





### To Do List

- **自动上传到 Google Drive**  
调用 rclone 来完成，需要你自己设置好 rclone，且在脚本里设置 rclone remote path  
（我会把这个设置项放在脚本开头的注释里）  

### Under Consideration

- **判断操作是否成功**  
目前操作中哪一步翻车了也不会有翻车了的提醒  
- **自动检测分辨率**  
自动使用 AR 后的分辨率  
- **自动上传到 ptpimg**  
调用 ptpimg_uploader 来完成，脚本跑完后会输出 ptpimg 的链接。运行之前你需要自己配置好 ptpimg_uploader  