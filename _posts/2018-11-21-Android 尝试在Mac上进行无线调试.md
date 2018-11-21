### Android 尝试在Mac上进行无线调试

1. Install [homebrew](http://brew.sh/)

   ` ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" `

2. Install adb 

   ` brew cask install android-platform-tools `

3. Start using adb

   ` adb devices`

4. Connect Phone

   Adb connect 192.168.209.27  ; 这里可能不同手机端口不一样，我的小米手机，尝试多个短裤，均不能连接  

   > unable to connect to 192.168.209.75:5555: Connection refused

   解决方案 ：

   > 手机连接电脑，运行 adb tcpip 8888  为手机设置一个临时端口。经测试，手机重启后继续连接失败，还是要重新设置端口。





#### 常用命令

安装    adb install apk路径

卸载    adb uninstall 包名