Play-Nice
=========

Custom settings for developing your Ruby on Rails app without affecting the main repo

Use this if you want to:

  - develop with a different version of ruby to what's in .ruby-version
  - install extra gems like pry or spring without annoying other developers on tlcohe same project
  - customise your scripts and binstubs for the project without sharing

Installation
============

You will almost certainly want to customise this so it's easiest if you fork it first and clone your fork.

    cd YOUR_RAILS_APP_DIR
    git clone git@github.com:YOUR_GITHUB_ACCOUNT/play-nice.git
    echo "play-nice/" >> .git/info/exclude
    cp Gemfile.lock play-nice/Gemfile.local.lock

Usage
=====

Run the `app/play-nice/init` script once when you start a shell to work on the project. You *could* add it to your .bash_profile or .zshrc but it's really a project specific thing so you probably don't want to do that.
If you're using [tmuxinator](https://github.com/tmuxinator/tmuxinator), specify it in the project file with this line:

    pre_window: . ./play-nice/init

 - Check your ruby version with `ruby -v`. It should be the one specifed in play-nice/init instead of .ruby-version.

 - Running bundle will now use the `play-nice/Gemfile.local` which happens to include your `Gemfile` as well as whatever
 gems you modify it to use.

 - The `gbundle` alias will operate on your standard `Gemfile` to update `Gemfile.lock`. Whenever you modify `Gemfile` you should run both `gbundle` and `bundle`.


Customizing
===========
- Add your own gems to `play-nice/Gemfile.local` and run `bundle` to install them.
- Review the `play-nice/init` script and read the comments to customize any other behaviour

How it Works
============

 - The Gemfile customization is based on [this Stackoverflow answer](http://stackoverflow.com/a/19941643/195369).

 - Ruby version is set by an environment variable (for RBENV at least)

 - `play-nice/bin` is prepended to your PATH for overriding binstubs and scripts
