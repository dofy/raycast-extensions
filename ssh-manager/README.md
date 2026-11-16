# SSH Connections

在 Raycast 中搜索和管理 SSH 配置，按回车在选定的终端中连接。

## 安装与使用

```sh
pnpm install --frozen-lockfile
pnpm dev
```

打开 **SSH Connections**，列表自动读取 `~/.ssh/config` 和其 Include 文件中的具体主机别名；通配符和排除规则不作为连接显示。使用 `⌘ N` 新建连接，填写 SSH 别名，以及可选的 HostName、User、Port 和 IdentityFile。新连接写入 `~/.ssh/config`，留空字段交由 SSH 配置和默认值处理；不保存密码或私钥内容。

列表读取 SSH Config Editor 的部分图标，并映射为 emoji。SSH Config Editor 的颜色标签保存在 SSH 配置注释中，列表不显示这些标签。操作菜单中的 Set Icon 可以自定义单个 emoji；图标以 `#SSHManagerIcon` 注释保存在对应 Host 块，共享块的别名共用图标，清空后恢复已有图标。

Edit SSH Options 支持 ForwardAgent、ServerAliveInterval、ProxyJump、ProxyCommand、RemoteCommand、RequestTTY 以及 LocalForward、RemoteForward、DynamicForward。重复出现的受管选项和包含不同主机名的共享 Host 块需要手动编辑；原有其他指令和独立注释会保留，更改的选项行上的注释可能被替换。前面的全局或 Match 指令仍可能优先生效。

列表右侧显示代理、Agent 转发、端口转发、远程命令、端口和密钥配置标识；这些表示静态配置，而不是实时状态。列表显示别名以及可直接读取的 HostName、User、Port 和密钥标识；对包含显式主机匹配的条件规则，列表标注 Conditional route 并展示可静态读取的候选地址；这不是当前路由检测，展示时不会执行 Match 命令。其他复杂规则或继承值不保证在列表中显示，连接时仍由 SSH 解析完整配置。列表支持搜索、连接、编辑、复制命令和删除。删除前会确认，并移除对应的整个 Host 块。为保护已有配置，包含多个不同 Host 模式、重复别名、重复受管字段或 Include 的复杂块需要在文本编辑器中手动处理。仅大小写不同的等价 Host 模式可编辑字段；带显式主机 Match 条件的别名，以及多个等价拼写的 Host 块，重命名和删除仍需手动处理，避免遗漏相关规则。悬空的配置文件符号链接不会被覆盖。编辑保留其他指令和独立注释；受编辑字段行内的注释可能被移除。新增块放在全局指令之后、首个 Host 或 Match 之前；OpenSSH 的前置全局配置或 Include 仍可能优先生效。外部修改配置后重新打开命令，或使用 Refresh SSH Config。

旧版本保存在 Raycast LocalStorage 的连接会继续显示在 **Previous Raycast Connections**，可用 Copy to SSH Config 复制到配置文件，检查无误后再删除旧条目；备注和收藏状态不会写入 SSH 配置。

在扩展偏好设置的 **Default Terminal** 中选择 Terminal、iTerm 或 Ghostty（需已安装）。三个终端首次使用时都可能需要允许 Raycast 控制对应应用的 macOS 自动化权限。Ghostty 使用其 AppleScript 窗口配置接口（已在 Ghostty 1.4.0 测试），连接结束后保留窗口以显示结果。终端窗口打开不代表 SSH 已成功连接，认证和错误信息显示在终端中。

## 检查

```sh
pnpm test
pnpm lint
pnpm exec tsc --noEmit
pnpm build
```
