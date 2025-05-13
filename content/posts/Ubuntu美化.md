+++
date = '2025-05-12T00:15:28+08:00'
draft = true
title = 'Ubuntu美化'
+++
面对黑乎乎的命令行和靠左的菜单，是不是有点不适应呢？这里介绍一些美化的软件让你的Ubuntu更加美观，使用更加顺畅。
<!--more-->

> 如果修改过后发现用起来更卡了，建议卸载，毕竟用的流畅才能给人更好的体验！
> 在进行以下操作之前，请给你的虚拟机做好快照，避免出现其他问题导致虚拟机损坏还无法复原。

# vim
https://gitee.com/HGtz2222/VimForCpp

如果你是Centos系统，试试这个吧！个人评价：最佳。但很可惜，只支持Centos。

至于ubuntu的vim个性化设置，我了解的不多，如果你有好的推荐，欢迎留言！

# 窗口

主要是实现窗口的亚克力效果，俗称半透明磨砂、毛玻璃

执行：
```bash
sudo apt install chrome-gnome-shell -y
sudo apt install gnome-shell-extensions -y
sudo apt install gnome-tweaks -y
```

火狐浏览器搜**https://extensions.gnome.org**。先点击蓝色(蓝粉色？)的窗口里的`Click here to install browser extension`，然后点击右上角的弹窗里的`Continue to Insatllation`，之后依旧是右上角点击`Add`，最后系统弹窗选`Allow`。

## Blur My Shell
### 安装

> 笔者写这篇文章时，该插件刚好更新，更新之后的插件好多功能修改了，甚至删除，其中就包括笔者最喜欢的一个，笔者的插件是2025年之前的版本。

回到`https://extensions.gnome.org`页面，搜索 **Blur My Shell** ，进去之后点击OFF滑钮把他变成**ON**（如果没有说明上面的安装没有成功，重新安装一下），蓝色框框的右下角，Donate左边，然后点击`Install`。

装好之后原本滑钮的位置会变成一个锥子和扳手交叉的图片，点击就可以启动。（没有的话刷新一下）

点击最下方的Applications，右上角的滑钮点一下，让它拜托灰色状态。从上往下依次是：sigma = 模糊程度、Brightness = 亮度、Opacity = 透明度、取消当前窗口的半透明效果、全景模糊和全部窗口都开启半透明效果。一般都是开启倒数第三个和最后一个，前三个自己调到喜欢的程度就行。倒数第二个我没用过，不知道是啥。如果你开启了最后一个就可以不用做接下来的**Add Windows**了。

然后下滑找到标题**Whitelist**，点击它右边的**Add Windows**，然后点击你要半透明的窗口，多点点，如果出现无法选中的情况就拖拽一下窗口，然后多Add几次就行。

然后点击最下方的**Dash**，选择**Dynamic**，**sigma**调到0，**Brightness**调到1，这样可以让上面的时间哪里变透明。

点击最下方的**Panel**，重复以上操作，就可以让你的任务栏也变透明。

来到桌面，右键，点击`Change background`，然后选择`Dark`主题，下方的color选蓝色。（为啥选蓝色？我觉得般配就选了，如果你有其他喜欢的搭配就按你的来）

点击左边的Ubuntu Desktop，来到Dock的Position on Screen，选择Bottom，这样你的Dock就会在屏幕底部，size调成你觉得合适的大小就行。

---

### 卸载
回到`https://extensions.gnome.org`页面，点击锥子和扳手交叉的图片的右边的红叉叉就可以直接卸载。

---

## 壁纸
如果你要静态壁纸的话，不如直接在Ubuntu的设置里设置。但是如果你要设置动态的壁纸的话，就安装[fantascene-dynamic-wallpaper](https://github.com/dependon/fantascene-dynamic-wallpaper)吧！

```bash
cd ~
git clone https://gitee.com/liuminghang/fantascene-dynamic-wallpaper
cd fantascene-dynamic-wallpaper
sh start_deb.sh
```

安装完成之后，可以点击左下角的9个·，点击最右边的箭头来到右边，然后找到fantascene-dynamic-wallpaper，双击启动。

事先准备好动态壁纸的mp4文件，然后在右上角有个fantascene-dynamic-wallpaper的小图标。双击即可打开，弹出的窗口中，点击File选择你的MP4文件或者直接粘贴路径，找到model，点击`Add to startup Video aspect ratio`左边的小方块，重启试试效果即可。

## 终端
下载[MesloLGSNF](https://github.com/fontmgr/MesloLGSNF/tree/main/fonts)里的`MesloLGS NF Bold Italic.ttf`、`MesloLGS NF Bold.ttf`和`MesloLGS NF Regular.ttf`并安装。

```bash
cd ~
git clone https://github.com/fontmgr/MesloLGSNF.git
```

打开MesloLGSNF文件夹，进入fonts文件夹，分别双击`MesloLGS NF Bold Italic.ttf`、`MesloLGS NF Bold.ttf`和`MesloLGS NF Regular.ttf`，然后点击窗口右上角的`Install`，安装完成之后重启终端即可。

打开一个新的终端，点击右上角三条杠，点击`Preferences`，弹出的窗口中点击最左边的`Unnamed`，然后点击Custom font的左边的小方块启用，然后点击右边的大方块更改字体。在弹出的窗口中搜索**MesloLGS**，点击出来的MesloLGS NF，然后点击右上角的select。字体就完成了！

请保存快照，因为以下步骤极其容易出错！

安装zsh：

```bash
sudo apt install zsh -y
```

oh-my-zsh：

```bash
cd ~/
sudo git clone https://github.com/robbyrussell/oh-my-zsh
cd ~/oh-my-zsh/tools
sudo sh install.sh
exit
```
其他插件：
```bash
sudo apt install zsh-autosuggestions
sudo apt install zsh-syntax-highlighting
sudo mv /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh /usr/share/zsh-autosuggestions/zsh-autosuggestions.plugin.zsh
sudo mv /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.plugin.zsh
sudo cp -r /usr/share/zsh-autosuggestions ~/oh-my-zsh/custom/plugins
sudo cp -r /usr/share/zsh-syntax-highlighting ~/oh-my-zsh/custom/plugins
sudo git clone https://github.com/romkatv/powerlevel10k ~/oh-my-zsh/themes/powerlevel10k
sudo vim ~/.zshrc
```

然后会弹出vim窗口编辑文件，按i进入编辑模式，复制粘贴以下内容：
```bash
export ZSH="$HOME/oh-my-zsh"
ZSH_THEME="powerlevel10k/powerlevel10k"
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
source /usr/share/zsh-autosuggestions/zsh-autosuggestions.plugin.zsh
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.plugin.zsh
source $ZSH/oh-my-zsh.sh
```
然后esc退出编辑模式，输入`:wq`保存并退出vim。
输入以下命令：
```bash
sudo chmod 777 ~/.zshrc
chsh -s /bin/zsh
```
输入完后重启。重启之后打开终端，会显示一堆英文，这说明以上步骤你都成功了。

其实之后的步骤就全看个人喜好了，英语好的可以直接自立根生了，后面都是配置终端窗口的美化效果，比如测试终端能否正常显示字符，修改颜色，修改背景等等。

---

未完待续……



