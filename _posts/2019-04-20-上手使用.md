---
layout:     post                    # 使用的布局（不需要改）
title:      wavesurfer上手使用               # 标题 
subtitle:   本文将介绍wavesurfer的使用方式  #副标题
date:       2019-04-20              # 时间
author:     Vega                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - Vue.js
---

# wavesurfer上手使用（Vue）

### 前言

此wavesurfer只适用于兼容的`Web Audio`标签的浏览器上，包括Firefox，Chrome，Safari（桌面和移动）和Opera。故不支持IE，如需兼容IE，请参考<https://github.com/laurentvd/wavesurfer.swf>



### 安装

`wavesurfer`在npm 上有两个包，分别是`wavesurfer`与`wavesurfer.js` 引用时请注意安装的是哪个，下面以`wavesurfer.js`为例

#### install wavesurfer

使用 `npm install` 命令安装 wavesurfer

```sh
npm install wavesurfer.js
```



#### 引入

##### 使用es 6方式

```javascript
import WaveSurfer from 'wavesurfer.js' //引入wavesurfer
```

##### 使用require方式

```javascript
var WaveSurfer = require('wavesurfer.js') //引入wavesu
```



### 使用

##### 创建一个用于显示波形图的容器（div标签）

```html
<div id="waveform"></div>
```

##### 在JavaScript中，创建WaveSurfer对象的实例（建议使用Vue变量）

```javascript
var wavesurfer = WaveSurfer.create({
    container: "#waveform" //选择容器
})
```

##### 加载音频

```javascript
wavesurfer.load(url) //url为音频文件位置
```

**wavesurfer.js**将加载文件，对其进行解码并显示漂亮的波形图。完成后将触发ready事件

##### 事件监听

wavesurfer.js有许多事件可以订阅，例如播放

```javascript
wavesurfer.on('ready',function(){
    wavesurfer.paly()
})
```

在Vue下可以在methos下直接写事件

``` javascript
play(){
    wavesurfer.play() //"wavesurfer" 为wavesurfer实例，具体名字请看自己定义的
}
```



### 方法（粗糙汉化）

在完成创建实例后（`var wavesurfer = WaveSurfer.create({ ... })`），可以调用以下方法



- `destroy()` 移除事件，元素，断开与Web Audio nodes的连接

- `empty()` 清除waveform图像

- `getCurrentTime()` 获取当前播放进度的时间

- `getDuration()` 获取音频时长

- `getPlaybackRate()` 获取播放速度

- `getVolume()` 获取音量

- `getMute()` 获取当前音量状态（是否静音）

- `getFilters()`  获取一个filters数组

- `getReady()` 获取当前准备状态

- `getWaveColor()` 获取播放后波形图显示的颜色

- `exportPcm(length, accuracy, noWindow, start)`导出PCM的JSON数组

- `exportImage(format, quality)` 导出波形图并回传URI

- `isPlaying()` 是否是播放状态，true为正在播放

- `load(url,peaks,preload)` 载入音频文件

- `loadBlob(url)`载入Blob类型的音频文件`on（eventName, callback）` 监听（订阅）事件

- `un（eventName, callback）` 取消监听（订阅）事件

- `unAll()`取消监听（订阅）所有事件

- `pause()` 暂停

- `play([start[,end]])`开始播放，可以设定播放起始点和结束点

- `playPause()` 暂停时播放，播放时暂停

- `seekAndCenter(progress)` 跳转到进度位置`[0..1]`( 0开始，1结束)

- `seekTo(progress)`跳转到进度位置，如上

- `setHeight(height)` 设定波形图高度

- `setFilter(filters)`  For inserting your own WebAudio nodes into the graph（不知道用途）
- 
- `setPlaybackRate(rate)` 设定播放速度（0.5半速，1正常，2为两倍速）

- `setVolume(newVolume)` 设定音量

- `setMute(mute)`设定静音，true静音，false取消静音

- `setWaveColor(color)` 设定播放过的声纹颜色

- `skip(offset)` 设定当前位置，跳过秒数（负数往后调）

- `skipBackward()`倒带

- `skipForward()` 前进

- `setSinkId(deviceId)` 设定播放设备

- `stop()` 停止，进度归零

- `toggleMute()` – Toggles the volume on and off.

- `toggleInteraction()` – Toggle mouse interaction.

- `toggleScroll()` – Toggles `scrollParent`.

- `zoom(pxPerSec)` – Horizontally zooms the waveform in and out. The parameter is a number of horizontal pixels per second of audio. It also changes the parameter `minPxPerSec` and enables the `scrollParent` option.



### 事件（粗糙汉化）

```javascript
wavesurfer.on('pause', function () {
 wavesurfer.params.container.style.opacity = 0.9
})
```

- `audioprocess`  播放进度同步
- `destroy` 实例被摧毁
- `error` 出错，返回错误信息
- `finish` 播放完成
- `interaction` 当与波形图有交互
- `loading` 音频文件载入中
- `mute` 静音状态改变，返回新的静音状态
- `pause` 音频被暂停时
- `play` 音频播放开始
- `ready` 音频文件准备完成
- `scroll` 滚动条滚动时
- `seek` 跳转时，回调会收到`[0..1]`的浮点数
- `volume` 音量改变时
- `waveform-ready` 波形图就绪时
- `zoom`缩放时，回调会收到minPxPerSec的整数

### 插件

#### 引入

##### 使用es 6方式

```javascript
import TimelinePlugin from 'wavesurfer.js/dist/plugin/wavesurfer.timeline.min.js' //引入插件
```

##### 使用require方式

```javascript
var TimelinePlugin = require('wavesurfer.js/dist/plugin/wavesurfer.timeline.min.js') //引入插件
```

### 使用

```javascript
var wavesurfer = WaveSurfer.create({
    container: "#waveform" //选择容器
    plugins: [
        TimelinePlugin.create({
        	container: '#wave-timeline',
        }),
    ]
})
```

### 现有插件

- #### [Regions plugin](https://wavesurfer-js.org/plugins/regions.html)

  Adds ability to display and interact with audio regions. Regions are visual overlays that can be resized and dragged around the waveform. You can play back and loop a region.

- #### [Timeline plugin](https://wavesurfer-js.org/plugins/timeline.html)

  Adds a nice simple timeline to your waveform. By [Instajams](https://github.com/instajams).

- #### [Microphone plugin](https://wavesurfer-js.org/plugins/microphone.html)

  Visualizes audio input from a microphone. By [Thijs Triemstra](https://github.com/thijstriemstra).

- #### [Minimap plugin](https://wavesurfer-js.org/plugins/minimap.html)

  Adds a minimap preview of your waveform. By [Enton Biba](https://github.com/entonbiba).

- #### [Playlist plugin](https://wavesurfer-js.org/plugins/playlist.html)

  Adds a playlist feature to your waveform. By [Enton Biba](https://github.com/entonbiba).

- #### [Cursor plugin](https://wavesurfer-js.org/plugins/cursor.html)

  Shows a cursor on your waveform.

- #### [Spectrogram plugin](https://wavesurfer-js.org/plugins/spectrogram.html)

  Shows a spectrogram for your waveform.

### 参考

- #### <https://wavesurfer-js.org/>