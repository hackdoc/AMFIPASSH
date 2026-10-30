# AMFIPASSH

AMFIPassH 的已签名发布页。每次发布包含两个产物：

- `AMFIPassH-kext-strong.zip`：`AMFIPassH.kext`
- `AMFIPASSH-Monitor.zip`：`AMFIPASSH Monitor.app`

## 安装 kext

1. 下载并解压 `AMFIPassH-kext-strong.zip`。
2. 将 `AMFIPassH.kext` 放入 `EFI/OC/Kexts`。
3. 在 OpenCore 配置的 `Kernel -> Add` 中加入该条目，排在 Lilu 之后。
4. 将 `SecureBootModel` 设为 `Disabled`，不要添加 `amfi` 启动参数。
5. 重启。

## 状态面板

解压 `AMFIPASSH-Monitor.zip`，把 `AMFIPASSH Monitor.app` 拖入 `/Applications` 后打开。它显示 kext 是否加载、钩子状态与放行记录，并提供放行测试与 TCC 授权检查。

## 发布方式

Actions 每 30 分钟检查一次是否有新版本：有新版本时自动编译并发布，版本已发布则跳过。也可以在 Actions 页面手动运行；勾选 `force` 会替换同版本的旧发布。
