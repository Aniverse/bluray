# BD-Upload
Automatic Blu-ray Disk Upload Toolkit

### 下载与安装
独服，VPS
```
wget -O /usr/local/bin/bdupload https://github.com/Aniverse/bdupload/raw/master/bdupload
chmod +x /usr/local/bin/bdupload
```

FH,SH 盒子
```
git clone https://github.com/Aniverse/bdupload
cd bdupload && bash bdupload
```

### 运行
```
bdupload
```
### 介绍

转发蓝光原盘时可以使用的一个脚本；目前不支持 UltraHD Blu-ray

![检查是否缺少软件](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.01.png)

一开始脚本会检查是否存在缺少的软件，如缺少会提示你安装，如果选择不安装的话脚本会退出  

![正常运行界面](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.02.png)

注意：路径里即使带空格也不需要双引号  

目前可以实现以下功能：  

- **判断是 BDISO 还是 BDMV**  
输入一个完整的路径，判断是不是文件夹；*是文件夹的话认为是 BDMV，不是文件夹的话认为是 BDISO*  

- **自动挂载镜像**  
如果是 BDISO，会挂载成 BDMV，并问你是否需要对这个挂载生成的文件夹重命名（有时候 BDISO 的标题就是 DISC1 之类的，重命名下可能更好）  
全部操作完成后 BDISO 会自动解除挂载  

- **截图**  
自动寻找 BD 里体积最大的 m2ts 截 10 张 png 图。默认用 1920×1080 的分辨率，也可以手动填写分辨率  
指定 1920×1080 分辨率是因为某些原盘用 ffmepg 直接截图的话截出来的图是 1440 ×1080 的，不符合某些站的要求  
自定义分辨率主要是考虑到有些原盘的分辨率不是 1080 （有些蓝光原盘甚至是 480i ）  

- **扫描 BDinfo**  
默认是自动扫描第一个最长的 mpls；也可以手动选择扫描哪一个 mpls  
BDinfo 会有三个文件，一个是原版的，一个是 Main Summary，一个是 Quick Summary  
一般而言发种写个 Quick Summary 就差不多了  

- **生成缩略图**  
这个功能默认不启用；其实一般也用不上  

- **制作种子**  
针对 BDISO，默认选择重新做种子；针对 BDMV，默认选择不重新做种子 

![输出结果](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.03.png)

![h5ai](https://github.com/Aniverse/filesss/raw/master/Images/bdupload.04.png)
需要注意的是，脚本里挂载、输出文件都是指定了一个固定的目录`/etc/inexistence`  
安装了 `h5ai` 的话可以在网页上预览、下载生成的图片和文字  

### To Do List

- **完善对于输入路径的判断**  
对于文件夹，检查是不是里面包含着单个 BDISO，或者包不包含 BDMV 这个文件夹  
对于非文件夹，检查文件后缀名是不是 ISO  
- **增加对于无 root 权限盒子的支持**  
主要适配 FeralHosting 与 SeedHost  
- **判断操作是否成功**  
目前操作中哪一步翻车了也不会有翻车了的提醒    
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