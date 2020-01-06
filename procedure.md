# Laptop environment setup procedure

## Overview
manjaro linux のセットアップ手順

## pacman / yay
```
$ sudo pacman-mirrors -f 0
$ sudo pacman -Syyu
$ sudo pacman -S yay # for chrome/dropbox ...
$ # pacman
$ sudo pacman -S zsh neovim tmux gpg
$ sudo pacman -S docker docker-compose
$ sudo pacman -S pass
$ sudo pacman -S git
$ sudo pacman -S xsel # for pbcopy
$ sudo pacman -S alacritty
$ sudo pacman -S pulseaudio
$ sudo pacman -S bat
$ # yay
$ yay -S google-chrome
$ yay -S dropbox
```

## tool インストール用のディレクトリ作成
```
$ mkdir ~/.local/bin
```

## 設定変更
- スクロールを逆にする
  - Mouse and Touchpad で、Reverse scroll direction をチェック
- 時計のフォーマットを以下に変更
  - preference で、`%m/%d %T` を指定

## 日本語入力
fcitx系パッケージのインストール
```
$ sudo pacman -S fcitx-mozc
$ sudo pacman -S fcitx-im fcitx-configtool
```

フォントのインストール
```
sudo pacman -S noto-fonts-cjk
cd /etc/fonts/conf.d
sudo ln -s ../conf.avail/70-noto-cjk.conf
```

Input method の設定
```
$ fcitx-configtool
```
- Mozc を追加

[参考](https://blog.inagaki.in/manjaro-linux-japanese-environment/)

## アプリケーション設定

### docker
起動設定
```
$ sudo systemctl enable docker
$ sudo usermod -aG docker m3y
```

### Cica font
```
$ git clone https://github.com/miiton/Cica.git
$ cd Cica
$ docker-compose build ; docker-compose run --rm cica
$ mkdir ~/.local/share/fonts
$ cp dist/*.ttf ~/.local/share/fonts/
$ chmod 444 ~/.local/share/fonts/*.ttf
$ fc-cache -vf
```

### chrome
- font を Cica に変更
- google アカウントでログインし、連携を有効にする

### gpg
gpg鍵のimport
```
$ gpg import /path/to/key
$ gpg --edit-key <KEY ID>
$ gpg> trust
```

### github
鍵登録
- [help document](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

### ZSH
デフォルト shell の変更
```
$ chsh -s $(which zsh)
```

zplug のインストール
```
$ curl -sL --proto-redir -all,https https://raw.githubusercontent.com/zplug/installer/master/installer.zsh | zsh
```

### peco
```
$ wget https://github.com/peco/peco/releases/download/v0.5.3/peco_linux_amd64.tar.gz
$ mv peco_linux_amd64/peco ~/.local/bin/
```

### ghq
```
$ wget https://github.com/motemen/ghq/releases/download/v0.12.9/ghq_linux_amd64.zip
$ unzip ghq_linux_amd64.zip
$ mv ghq_linux_amd64/ghq ~/.local/bin/
```

### memo
```
$ ghq get https://github.com/mattn/memo.git
$ cd /path/to/mattn/memo
$ go build
$ mv memo ~/.local/bin
```

plugin のインストール
```
$ ghq get git@github.com:m3y/memo-sync-plugins.git
$ cd /path/to/memo-sync-plugins/
$ cp pull ~/.config/memo/plugins/
$ cp push ~/.config/memo/plugins/
$ cp status ~/.config/memo/plugins/
$ ghq get git@github.com:m3y/memo-til-plugin.git
$ cd /path/to/memo-til-plugin/
$ cp til ~/.config/memo/plugins/
```

### Thunar
Show Hidden Files
- View > Show Hidden Files にチェック

### Ulauncher
```
$ ghq get https://aur.archlinux.org/ulauncher.git
$ cd /path/to/ulauncher
$ makepkg -is
```

### mdr
```
$ wget https://github.com/MichaelMure/mdr/releases/download/v0.2.2/mdr_linux_amd64
$ chmod +x mdr_linux_amd64
$ mv mdr_linux_amd64 ~/.local/bin/mdr
```

### gojq
```
$ wget https://github.com/itchyny/gojq/releases/download/v0.7.0/gojq_v0.7.0_linux_amd64.tar.gz
$ tar zxvf gojq_v0.7.0_linux_amd64.tar.gz
$ cd gojq_v0.7.0_linux_amd64
$ mv gojq ~/.local/bin/
```

## dotfiles 反映
```
$ ghq get git@github.com:m3y/dotfiles.git
$ cd /path/to/dotfiles
$ ./install
```
