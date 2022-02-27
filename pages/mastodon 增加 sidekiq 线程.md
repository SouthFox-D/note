- 参考官方文档：[https://docs.joinmastodon.org/admin/scaling/](https://docs.joinmastodon.org/admin/scaling/)
- `docker-compose` 如下：
	- ```docker-compose
	    sidekiq:
	      image: tootsuite/mastodon
	      restart: always
	      env_file: .env.production
	      environment:
	        - DB_POOL=10
	      command: bundle exec sidekiq -c 10
	      depends_on:
	        - db
	        - redis
	      networks:
	        - external_network
	        - internal_network
	      volumes:
	        - ./public/system:/mastodon/public/system
	  
	  
	  ```
	- 主要是增加 `DB_POOL` 数量，然后修改 `sidekiq` 启动参数(如上修改 `-c` 参数将线程设置为 `10`)。
	- 之后重载容器即可：
	- ```shell
	  docker-compose down #删除镜像
	  docker-compose up -d #重新创建并后台启动镜像
	  ```
- 之后在 `https://实例地址/sidekiq` 的 `Busy` 页面应该能看到 `Threads` 显示为 `10`。