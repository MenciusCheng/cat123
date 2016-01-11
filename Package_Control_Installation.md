Package Control Installation
============================

本文摘自: <https://packagecontrol.io/installation>, 时间: 2016-1-12

项目GitHub: <https://github.com/wbond/package_control>

Simple
------

The simplest method of installation is through the Sublime Text console. The console is accessed via the ``ctrl+` `` shortcut or the `View > Show Console` menu. Once open, paste the appropriate Python code for your version of Sublime Text into the console.

**SUBLIME TEXT 3**

```
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

**SUBLIME TEXT 2**

```
import urllib2,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')
```

This code creates the Installed Packages folder for you (if necessary), and then downloads the Package Control.sublime-package into it. The download will be done over HTTP instead of HTTPS due to Python standard library limitations, however the file will be validated using SHA-256.

WARNING: Please do not redistribute the install code via another website. It will change with every release. Instead, please link to this page.

Manual
------

If for some reason the console installation instructions do not work for you (such as having a proxy on your network), perform the following steps to manually install Package Control:

1. Click the `Preferences > Browse Packages…` menu
2. Browse up a folder and then into the `Installed Packages/` folder
3. Download Package [Control.sublime-package](https://packagecontrol.io/Package%20Control.sublime-package) and copy it into the `Installed Packages/` directory
4. Restart Sublime Text

问题解决
--------

**问题：**安装完后无法显示 `Package Control` 菜单或执行代码后显示186789。

**解决：**点击 `Preferences > Settings - User`，找到 "ignored_packages" ，把它的值中的 "Package Control" 去掉，就能看到 `Package Control` 菜单了。
