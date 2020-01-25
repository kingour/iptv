# iptv



## 1. 说明

>​	本项目旨在通过自动化脚本检测内网组播地址哪些是可播放，并通过ffmpeg

>   ​	截屏直播流第0.1s的图像，后续通过整理图像获得地址所对应的频道内容。



## 2. 依赖



*   nodejs
*   iptv-checker（nodejs版）
*   ffmpeg
*   家庭宽带已安装



## 3. 环境安装



>   ​	现在以Mac为例，默认已安装`brew`

```bash
# install nodejs 12 lts
brew install node@12
npm config set registry https://registry.npm.taobao.org
npm config set disturl https://npm.taobao.org/dist

# install ffmpeg
brew install ffmpeg

# 需要知道本宽带对应的组播地址，比如是`239.1.1.1/24:1008`,不知道的可以通过抓包分析
```



## 4. 实操



## 4.1 生成单播列表



```bash
# 写个脚本或者人肉穷举所有单播地址，比如
rtp://239.1.1.1:1008
...
# 将结果输出到一个m3u文件中，比如iptv.m3u
```



## 4.2 检查列表是否可以播放



```bash
# 检查10s内能连接播放的地址
iptv-checker -t 10000 -o ~/iptv_checker iptv.m3u
# 程序最后会输出一个online.m3u
cat ~/iptv_checker/online.m3u
```



## 4.3 截屏IPTV直播流



```bash
# 针对每一个online的地址，截屏
ffmpeg -i "rtp://239.1.1.1:1008" -y -f mjpeg -t 0.1 -s 1280x720 "239.1.1.1.jpg"
```



## 5 结尾



>   ​	脚本还没写，有空整理下脚本