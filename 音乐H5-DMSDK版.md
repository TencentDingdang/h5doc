### PlayBackController DMSDK

- H5 发送获取播放状态消息

  H5 在每次显示页面时都会发送该消息给终端

1. H5 发送消息格式：

```js
{
    cmd: "DDApi.proxydata",
    id: "{{msgId}}",
    callback: "回调函数名",
    data: {
        action: "media", // 固定值
        event: "ON_RESUMED"
    }
}
```

2. Navtive根据收到的msg格式，执行相应操作后，调用DMSDK的api回调——onDataRecv

data属性格式如下：
```js
{
    action: "media",  // 固定值
    data: {
        version: 3,
        event: "ON_RESUMED",
        source: {
            song: "温柔",  // 歌曲
            songId: "5199848", // 歌曲id
            singer: "五月天",  // 歌手
            singerId: "74",   // 歌手id
            album: "爱情万岁",  // 专辑
            albumId: "96252",  // 专辑id
            like: 1  // 是否喜欢
        },
        control: {
            state: "当前播放状态: PLAY, PAUSE, STOP",
            offset: 100,  // 当前播放位置，单位s
            duration: 360, // 总时长
            mode: 0  // 播放模式 0:由终端控制 1:随机 2:顺序 3:单曲循环 4:列表循环
        }
    },
}
```

- H5发送senmatic消息

用户点击H5执行操作时，发送对应semantic消息，Navitve接收到消息后直接将semantic内容发送给后台。

```js
{
    cmd: "DDApi.proxydata",
    id: "{{msgId}}",
    callback: "回调函数名",
    data: {
        action: "semantic",
        data: "明确语义"
    }
}
```

2. H5 接受回调

   Navtive 调用DMSDK的api回调——onDataRecv，其中data字段格式如下：
  
```js
{
    action: "media",  // 固定值
    data: {
        version: 3,
        event: "PLAY",   // PLAY, PAUSE, STOP, MEXT, PRE, LIKE
        source: {
            song: "温柔",  // 歌曲
            songId: "5199848", // 歌曲id
            singer: "五月天",  // 歌手
            singerId: "74",   // 歌手id
            album: "爱情万岁",  // 专辑
            albumId: "96252",  // 专辑id
            like: 1  // 是否喜欢
        },
        control: {
            state: "当前播放状态: PLAY, PAUSE, STOP",
            offset: 100,  // 当前播放位置，单位s
            duration: 360, // 总时长
            mode: 0  // 播放模式 0:由终端控制 1:随机 2:顺序 3:单曲循环 4:列表循环
        }
    }
}
```