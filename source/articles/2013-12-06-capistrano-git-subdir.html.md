---
title: Capistranoでgitレポジトリのサブディレクトリをデプロイ対象にする
date: 2013-12-06 10:28 JST
tags: Capistrano, git
published: false
---

教えて[Stackoverflow](http://stackoverflow.com/questions/29168/deploying-a-git-subdirectory-in-capistrano)

set \:deploy\_via, \:remote\_cache の場合
-----------------

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

## set :deploy_via, :copy の動作をさせたい場合
