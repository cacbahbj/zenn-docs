---
title: "AnsibleでMacの環境構築を自動化する"
emoji: "📘"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["mac", "ansible"]
published: true
---
# 概要

以下のツールを使ってローカル環境の構築を自動化します
- Ansible: 自動化ツール
- Homebrew: macOS用パッケージマネージャ
  - homebrew-cask: GUIのアプリも管理
- mas-cli: Mac App Storeのアプリを管理

わかりやすさを優先して、シンプルにyamlファイル1つの構成で設定します
Roleを使ったグループ化や、Ansible Galaxyなどは使用しません

以下で動作確認済
- MacBook Pro 2021 / Apple M1 Pro
- ansible 2.16.7
- homebrew 4.3.5

# Ansibleとは

Redhatにより開発・提供されているオープンソースの自動化ツール
以下のようなプロセスの自動化ができ、プロビジョニングツールとか構成管理ツールと呼ばれることもあります
- [プロビジョニング](https://ja.wikipedia.org/wiki/%E3%83%97%E3%83%AD%E3%83%93%E3%82%B8%E3%83%A7%E3%83%8B%E3%83%B3%E3%82%B0)
- [構成管理](https://ja.wikipedia.org/wiki/%E6%A7%8B%E6%88%90%E7%AE%A1%E7%90%86)
- [アプリケーションのデプロイメント](https://ja.wikipedia.org/wiki/%E3%82%BD%E3%83%95%E3%83%88%E3%82%A6%E3%82%A7%E3%82%A2%E3%83%87%E3%83%97%E3%83%AD%E3%82%A4%E3%83%A1%E3%83%B3%E3%83%88)
- [オーケストレーション](https://ja.wikipedia.org/wiki/%E3%82%AA%E3%83%BC%E3%82%B1%E3%82%B9%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B7%E3%83%A7%E3%83%B3_(%E3%82%B3%E3%83%B3%E3%83%94%E3%83%A5%E3%83%BC%E3%82%BF))

※この辺の用語はふわっとしていて、デプロイのプロセスとして↑があるという言い方をしたり
プロビジョニングとオーケストレーションに分けたり割と曖昧です

https://docs.ansible.com/ansible/2.9_ja/index.html

# 事前準備

下記を参照してHomebrewをインストール
https://brew.sh/ja/

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Ansibleをインストール
```
brew install ansible
```

# 設定ファイル

## ファイル一覧
```
.
├── ansible.cfg
├── hosts
└── localhost.yml
```
## ansible.cfg

pythonがインストール済みの場合、設定しておくと実行時に警告が出なくなる
設定してなくてもおそらく問題ない
```
[defaults]
# interpreter_python=/usr/local/bin/python3
```

## hosts

```
[defaults]
localhost
```

## localhost.yml

- homebrew_packages
Homebrewで管理するパッケージ
- homebrew_cask_packages
homebrew-caskで管理するGUIのアプリ
- mac_app_store_apps
Mac App Storeのアプリ

```yml
---
- hosts: localhost
  connection: local
  gather_facts: no
  become: no
  vars:
    homebrew_packages:
      - { name: ansible }
      # - { name: awscli }
      # - { name: circleci }
      - { name: direnv }
      - { name: gettext }
      - { name: gh }
      - { name: gibo }
      - { name: git }
      - { name: git-flow }
      - { name: git-lfs }
      - { name: jq }
      - { name: mas }
      - { name: tree }
      - { name: wget }
      - { name: yq }
      - { name: zstd }
    homebrew_cask_packages:
      # - { name: alfred }
      # - { name: android-file-transfer }
      # - { name: android-studio }
      # - { name: brackets }
      # - { name: cyberduck }
      - { name: dbeaver-community }
      - { name: docker }
      # - { name: firefox }
      - { name: google-chrome }
      # - { name: google-japanese-ime }
      # - { name: intellij-idea }
      - { name: intellij-idea-ce }
      - { name: iterm2 }
      - { name: keepassxc }
      # - { name: mysqlworkbench }
      # - { name: pulsar }
      # - { name: pycharm-ce }
      # - { name: sequel-ace }
      - { name: slack }
      - { name: sourcetree }
      - { name: thunderbird }
      - { name: visual-studio-code }
      - { name: xmind }
      - { name: zoom }
    mac_app_store_apps:
      - { id: 497799835 } # Xcode

  tasks:
    # brew update
    - name: update homebrew
      community.general.homebrew:
        update_homebrew: yes

    # brew
    - name: brew install
      community.general.homebrew:
        name: '{{ item.name }}'
        state: present
      with_items: '{{ homebrew_packages }}'

    # cask
    - name: install homebrew cask packages
      community.general.homebrew_cask:
        name: '{{ item.name }}'
        state: present
        install_options: 'appdir=/Applications'
      with_items: '{{ homebrew_cask_packages }}'

    # mac app store
    - name: install mac app store apps
      community.general.mas:
        id: '{{ item.id }}'
        state: present
      with_items: '{{ mac_app_store_apps }}'

    # # pulsar packages
    # - name: pulsar packages install
    #   command: ppm install --packages-file pulsar_packages.txt --verbose

    # # dotfiles
    # - name: Pull dotfiles
    #   git: repo=git@github.com:foo/dotfiles.git dest=/path.to/tmp/dotfiles
    #   register: pull_dotfiles_result
    #
    # - name: Copy dotfiles
    #   copy: src=/path.to/tmp/dotfiles/{{ item }} dest=~/{{ item }} force=no
    #   with_items:
    #     - '.bashrc'
    #     - '.vimrc'
    #     - '.gitconfig'
    #   when: pull_dotfiles_result | changed
```

Mac App Storeのアプリは`mas-cli`のコマンドでIDを検索して↑のファイルで設定する
```
$ mas search Xcode
497799835 Xcode
```

コメントアウトしてますが、CLIでコマンドを実行したり、
GitHubに置いたdotfilesをコピーしたりなど実施することができます

↓pulsarについてはこちら
https://zenn.dev/cacbahbj/articles/a753aaea7ad82b

# セットアップ

カレントで以下のコマンドを実行
(Xcodeとかサイズがでかいのでちょっと時間かかります)
```
ansible-playbook localhost.yml -i hosts -v
```

(変更せずにチェックだけする場合)
```
ansible-playbook localhost.yml -i hosts -v --check
```
