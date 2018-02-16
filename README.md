# BD-Upload
> Automatic Blu-ray Disk Upload Toolkit  
> A Script used for scanning BDinfo and take screenshots for BDISO or BDMV on Linux  

转发蓝光原盘（不支持 UHD）时可以使用的一个脚本  
支持对 BDISO 或 BDMV 进行如下操作：扫描 BDinfo、截图、生成缩略图、重新制作种子  

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
3. 退出  

![询问选项](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.02.png)

注意：路径里即使带空格也不需要双引号  

目前可以实现以下功能：  

- **判断是 BDISO 还是 BDMV**  
输入一个**完整的路径**，若该路径是文件夹且内含名为 BDMV 的文件夹的话则认为该资源是 BDMV  
不是文件夹且文件扩展名是 ISO 的则认为是 BDISO（但事实上 DVDISO 也会被认为是 BDISO）  

- **自动挂载镜像**  
本操作需要用 root 权限执行 mount 命令，如无 root 权限则无法使用  
如果是 BDISO，会挂载成 BDMV，并问你是否需要对这个挂载生成的文件夹重命名  
（有时候 BDISO 的标题就是 DISC1 之类的，重命名下可能更好）  
全部操作完成后会自动解除挂载对 ISO 的挂载  

- **截图**  
自动寻找 BD 里体积最大的 m2ts 截 10 张 png 图，可以自定义截图分辨率  
由于某些 BD 的实际显示分辨率和原始分辨率不一样，因此脚本对分辨率做了计算，默认使用 DAR 的分辨率  

- **扫描 BDinfo**  
默认是自动扫描第一个最长的 mpls；也可以手动选择扫描哪一个 mpls  
BDinfo 会输出三个报告，一个是原版的，一个是 Main Summary，一个是 Quick Summary  
一般而言发种写个 Quick Summary 就差不多了  

- **生成缩略图**  
这个功能默认不启用；其实一般也不太用得上  

- **制作种子**  
针对 BDISO，默认选择重新制作种子；针对 BDMV，默认选择不重新制作种子  

- **使用 rclone 同步文件**  
需要你自己设置好 rclone，且在脚本里设置好 rclone remote path 才能使用（不然不会有这个选项出现）  

![正常运行](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.03.png)

脚本运行中 ...  

![输出结果](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.04.png)

如果选择扫描 BDinfo，则全部任务完成后会在 SSH 上输出 BDinfo Quick Summary，直接从 SSH 上复制即可  

![h5ai](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.05.png)

安装了 `h5ai` 的话可以在网页上预览、下载生成的截图、BDinfo、种子  





### To Do List

- **判断操作是否成功**  
目前操作中哪一步翻车了也不会有翻车了的提醒  


### Under Consideration

- **自动上传到 ptpimg**  
调用 ptpimg_uploader 来完成，脚本跑完后会输出 ptpimg 的链接。运行之前你需要自己配置好 ptpimg_uploader  