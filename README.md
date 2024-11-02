# T-Box App 使用指南

## 概述
T-Box 是一款影视资源嗅探和播放应用，用户可以通过配置链接自定义影视站点和规则。应用本身不包含任何内置配置，用户需自行维护规则。T-Box 无广告、无后门、无远程开关，用户只要自行维护好规则就能一直免费使用。

## 常见问题

### 修改配置文件未生效
每次打开应用或切换站点时，应用会重新加载配置文件。修改配置文件后，建议重新打开应用以确保配置生效。

### 加载列表慢
切换站点时，应用会加载配置文件和影视列表。加载速度受配置链接和站点访问速度影响，与应用本身无关。

### 嗅探到链接后一直加载中
点击右上角感叹号查看是否成功嗅探到视频链接。如嗅探成功，可尝试切换系统播放器或在配置文件中指定播放器。如系统播放器也播放慢的话，可能是资源链接问题，请尝试切换播放源或站点。

### 嗅探链接慢
部分站点可能有广告倒计时，应用无法跳过。如多次尝试嗅探失败，可能是网页在手机端无法加载视频。

### 夸克或者uc网盘获取链接失败的问题
请在设置中检查cookie状态是否为登录成功，如果失效或未登录的话请重新登录。另外夸克网盘在切换剧集播放时需转存资源，在短时间内切换剧集会导致转存失败从而无法播放，建议切换剧集间隔时间在10秒以上。

## 配置链接

### 测试配置链接
- 国内加速链接：[https://ghp.ci/raw.githubusercontent.com/tBox2010/tBox/refs/heads/main/配置.json](https://ghp.ci/raw.githubusercontent.com/tBox2010/tBox/refs/heads/main/配置.json)
- 原链接：[https://raw.githubusercontent.com/tBox2010/tBox/refs/heads/main/peizhi.json](https://raw.githubusercontent.com/tBox2010/tBox/refs/heads/main/peizhi.json)

### 建议
将配置转存到自己的仓库，本仓库不做规则维护，现有规则仅供学习。

## 配置链接方式

### HTTP链接
直接使用HTTP链接。

### Gitee私人链接配置方式
1. 创建非公开仓库并上传配置文件。
2. 获取原始链接，如 `https://gitee.com/用户名/t-box/raw/master/348z_xbiu.json`。
3. 添加私人令牌，形成新链接：`https://gitee.com/用户名/t-box/raw/master/348z_xbiu.json?access_token=私人令牌`。

## 推荐播放器
- **流畅播放4K画质**
- **手势控制**：
  - 左边上下滑动：调节亮度
  - 右边上下滑动：调节音量
  - 左边双击：快退10秒
  - 右边双击：快进10秒
  - 屏幕上左右滑动：拖动播放的进度条
  - 长按2倍数播放
- **双语切换**
- **兼容性**：部分视频可能出现有声音没画面的情况，可切换至系统播放器。

## 系统播放器
- **播放4K视频**：部分4K视频可能稍卡顿，但兼容性高。
- **手势控制**：
  - 左边上下滑动：调节亮度
  - 右边上下滑动：调节音量
  - 双击：暂停或播放
  - 屏幕上左右滑动：拖动播放的进度条
- **双语切换**：不支持
- **兼容性**：兼容性强，但播放大文件的4K视频可能存在卡顿。

## 缓冲区大小
- **设置建议**：缓冲越大播放越流畅，一般设置128M即可，最大可设置256M。（仅针对推荐播放器）部分老设备建议不要设置太高，容易造成运行内存的压力。

## 配置类型说明
- `type=0`：苹果CMS影视对应的XML格式
- `type=1`：苹果CMS影视对应的JSON格式
- `type=2`：tvbox对应的xpath规则
- `type=3`：xbiu规则（在剧集获取时，部分站点可能会获取失败。建议使用soup规则）
- `type=4`：xbiubiu规则
- `type=5`：js爬虫脚本（对技术要求稍高）
- `type=6`：soup规则（推荐）

### 规则说明
- **xpath、xbiu、xbiubiu**：参考自tvbox的规则，能直接套娃。
- **soup规则**：使用简单，适配性强，推荐使用。

### type=5 补充说明
- **js脚本运行环境**：JavascriptCore。部分js代码可能无法直接运行，但写简单爬虫够用。

## 配置示例
```json
{
    "key": "wogg",  //每个站点的key需独立，不能用同一个key，key用以储存本地配置文件
    "name": "玩偶哥哥",//站点名称（如无特殊情况，不要频繁改动站点名称，涉及到本地历史、收藏记录等）
    "type": 5,
    "searchable": 1, //是否支持搜索 1=支持 0=不支持
    "filterClass": "", //过滤分类名称（多个分类用,逗号隔开）
    "firstClass": "", //将指定分类名称前置（多个分类名称用,逗号隔开）
    "filterPlay": "",  //过滤播放源名称（多个播放源用,逗号隔开）
    "firstPlay": "夸克网盘,夸克网盘2", //将指定播放源名称前置（多个源名称用,逗号隔开）
    "ext": "https://gitee.com/用户名/t-box/raw/master/js/wogg.js?access_token=私人令牌",//配置链接（支持带私人令牌的gitee链接）
    "flagable": 0, //是否需要vip或播放器解析播放 1=需要  0=不需要（youku、qq、iqiyi等需要解析，如网页嗅探视频的话部分网站已内置了vip解析）
    "filterPlayFileKeywords": "", //嗅探网页时过滤的视频链接关键字，过滤掉的链接不会取过来（多个关键字用,逗号隔开）
    "keepPlayFileKeywords": "", //嗅探时采用的视频链接关键字，app已支持大部分视频链接的嗅探，一般不需要特别设置（多个关键字用,逗号隔开）
    "selectedPlayer": "1" //指定播放器  0=推荐播放器  1=系统播放器，如留空将使用设置中选择的播放器
}
```
