# Go拉取依赖的issue


> go: github.com/dnephin/govet@v0.0.0-20171012192244-4a96d43e39d3: invalid version: git fetch -f origin refs/heads/*:refs/heads/* refs/tags/*:refs/tags/* in /Users/max/myGo/pkg/mod/cache/vcs/3805abc374bbc28ca24911d616875e58201c4d7d8ef1b4525356b9dfb85aeb6b: exit status 128: 	fatal: unable to access 'https://github.com/dnephin/govet/': Failed to connect to github.com port 443 after 16923 ms: Operation timed out

> go: github.com/dnephin/govet@v0.0.0-20171012192244-4a96d43e39d3: invalid version: git fetch -f origin refs/heads/*:refs/heads/* refs/tags/*:refs/tags/* in /Users/max/myGo/pkg/mod/cache/vcs/3805abc374bbc28ca24911d616875e58201c4d7d8ef1b4525356b9dfb85aeb6b: exit status 128:
	fatal: unable to access 'https://github.com/dnephin/govet/': Failed to connect to github.com port 443 after 75007 ms: Operation timed out


1. 保证ping github.com -> sudo vim /private/etc/hosts 
2. 依赖拉取success，但import依赖报红 -> 使用
https://ipaddress.com/website/github.com
**github.com** 
140.82.112.3 github.com
![](https://raw.githubusercontent.com/hi-Ernest/imgbed/master/Preferences.jpg)
￼
https://goproxy.cn,direct