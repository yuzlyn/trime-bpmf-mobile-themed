# trime-bpmf-mobile-themed

Android Trime / 同文输入法的手机注音配置，基于 Rime 内置 `bopomofo_tw` 方案、`nopdan/danjing` 单静主题和 `ChiesiMario/trime_fira_theme` 的 Fira 外观调整。

这个配置的目标是让 Trime 在手机上直接使用纯注音键盘，而不是 26 键拉丁键盘。

## 功能

- 默认启用 `bopomofo_tw`
- 默认输出臺灣正體字形
- 使用 Fira 风格配色，并内置适配后的手机注音键盘
- 使用系统字体，不依赖 Fira 主题自带字体文件
- 注音键盘按 Google 注音手机键盘风格排列
- 长按中文空格切换到英文 QWERTY 键盘，英文键盘按手机交错字母排列
- 禁用 `default`、`letter`、`qwertys`、`qwerty_` 的 26 键回退影响
- 长按第一排输入数字 `1-0`
- 长按其他注音键输入常用标点和符号
- 底部逗号键直接输入 `，`，长按输入 `。`
- 空格双击输入 `。`
- 支持 emoji 候选和 `/happy`、`/sad` 等颜文字短码

## 文件结构

```text
.
├── default.custom.yaml          # Rime 全局补丁，只启用 bopomofo_tw
├── bopomofo_tw.custom.yaml      # 注音方案补丁，默认臺灣正體、emoji、颜文字
├── kaomoji.schema.yaml          # 颜文字独立方案
├── kaomoji.dict.yaml            # 颜文字码表
├── opencc/                      # emoji OpenCC 数据
├── trime/
│   ├── danjing.yaml             # 单静主题公共配置
│   └── 单静.trime.yaml          # 已适配 Fira 外观的 Trime 主题和注音键盘
└── backgrounds/                 # 单静主题背景资源
```

## 安装到手机

手机需要已安装 Trime，并能通过 ADB 访问。默认 Rime 用户目录为 `/sdcard/rime`。

```powershell
adb push default.custom.yaml /sdcard/rime/default.custom.yaml
adb push bopomofo_tw.custom.yaml /sdcard/rime/bopomofo_tw.custom.yaml
adb push kaomoji.schema.yaml /sdcard/rime/kaomoji.schema.yaml
adb push kaomoji.dict.yaml /sdcard/rime/kaomoji.dict.yaml
adb push opencc /sdcard/rime/opencc
adb push trime/danjing.yaml /sdcard/rime/danjing.yaml
adb push trime/单静.trime.yaml /sdcard/rime/单静.trime.yaml
adb push backgrounds /sdcard/rime/backgrounds
adb shell rm -rf /sdcard/rime/build
adb shell am broadcast -a com.osfans.trime.deploy
```

部署后在 Trime 设置中选择主题：

```text
单静.trime
```

并选择方案：

```text
注音·臺灣正體 / bopomofo_tw
```

## 注音键盘

主键点击仍发送 Rime `bopomofo_tw` 方案使用的注音编码；键面显示为注音符号。

第一排长按：

```text
1 2 3 4 5 6 7 8 9 0
```

第二排长按：

```text
？ ！ 、 ： ； …… —— · ~ ￥
```

第三排长按：

```text
（ ） 「 」 “ ” 《 》 〈 〉
```

第四排长按：

```text
@ # $ % & * + - = /
```

这些符号使用 Trime `commit` 直接上屏，避免和正在输入的注音编码串接。

## 英文键盘

中文注音布局保持不变。需要输入英文时，长按中文空格进入 `English` 键盘；英文键盘底部为数字、`☺︎` 表情、逗号、`EN` 空格、句号、回车，长按 `EN` 空格返回注音。

## 颜文字

在注音方案内输入 `/` 加编码即可：

```text
/happy
/sad
/angry
/shy
/surprise
/shrug
/tableflip
/sleep
/all
```

## 来源和许可证

- 单静主题来自 [`nopdan/danjing`](https://github.com/nopdan/danjing)，许可证见 [LICENSE.danjing](./LICENSE.danjing)。
- Fira 外观参考 [`ChiesiMario/trime_fira_theme`](https://github.com/ChiesiMario/trime_fira_theme)。本仓库只移植配色和界面参数，保留手机注音布局，并使用系统字体。
- emoji 配置来自 [`rime/rime-emoji`](https://github.com/rime/rime-emoji)，许可证见 [LICENSE.rime-emoji](./LICENSE.rime-emoji)。
