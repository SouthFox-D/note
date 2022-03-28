title:: ## xargs 命令

- https://www.runoob.com/linux/linux-comm-xargs.html
- 例子：使用 `xargs` 拿到运行中的 `docker` 容器的 `IP` 并挨个 `ping`。
	- ```shell
	  docker ps -q | \
	  xargs docker inspect --format='{{>NetWorkSettings.IPAddress}}' | \
	  xargs -l1 ping -c1
	  ```