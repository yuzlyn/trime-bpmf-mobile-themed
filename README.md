# window-rime-bpmf

小狼毫 / Rime 的注音台湾正体配置，基于内置 `bopomofo_tw` 方案，额外加入 emoji 候选和 kaomoji 颜文字。

> 说明：仓库名使用 `bpmf`，但当前小狼毫内置方案 ID 是 `bopomofo_tw`。因此补丁文件必须命名为 `bopomofo_tw.custom.yaml`，否则重新部署后会找不到方案，表现为只能输入拉丁字母。

## 功能

- 默认启用 `bopomofo_tw`
- 为 `bopomofo_tw` 增加 emoji 候选开关
- 在 `bopomofo_tw` 内直接按注音打“顏文字”“開心”“哭”等词来输入颜文字
- 保留 `/vd`、`/vs` 等符号编码作为备用入口
- 保留小狼毫外观补丁 `weasel.custom.yaml`

## 安装

把仓库内文件复制到 Rime 用户目录，例如 Windows 小狼毫通常是：

```text
%APPDATA%\Rime
```

然后在小狼毫托盘菜单选择“重新部署”。

## 使用

### 注音输入

默认方案是 `bopomofo_tw`。这个方案底层使用 Rime 的 `terra_pinyin` 词典，所以生成 `terra_pinyin.userdb` 是正常现象，不代表切到了拼音方案。

### Emoji 候选

在 `bopomofo_tw` 中输入中文词时，候选里会出现相关 emoji。

可以通过方案选项切换：

```text
無繪文字 / 有繪文字
```

### 颜文字

不用切换方案，在 `bopomofo_tw` 中直接按注音输入这些词即可出颜文字候选：

```text
顏文字
表情
開心
笑
哭
難過
生氣
害羞
驚訝
攤手
無奈
躺平
動作
姿勢
```

例如用注音打“開心”，候选里会出现：

```text
≧▽≦ / ヽ(ﾟ∀ﾟ*)ﾉ / ～(￣▽￣～)(～￣▽￣)～
```

也可以继续使用 `/` 加编码作为备用入口：

常用编码：

```text
/va    动作/态度类
/vd    可爱/哭笑类
/vs    杂项表情
/vz    姿势类
/kao   全部候选
```

示例：

```text
/vd -> ≧▽≦ / 〒▽〒 / ＞﹏＜
/vs -> (´･ω･`) / (つД`) / ヽ(ﾟ∀ﾟ*)ﾉ
```

## 文件说明

- `default.custom.yaml`：启用 `bopomofo_tw`
- `bopomofo_tw.custom.yaml`：注音台湾正体补丁，加入 emoji 过滤器和颜文字符号表
- `kaomoji_tw.dict.yaml`：按注音词触发的颜文字词库
- `kaomoji.schema.yaml`：颜文字独立方案
- `kaomoji.dict.yaml`：颜文字码表
- `opencc/`：emoji OpenCC 转换数据
- `weasel.custom.yaml`：小狼毫外观补丁

## 来源

- emoji 配置来自 [`rime/rime-emoji`](https://github.com/rime/rime-emoji)
- kaomoji 配置来自 GitHub Gist `Godoword/52a37d38b31d8906a844cea880dd95d4`

`rime-emoji` 的许可证见 [LICENSE.rime-emoji](./LICENSE.rime-emoji)。
