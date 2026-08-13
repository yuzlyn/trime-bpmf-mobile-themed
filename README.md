# trime-bpmf-mobile-themed

Android Trime / 同文輸入法的手機注音配置，基於 Rime 內建 `bopomofo_tw` 方案與 `nopdan/danjing` 主題結構，提供 Google 手機注音鍵盤配置與 `yuzlyn` 自訂主題。

預設主題使用 Catppuccin Frappe 配色，預設方案為注音臺灣正體。目標是在手機上直接使用純注音鍵盤，避免回退到 26 鍵拉丁鍵盤。

## 功能

- 預設啟用 `bopomofo_tw`
- 預設輸出臺灣正體字形
- 使用 `yuzlyn.trime` 主題，預設配色為 Catppuccin Frappe
- 點擊候選詞直接提交，不先放入預編輯區
- 停用應用程式輸入框內嵌預編輯，改用 Trime 候選窗預編輯
- 使用系統字體，不依賴第三方主題字型檔
- 注音鍵盤依 Google 手機注音鍵盤風格排列
- 長按中文空格切換到英文 QWERTY 鍵盤，英文鍵盤依手機交錯字母排列
- 禁用 `default`、`letter`、`qwertys`、`qwerty_` 的 26 鍵回退影響
- 長按第一排輸入數字 `1-0`
- 長按其他注音鍵輸入常用標點和符號
- 底部逗號鍵直接輸入 `，`，長按輸入 `。`
- 空格雙擊輸入 `。`
- 支援 emoji 候選和 `/happy`、`/sad` 等顏文字短碼

## 檔案結構

```text
.
├── default.custom.yaml          # Rime 全域補丁，只啟用 bopomofo_tw
├── bopomofo_tw.custom.yaml      # 注音方案補丁，預設臺灣正體、emoji、顏文字
├── kaomoji.schema.yaml          # 顏文字獨立方案
├── kaomoji.dict.yaml            # 顏文字碼表
├── opencc/                      # emoji OpenCC 資料
├── trime/
│   ├── danjing.yaml             # 符號鍵盤公共配置
│   └── yuzlyn.trime.yaml        # yuzlyn 主題與手機注音鍵盤
└── backgrounds/                 # 主題背景資源
```

## 安裝到手機

手機需要已安裝 Trime，並能透過 ADB 存取。預設 Rime 使用者目錄為 `/sdcard/rime`。

```powershell
adb push default.custom.yaml /sdcard/rime/default.custom.yaml
adb push bopomofo_tw.custom.yaml /sdcard/rime/bopomofo_tw.custom.yaml
adb push kaomoji.schema.yaml /sdcard/rime/kaomoji.schema.yaml
adb push kaomoji.dict.yaml /sdcard/rime/kaomoji.dict.yaml
adb push opencc /sdcard/rime/opencc
adb push trime/danjing.yaml /sdcard/rime/danjing.yaml
adb push trime/yuzlyn.trime.yaml /sdcard/rime/yuzlyn.trime.yaml
adb push backgrounds /sdcard/rime/backgrounds
adb shell rm -rf /sdcard/rime/build
adb shell am broadcast -a com.osfans.trime.deploy
```

部署後在 Trime 設定中選擇主題：

```text
yuzlyn.trime
```

配色選擇：

```text
catppuccin
```

方案選擇：

```text
注音·臺灣正體 / bopomofo_tw
```

## 注音鍵盤

主鍵點擊仍送出 Rime `bopomofo_tw` 方案使用的注音編碼；鍵面顯示為注音符號。

第一排長按：

```text
1 2 3 4 5 6 7 8 9 0
```

第二排長按：

```text
？ ！ 、 ： ； …… —— · ~ ￥
```

第三排長按：

```text
（ ） 「 」 “ ” 《 》 〈 〉
```

第四排長按：

```text
@ # $ % & * + - = /
```

這些符號使用 Trime `commit` 直接上屏，避免和正在輸入的注音編碼串接。

## 英文鍵盤

中文注音布局保持不變。需要輸入英文時，長按中文空格進入 `English` 鍵盤；英文鍵盤底部為數字、`☺︎` 表情、逗號、`EN` 空格、句號、Enter，長按 `EN` 空格返回注音。

## 顏文字

在注音方案內輸入 `/` 加編碼即可：

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

## 來源和授權

- 符號鍵盤與主題結構來自 [`nopdan/danjing`](https://github.com/nopdan/danjing)，授權見 [LICENSE.danjing](./LICENSE.danjing)。
- Catppuccin Frappe 配色參考 [`Slinet6056/rime-theme-catppuccin`](https://github.com/Slinet6056/rime-theme-catppuccin)，並調整為手機 Trime 使用。
- emoji 配置來自 [`rime/rime-emoji`](https://github.com/rime/rime-emoji)，授權見 [LICENSE.rime-emoji](./LICENSE.rime-emoji)。
