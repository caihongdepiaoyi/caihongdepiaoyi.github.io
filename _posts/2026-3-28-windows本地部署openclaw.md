# 在 Windows 本地安装 OpenClaw 的基本流程与方案比较

## 方案 A：在原生 Windows 上安装（概述）
1. 获取代码或发行包：git clone <OpenClaw 仓库> 或下载 release。
2. 安装依赖：
    - 安装 Python（如果是 Python 项目）并创建 venv。
    - 安装 Visual Studio Build Tools（含 C/C++ 编译器）或对应 Windows 编译器。
    - 安装库依赖（pip install -r requirements.txt / Windows 二进制依赖）。
3. 构建与安装：
    - 如果使用 CMake：在 PowerShell/CMD 执行 cmake && cmake --build。
    - 或运行项目提供的 Windows 安装脚本（如 setup.py、install.bat）。
4. 配置环境：
    - 设置 PATH、库路径（如 DLL 位置）。
    - 配置 config 文件、服务或注册表（如需要）。
5. 验证运行：执行自带测试或示例，检查日志与功能。

提示命令示例（替换为实际仓库/脚本）：
- git clone <repo>
- python -m venv venv && .\venv\Scripts\activate
- pip install -r requirements.txt
- cmake -S . -B build && cmake --build build --config Release

---

## 方案 B：在 WSL（Windows Subsystem for Linux）中安装
1. 启用 WSL：在 PowerShell（管理员）运行
    - wsl --install 或按需启用 WSL 功能并安装 Ubuntu 等发行版。出错：
    ```
    PS C:\Users\Administrator> wsl --install
    正在下载: Ubuntu
    无法与服务器建立连接
    错误代码: Wsl/InstallDistro/WININET_E_CANNOT_CONNECT
    ```
    改用下列命令，直接从微软的服务器下载 Ubuntu 安装包，而不是通过 Microsoft Store
    ```
    PS C:\Users\Administrator> wsl --install --web-download -d Ubuntu
    ```
    运行结果-设置账号密码：
    ```
    PS C:\Users\Administrator> wsl --install --web-download -d Ubuntu
    正在下载: Ubuntu
    正在安装: Ubuntu
    已成功安装分发。可以通过 “wsl.exe -d Ubuntu” 启动它
    正在启动 Ubuntu...
    Provisioning the new WSL instance Ubuntu
    This might take a while...
    Create a default Unix user account: administrator
    ```
    弹出配置窗口：
    ![配置窗口](/assets/img/20260328/welcome.png)
    如何在windows上访问wsl中文件：
    ```
    \\wsl.localhost\
    ```
    如何在wsl中访问windows文件：
    ```
    cd /mnt/c
    ```
    ![跨系统文件访问](/assets/img/20260328/跨系统文件访问.png)


2. 启动并更新发行版：sudo apt update && sudo apt upgrade。
3. 安装构建与运行依赖：gcc/g++, make, cmake, python3, pip, git 等。
    ```
    sudo apt install build-essential cmake python3 python3-pip
    sudo apt install git -y
    ```
4.  git配置：
    ```
    git config --global user.name "你的GitHub用户名"
    git config --global user.email "你的GitHub注册邮箱"
    ```
