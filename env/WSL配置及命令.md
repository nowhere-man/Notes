# WSL

## WSL命令

| **列出可用的 Linux 发行版** | **wsl --list --online**                                       |
|----------------------|----------------------------------------------------------------|
| 列出已安装的 Linux 发行版     | wsl --list --verbose                                           |
| 安装                   | wsl --install <Distribution Name>                              |
| 设置WSL 版本             | wsl --set-version <distribution name> <versionNumber>          |
| 设置默认 WSL 版本          | wsl --set-default-version <Version>                            |
| 设置默认 Linux 发行版       | wsl --set-default <Distribution Name>                          |
| 更新 WSL               | wsl --update                                                   |
| 检查 WSL 状态            | wsl --version                                                  |
| 关闭                   | Wsl --shutdown                                                 |
| 导出发行版                | wsl --export <Distribution Name> <FileName>                    |
| 导入发行版                | wsl --import <Distribution Name> <InstallLocation> <FileName>  |