# Windows下Switch Homebrew自制程序开发环境部署指南

本指南将帮助您在Windows上设置Nintendo Switch自制程序的开发环境。我们将使用Windows子系统Linux（WSL）和Docker来创建这个环境。

## 目录
1. [安装WSL](#安装wsl)
2. [安装Docker并配置代理](#安装docker并配置代理)
3. [下载Docker镜像](#下载docker镜像)
4. [编译和测试](#编译和测试)
5. [下载所需的头文件](#下载所需的头文件)
6. [下载模拟器](#下载模拟器)
7. [运行自制程序](#运行自制程序)

## 安装WSL
参照 https://zhuanlan.zhihu.com/p/475462241 安装wsl到windows
## 安装Docker并配置代理

1. **下载Docker Desktop**：
   - 访问[Docker Desktop](https://www.docker.com/products/docker-desktop)并下载安装程序。

2. **安装Docker Desktop**：
   - 运行安装程序并按照说明完成安装。

3. **配置代理（如有需要）**：
   - 如果您在代理后面，打开Docker Desktop，进入“Settings” > “Resources” > “Proxies”，输入您的代理设置。

4. **启用WSL集成**：
   - 在Docker Desktop中，进入“Settings” > “General”，启用“Use the WSL 2 based engine”。

## 下载Docker镜像

1. **打开您的WSL终端**。
2. **运行以下命令下载Docker镜像**：

``` bash
docker run --rm -it --privileged --network=host -v //c/Users/%USERNAME%/workspace:/workspace devkitpro/devkita64:latest
``` 

- 此命令将下载`devkitpro/devkita64`镜像并打开一个交互式终端。

## 编译和测试

1. **下载SwitchPixelGameEngine**：
- 运行以下命令克隆该项目：
  ```
  git clone https://github.com/tiansongyu/SwitchPixelGameEngine.git
  ```

2. **导航到项目目录**：

3. **编译项目**：
``` bash 
make -j12
``` 

- 此命令将编译项目并创建可执行文件。

4. **进行测试以确保一切正常工作**。

## 下载所需的头文件

1. **下载libnx头文件**：
- 运行以下命令克隆libnx库：
  ```
  git clone git@github.com:switchbrew/libnx.git
  ```

2. **配置开发环境**：
- 确保在VSCode中正确配置include路径，以便能找到libnx中的头文件。您可以在VSCode的设置中添加如下内容：

  ```
  {
    "C_Cpp.default.includePath": [
      "${workspaceFolder}/**",
      "/path/to/libnx/include" // 替换为实际路径
    ]
  }
  ```

3. **按照库中的说明进行额外设置**：
- 在libnx的文档中查找任何特定的环境变量或其他配置步骤，确保开发环境能够正确找到所有需要的库和工具。

## 下载模拟器

1. **访问Citron模拟器网站**： [Citron Emulator](https://citron-emu.pro/)
2. **下载并安装模拟器**。
- 此模拟器允许您合法地运行自制程序。

## 运行自制程序

1. **打开Citron模拟器**。
2. **将您的编译好的自制程序加载到模拟器中**。
3. **按照Citron模拟器提供的说明运行您的应用程序**。

## 结论

您已经成功在Windows上使用WSL和Docker设置了Nintendo Switch自制程序的开发环境！请仔细遵循这些步骤，您应该能够有效地编译和测试您的应用程序。

如果遇到任何问题，请参考每个工具的官方文档或在线寻求相关社区的帮助。
