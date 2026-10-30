# AMFIPASSH

在保证 AMFI 开启的情况下绕过 hackdoc 签名的 framework、kext 等，以及 nullmoth 的驱动。

本仓库只承载发布流程与发布产物；源码在 [pyquick/AMFIPass](https://github.com/pyquick/AMFIPass)。

## 发布流程

`.github/workflows/release.yml` 每 30 分钟运行一次（也可手动触发）：

1. 用 `PYQUICK_TOKEN` 克隆 `pyquick/AMFIPass`，从 `Tools/build.zsh` 读取 `VERSION`。
2. 检查本仓库是否已有 `v<VERSION>` 的 release；存在则直接结束，不编译。手动触发时勾选 `force` 可强制重建。
3. 安装 Homebrew LLVM 与 cmake，构建 OLLVM 插件，用 strong 配置编译 kext：`-bcf -sub -split`，函数级 flatten 由源码的 `HD_FLA` 注解控制。
4. 从 `HACKDOC_P12_BASE64` / `HACKDOC_P12_PASSWORD` 导入签名身份，kext 与状态面板都用 `Hackdoc Code Signing` 签名。
5. 编译状态面板，重命名为 `AMFIPASSH Monitor`，不混淆。
6. 打 tag 并创建 release，附上两个压缩包。

## 需要配置的 Secrets

| 名称 | 用途 |
| --- | --- |
| `PYQUICK_TOKEN` | 克隆 pyquick/AMFIPass 的访问令牌 |
| `HACKDOC_P12_BASE64` | Hackdoc 代码签名身份的 .p12，base64 编码 |
| `HACKDOC_P12_PASSWORD` | 上述 .p12 的密码 |

`GITHUB_TOKEN` 由工作流自动提供，用于在本仓库创建 release。

## 产物

- `AMFIPassH-kext-strong.zip`：`AMFIPassH.kext`，LLVM + OLLVM strong，Hackdoc 签名
- `AMFIPASSH-Monitor.zip`：`AMFIPASSH Monitor.app`，Hackdoc 签名，不混淆

安装：将 `AMFIPassH.kext` 放入 `EFI/OC/Kexts`，并在 `Kernel -> Add` 中排在 Lilu 之后；`SecureBootModel` 设为 `Disabled`；不要添加 `amfi` 启动参数。
