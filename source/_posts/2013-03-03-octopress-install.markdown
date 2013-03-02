---
layout: post
title: "GitHub+Octopressでブログ構築"
date: 2013-03-03 03:42
comments: true
categories: Github
---

![Octopress title](/images/201303/octopress-title.png)

GitHub+[Octopress](http://octopress.org/)でブログを構築したときのメモ。

今回は[Github Pages](http://pages.github.com/)の*User& Organization Pages*にブログを設置する。

あらかじめ`アカウント名.github.com`という名前のレポジトリを生成しておく。
サイトのURLは`http://アカウント名.github.com/`になる。
`Ruby 1.9.3`が必要。

```bash
$ git clone https://github.com/imathis/octopress.git tsujita.github.com
$ cd tsujita.github.com
$ rbenv global 1.9.3-p194
$ gem install bundler
$ rbenv rehash
$ bundle install
$ rake install
$ rake setup_github_pages
Enter the read/write url for your repository: git@github.com:tsujita/tsujita.github.com.git
$ rake generate
$ rake deploy
```

`rake generate`で`_deploy`以下にサイトに公開されるファイルが生成されるようだ。
`rake deploy`で`_deploy`がmasterブランチにpushされ、
<http://tsujita.github.com/>から参照できるようになる。

設定ファイルやポストはsourceブランチで管理するようなので別途pushしておく。

```bash
$ git add .
$ git commit -m '最初のコミット'
$ git push -u origin source
```

設定は`_config.yml`で行う。

```yml
url: http://tsujita.github.com
title: GitHubでブログのテスト
subtitle: Octopressでおためしブログ
author: tsujita
simple_search: http://google.com/search
description:
```

ポストを作成するコマンドが用意されている。

```bash
$ rake new_post['octopress-install']
$ vi source/_posts/2013-03-03-octopress-install.markdown
```

画像ファイルは`source/images`に月毎にディレクトリを作成して設置することにした。
`rake generate`で`_deploy`以下にコピーされるので絶対パスで指定。

書き終わったら生成＆デプロイ。

```bash
$ rake generate
$ rake deploy
```

ローカルでプレビューもできる。

```bash
$ rake preview
```

