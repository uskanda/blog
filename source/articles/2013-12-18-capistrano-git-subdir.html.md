---
title: Capistranoでgitレポジトリのサブディレクトリ以下をデプロイ対象にする
date: 2013-12-18 00:15 JST
tags: Capistrano, git
---

gitの特定サブディレクトリ以下だけデプロイしたいんです＞＜
--------------------------------
Subversionからgitへの移行をしていると、
[Capistrano](https://github.com/capistrano/capistrano)の移行でつまづきました。

これまで、svnの特定のサブディレクトリ以下を取得、デプロイしていたけど、
gitはそもそもサブディレクトリ以下のみを指定したcloneができないので、そのまま移行できなかった。  

※これを書くときに調べたら、sparse-checkout という機能はあるみたい。   
[何もわからない / git の sparse-checkout](http://okitan.tumblr.com/post/7642201668/git-sparse-checkout)

教えて[Stackoverflow](http://stackoverflow.com/questions/29168/deploying-a-git-subdirectory-in-capistrano)した結果、下記のようにすればOKでした。

set \:deploy\_via, \:remote\_cache を指定している場合
-----------------
Capfile, deploy.rbに下記を追加。

##### Capfile
```ruby
require 'capistrano/recipes/deploy/strategy/remote_cache'

class RemoteCacheSubdir < Capistrano::Deploy::Strategy::RemoteCache

  private

  def repository_cache_subdir
    if configuration[:deploy_subdir] then
      File.join(repository_cache, configuration[:deploy_subdir])
    else
      repository_cache
    end
  end

  def copy_repository_cache
    logger.trace "copying the cached version to #{configuration[:release_path]}"
    if copy_exclude.empty? 
      run "cp -RPp #{repository_cache_subdir} #{configuration[:release_path]} && #{mark}"
    else
      exclusions = copy_exclude.map { |e| "--exclude=\"#{e}\"" }.join(' ')
      run "rsync -lrpt #{exclusions} #{repository_cache_subdir}/* #{configuration[:release_path]} && #{mark}"
    end
  end

end

set :strategy, RemoteCacheSubdir.new(self)
```

##### deploy.rb
```ruby
set :deploy_subdir, "project/subdir"
```

## set \:deploy\_via, \:copy の動作をさせたい場合
今回やりたかったのはこちら。
方法はいくつかためしたけど、gemになっている下記はちゃんと動きました。

[yyuu/capistrano-copy-subdir](https://github.com/yyuu/capistrano-copy-subdir)

Gemを追加するだけで動作します。

```ruby
gem 'capistrano-copy-subdir'
```

```shell
$ bundle install
```

インストール後、
deploy.rb内部の`deploy_via`自体を\:copyでなく、\:copy_subdirに書き換えます。

##### deploy.rb
```ruby
set(:deploy_via, :copy_subdir)
set(:deploy_subdir, 'project/subdir')
```

これでsvnで`set :deploy\_via, :copy`しているときと同等の動作になりました。
