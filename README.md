# Hyduan's Homebrew Tap

个人维护的 Homebrew 软件仓库，用于收录和管理日常使用的软件。

## 使用

添加此仓库：

```sh
brew tap hyduan/tap
```

当前尚未收录软件包。以下命令中的 `<软件包名>` 为占位符，使用时请替换为实际名称。

安装桌面应用（Cask）：

```sh
brew install --cask hyduan/tap/<软件包名>
```

安装命令行工具（Formula）：

```sh
brew install --formula hyduan/tap/<软件包名>
```

### 更新

```sh
brew update
brew upgrade hyduan/tap/<软件包名>
```

对于支持自动更新的桌面应用，可以使用：

```sh
brew upgrade --cask --greedy hyduan/tap/<软件包名>
```

### 卸载与清理

```sh
brew uninstall hyduan/tap/<软件包名>
```

如果 Cask 定义了 `zap` 规则，可显式清理对应的配置、缓存和用户数据：

```sh
brew uninstall --cask --zap hyduan/tap/<软件包名>
```

执行 `--zap` 前请查看对应 Cask 的清理路径，并备份需要保留的数据。

## 添加软件包

- 桌面应用放在 `Casks/<软件包名>.rb`。
- 命令行工具放在 `Formula/<软件包名>.rb`。
- 优先使用官方固定版本下载地址，并校验 SHA256。
- 根据软件实际要求声明系统版本、架构及依赖。
- Cask 的清理路径应依据源码或实际安装包确认，避免删除共享目录和外部项目。
- 添加软件后，在本文补充名称、用途、安装命令及必要说明。

### 本地开发

尚未发布时，可以将当前仓库链接到 Homebrew 的 tap 目录。仅在尚未注册 `hyduan/tap` 时执行，并按实际位置修改仓库路径：

```sh
mkdir -p "$(brew --repository)/Library/Taps/hyduan"
ln -s /Users/hyduan/Code/homebrew-tap "$(brew --repository)/Library/Taps/hyduan/homebrew-tap"
```

检查 Cask 格式、在线审查和上游版本：

```sh
brew style Casks/<软件包名>.rb
brew audit --cask --online hyduan/tap/<软件包名>
brew livecheck --cask hyduan/tap/<软件包名>
```

检查 Formula：

```sh
brew style Formula/<软件包名>.rb
brew audit --strict hyduan/tap/<软件包名>
brew test hyduan/tap/<软件包名>
```

提交前验证实际安装及普通卸载，测试 `zap` 时使用隔离数据。更新版本时同步修改版本号、下载地址、SHA256 和相关说明。
