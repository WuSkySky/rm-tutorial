针对snap火狐的处理
# 1. 如果还没做，先清理
sudo snap remove firefox
sudo apt purge firefox -y
sudo apt autoremove -y

# 2. 安装 Mozilla 官方仓库的密钥和源
sudo install -d -m 0755 /etc/apt/keyrings
wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee /etc/apt/sources.list.d/mozilla.list > /dev/null

# 3. 设置优先级（与上面仓库匹配）
echo 'Package: firefox*
Pin: origin packages.mozilla.org
Pin-Priority: 1001' | sudo tee /etc/apt/preferences.d/mozilla-firefox > /dev/null

# 4. 安装原生 Firefox
sudo apt update
sudo apt install firefox -y

# 5. 清理图标残留并重新登录
mv ~/.local/share/applications/firefox_firefox.desktop ~/.local/share/applications/firefox_firefox.desktop.backup 2>/dev/null
现在你的火狐浏览器就是完全脱离 Snap、真正的 APT 原生版本了，图标也会回来。
原因：
Snap 的隔离机制阻断了火狐与系统输入法框架的正常通信，导致中文输入法无法正常使用。
1. Snap 的沙盒（Sandbox）是做什么的？
Snap 默认运行在 “严格限制（strict）” 的沙盒模式中。应用被限制在自己的挂载命名空间、文件系统和网络环境内，看不到宿主系统的很多东西，包括：

    宿主系统的进程间通信（如 D‑Bus、Unix 套接字）

    宿主系统的环境变量（如 GTK_IM_MODULE、QT_IM_MODULE、XMODIFIERS）

    宿主系统的输入法守护进程（如 fcitx、ibus）

这就意味着，火狐浏览器不知道你正在使用哪种输入法，也不知道去哪儿连接它。
建议预留空间：500 MB