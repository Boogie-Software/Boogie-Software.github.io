# Boogie-Software.github.io
Blogs/Articles of Boogie Software
## Getting up and running

Prerequirements (OSX)
- HomeBrew needs to be working
  check that `brew update` runs with no errors
- Openssl needs to be installed (for Jekyll)
  `brew install openssl`


Install RVM & Ruby (3.x.x) - additional info: https://rvm.io/rvm/install
```
$ \curl -sSL https://get.rvm.io | bash -s stable
```
Start a new (login) shell (to find rvm in path)
```
$ rvm install ruby
```
This will take a while...

```
$ rvm list #to see your installed versions
$ rvm use 3.x.x
```
if you get error about "RVM is not a function"
run `$ source $HOME/.profile` or try to relaunch your shell


### First time for a new project run:
```
$ gem install bundler jekyll
```
If you get error like
```
make "DESTDIR="
compiling binder.cpp
In file included from binder.cpp:20:
./project.h:119:10: fatal error: 'openssl/ssl.h' file not found
#include <openssl/ssl.h>
         ^~~~~~~~~~~~~~~
1 error generated.
make: *** [binder.o] Error 1
```
( see https://stackoverflow.com/questions/68794527/rubygems-error-while-installing-jekyll-openssl-ssl-h-file-not-found for more info)

Run:
```
$ brew link --force openssl
$ gem install eventmachine -- --with-cppflags=-I/usr/local/opt/openssl/include
$ gem install jekyll
```
Seems that webrick is missing as dependency
```
$ bundle add webrick
```



### For existing project run:
```
$ bundle install
```

## Start Jekyll (local server)

```
$ bundle exec jekyll serve
```

Now you should be able to navigate to http://localhost:4000 and see your project


## Importing Blogger -blog to Jekyll

See https://import.jekyllrb.com/docs/blogger/

1. Export your BLOGGER blog to .XML dump

2. Install `jekyll-import` with dependencies
```
$ gem install rexml safe_yaml jekyll-import
```
3. Do the actual import
```
ruby -r rubygems -e 'require "jekyll-import";\n    JekyllImport::Importers::Blogger.run({\n      "source"                => "/path/to/blog-MM-DD-YYYY.xml",\n      "no-blogger-info"       => false, # not to leave blogger-URL info (id and old URL) in the front matter\n      "replace-internal-link" => false, # replace internal links using the post_url liquid tag.\n    })'
```








