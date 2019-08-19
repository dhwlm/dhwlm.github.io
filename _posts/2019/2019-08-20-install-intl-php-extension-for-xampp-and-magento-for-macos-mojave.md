---
layout: post
title: Install intl PHP extension for XAMPP and Magento for MacOS Mojave
description: "I have finally found a fix for this"
tags: [php-intl, php intl, bugfix, magento, xampp, macos, php7,]
image:
  feature: macos-intl-php-extension-for-xampp.jpg
  path: images/macos-intl-php-extension-for-xampp.jpg
---

If you are trying to install Magento on MacOS, welcome, let me help you save some time. After a lot of research I was finally able to resolve this. The issue is with PHP Extension in macOS, and especially with XAMPP.

There are multiple ways to get it to work on macOS,
1. Using built-in Apache and PHP
2. Using XAMPP

It seemed pretty straight forward to get it to work using built-in Apache and PHP. Installing PHP correctly solved the issue. Using brew, php7.1 has intl extension built-in:

```shell
brew install php@7.1
```

Upgrade it to the latest version
```shell
brew upgrade php@7.1
```

Symlinks for references in Cellar
```shell
brew link --overwrite --force php@7.1
```

Change PHP path in my bash profile
```shell
echo 'export PATH="/usr/local/opt/php@7.1/bin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/usr/local/opt/php@7.1/sbin:$PATH"' >> ~/.bash_profile
```

Reload your bash profile (you can close the terminal and open it again)
```shell
. ~/.bash_profile
```

Check for Intl
```shell
php -m | grep intl
```

**Note:** If you come across with warnings like:
PHP Warning: PHP Startup: Unable to load dynamic library '/usr/local/opt/php71-intl/intl.so'
Then you have to disable the previous intl:
``mv /usr/local/etc/php/7.1/conf.d/ext-intl.ini /usr/local/etc/php/7.1/conf.d/ext-intl.ini.disabled``

if you run into issues with this check which PHP your system is using by 
```shell
which php
```
(it should be the one which you just installed: /usr/local/opt/php@7.1/... )

Now I have couple of projects already running on my mac with XAMPP. And switching between built-in Apache and XAMPP or MAMP to run my projects was too confusing and time consuming. So I was hoping to find a solution to get it to work for XAMPP.

For XAMPP, installing intl extension was pain in the butt, firstly because this extension is not provided by XAMPP out of the box. I had almost given up, most of the solutions didn't work for me. Mainly because they were meant for PHP5.6 and not for PHP7. (using pecl) I kept getting this error: "fatal error: 'ext/standard/php_smart_str.h' file not found" . Even tried to build the intl-extension using macports instead of pecl. but no luck.

Some solutions used brew packages which are now deprecated/deleted/moved. (using php71-intl ).  
`` brew tap kyslik/homebrew-php `` & `` brew install kyslik/php/php71-intl ``

Finally I got it to work using the following steps. Overall idea is to build the intl-extension from PHP source code on your own. 

Before you begin make sure you have installed Xcode. Also, install the latest version of autoconf. this might help: 
```shell
brew install autoconf
```

Next download the version of PHP you use in XAMPP from [php.net](https://www.php.net/downloads.php). I am using 7.1.18. This version worked for me: php-7.1.31, I'm guessing if you follow the steps it might work for 7.0 or 7.2 as well. Do let me know if it does or doesnt, I'll update this post. Do not use PHP 7.3 for Magento 2.3.0, it is not supported.

Extract the tar.gz file using (I extracted it inside ~/Downloads/ folder )
```shell
tar -xzvf php-7.1.31.tar.gz
```

cd into the extracted folder
```shell
cd php-7.1.31
```

change to subfolder ext/intl
```shell
cd ext/intl/
```

Run these commands to build the extension
```shell
/Applications/XAMPP/bin/phpize
./configure --enable-intl --with-php-config=/Applications/XAMPP/bin/php-config --with-icu-dir=/Applications/XAMPP/xamppfiles/
make
sudo make install 
```

you can now delete all files you downloaded and also the extracted folders.

Open /Applications/XAMPP/xamppfiles/etc/php.ini , and add ``extension=intl.so``

That's it! It should work now. You have to run these commands each time you install a new version of XAMPP. 

Cheers, and if I helped you save some precious time, [buy me a beer](https://www.paypal.me/dhawalm)!