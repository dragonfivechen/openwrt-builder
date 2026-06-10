# OpenWrt 自动编译工作流

基于 GitHub Actions 的 OpenWrt / ImmortalWrt 自动编译系统。

## 使用方法

### 手动触发编译

1. 进入仓库 → **Actions** → **Build OpenWrt** → **Run workflow**
2. 填写参数：
   - **源码仓库** — 默认 `immortalwrt`，可选 `lede`、`openwrt` 官方源码
   - **源码分支** — `openwrt-24.10`、`main` 等
   - **目标设备** — `x86_64`、`rockchip_armv8` 等
   - **SSH 连接** — 用于调试，开启后编译前暂停等待 SSH 接入

### 支持的目标

| 设备/架构 | 配置文件 | 说明 |
|---|---|---|
| x86_64 | `x86_64.seed` | PC / 虚拟机 / 软路由 |
| Rockchip ARMv8 | `rockchip_armv8.seed` | NanoPi R2S/R4S/R5S/R6S |

### 自定义配置

- 修改 `configs/*.seed` 文件可自定义包选择
- 将补丁文件放入 `patches/` 目录，工作流会自动应用

### 使用 SSH 调试

1. 在 `Run workflow` 中将 `SSH 连接` 设为 `true`
2. 启动后等待输出 `tmate` 连接地址
3. 通过 SSH 连接到编译环境，手动调整配置
4. 执行 `make -j$(nproc)` 继续编译
