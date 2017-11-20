

# [Git代理设置](http://www.cnblogs.com/kaiux/p/6799242.html)

#### Problem

今天在使用的git的时候发现速度`clone`和`push`的速度都非常慢，折腾了一番之后，发现了如下的解决方式，还算有点效果。

#### 设置HTTP代理

如果你的代理是[SOCKS5](http://www.ccproxy.com/socks4-yu-socks5-de-qu-bie-jie-shao.htm)代理，那么你可以按照以下的方式设置

```
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

设置完成后在用户的主目录下可以看到如下的代码：

```
[http]
    proxy = socks5://127.0.0.1:1080
[https]
    proxy = socks5://127.0.0.1:1080
```

如何你想取消代理，那么输入如下的代码

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```

#### 设置SSH代理

我们也经常使用`SSH`来`clone`或者`push`项目，那么基于`SSH`的代理设置如下，首先在`~/.ssh/`中新建一个`config`文件，输入下面代码：

```
Host github.com
   HostName github.com
   User git
   ProxyCommand nc -v -x 127.0.0.1:1080 %h %p
```

#### 一些注意事项

- 作者使用的端口号是1080，读者请自行修改
- 如果代理的速度不如不使用代理，那么请关闭代理