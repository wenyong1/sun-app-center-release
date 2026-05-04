# Sun 应用中心

`Sun 应用中心` 是一个独立 Android APK，用来集中查看和安装自有 App。

## 当前能力

- 读取总清单 `apps.json`。
- 每个 App 可以直接写版本信息，也可以只写它自己的 `manifestUrl`。
- 自动识别手机上是否已安装目标 App。
- 对比本机 `versionCode` 和远端最新 `versionCode`。
- 显示 `未安装`、`可更新`、`最新`、`本机较新`、`清单异常`。
- 下载 APK 后通过 Android 系统安装器安装，用户仍需按系统提示确认。

## 后续新增 App

新增自有 Android App 时，默认把它接入 `Sun 应用中心`。具体步骤见：

```text
market/sun-app-center/ADDING-APPS.md
```

## 推荐清单结构

中心清单只登记 App，后续每个 App 发版时维护自己的 `latest.json`：

```json
{
  "name": "童程打卡",
  "packageName": "com.tongchengdaka.app",
  "description": "孩子日常打卡、记录和提醒。",
  "manifestUrl": "https://raw.githubusercontent.com/wenyong1/tongchengdaka-release/main/latest.json",
  "releasePageUrl": "https://wenyong1.github.io/tongchengdaka-release/"
}
```

这样 `童程打卡` 每次运行 `Publish-GitHub-Release.ps1` 后，`Sun 应用中心` 会自动看到它的新版本。

## 默认远端清单地址

`sunappcenter` module 默认读取：

```text
https://raw.githubusercontent.com/wenyong1/sun-app-center-release/main/apps.json
```

如果远端不可用，App 会回退到内置的 `assets/apps.json`。

## 构建命令

```powershell
.\gradlew.bat :sunappcenter:assembleRelease
```

输出 APK：

```text
sunappcenter/build/outputs/apk/release/sunappcenter-release.apk
```

本次已额外复制到：

```text
market/dist/SunAppCenter-1.0.1.apk
```

当前 APK 的 SHA-256：

```text
374825a5d7b59c3e978206b2656a28ae10190630627502a727572309efabfe81
```
