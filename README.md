需要调整运行环境变量才可以正常使用！！！

Windows 安装步骤：

1、下载文件： 下载 go−legacy−win7−<version>.windows_<arch>.zip 文件。

2、解压文件： 将 ZIP 文件解压到 d:\ (或任何您喜欢的路径)。这将创建一个名为go-legacy-win7 的文件夹。

3、添加系统环境变量： 将以下内容添加到您的 系统环境变量中：将 d:\go-legacy-win7\bin (或您选择的路径) 添加到系统 Path 变量中。设置 GOROOT 变量的值为 d:\go-legacy-win7 (或您选择的路径)。

4、添加用户环境变量： 将以下内容添加到您的 用户环境变量中：将 %USERPROFILE%\go\bin 添加到用户 PATH 变量中。设置 GOPATH 变量的值为 %USERPROFILE%\go。

TG频道：https://t.me/for_win7

可使用如下批处理添加：
@echo off
setlocal
:: ============================================================
:: 请根据您的实际解压路径修改下面这一行
set "GO_INSTALL_DIR=D:\go-legacy-win7"
:: ============================================================

echo 正在配置 Go 环境变量，请稍候...

:: 1. 设置系统变量 GOROOT
setx /M GOROOT "%GO_INSTALL_DIR%"

:: 2. 将 GOROOT/bin 添加到系统 Path
:: 注意：这里使用了 PowerShell 来确保路径添加且不重复，避免破坏原有的 Path
powershell -Command "[Environment]::SetEnvironmentVariable('Path', [Environment]::GetEnvironmentVariable('Path', 'Machine') + ';%GO_INSTALL_DIR%\bin', 'Machine')"

:: 3. 设置用户变量 GOPATH
setx GOPATH "%USERPROFILE%\go"

:: 4. 将 GOPATH/bin 添加到用户 Path
powershell -Command "$userPath = [Environment]::GetEnvironmentVariable('Path', 'User'); if ($userPath -notlike '*%USERPROFILE%\go\bin*') { [Environment]::SetEnvironmentVariable('Path', $userPath + ';%USERPROFILE%\go\bin', 'User') }"

echo.
echo ============================================================
echo 配置完成！
echo 注意：请重新打开一个新的命令行窗口（CMD）来验证安装。
echo ============================================================
pause
