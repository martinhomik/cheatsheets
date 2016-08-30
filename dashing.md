# Install RVM

Run the following command from your terminal.

```sh
curl -L https://get.rvm.io | bash -s stable --ruby
```

Be sure to follow any subsequent instructions as guided by the installation process.

## Install Ruby 2.3.1

Next install Ruby 2.3.1 and you'll be all set.

```sh
$ rvm install 2.3.1
$ rvm use 2.3.1
$ rvm use ruby-2.3.1
$ rvm rubygems latest
```

See also:  http://octopress.org/docs/setup/rvm/

Run ruby --version to be sure you're using Ruby 2.3.1. If you're having trouble, seek help here.

## Install Bundler

```sh
$ gem install bundler
```

See also: http://bundler.io/

Install all of the required gems from your specified sources:

```sh
$ gem install dashing
$ bundler
$ bundle install
$ git add Gemfile Gemfile.lock
```

Sometimes you need to install a dependency explicitly:

```sh
$ gem install nokogiri -v '1.6.8'
```

## Run on a different port, or in production

Dashing runs on Thin behind the scenes. That means that any config for running thin works. Example:

```sh
$ dashing start -p 5000 -e production
```

Run in the background

```sh
$ dashing start -d
```

Stop dashing running in the background:

```sh
dashing stop
```
