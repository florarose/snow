## 一、nginx基本定义

   - 高性能的http和反向代理Web的服务器，同时也提供IMAP/POP3/SMTP服务;
   - 一款轻量级的web服务器/反向代理服务器及电子邮件（IMAP/POP#）代理服务器;
   - 稳定、丰富的功能集、示例配置文件和低系统资源的消耗;
   - 特点是占有内存少，并发能力强（在同类型的网页服务器中表现较好）。
## 二、Nginx 优劣
### 优点：
   -  服务器
       1. Nginx作为负载均衡服务：Nginx 既可以在内部直接支持 Rails 和 PHP 程序对外进行服务，也可以支持作为 HTTP代理服务对外进行服务。
          Nginx采用C进行编写，不论是系统资源开销还是CPU使用效率都比 Perlbal 要好很多。
       2.  处理静态文件，索引文件以及自动索引;打开文件描述符缓冲。
       3. 无缓存的反向代理加速，简单的负载均衡和容错。
       4. FastCGI，简单的负载均衡和容错。
       5. 模块化的结构。包括 gzipping, byte ranges, chunked responses,以及 SSI-filter 等 filter。如果由 FastCG或其它代理服务器处理单页中存在的多个 SSI，则这项处理可以并行运行，而不需要相互等待。
       6. 支持 SSL 和 TLSSNI。
## 三、详细解释
   -  nginx有一个主进程和几个工作进程。主进程的主要目的是读取和评估配置，并维护工作进程。工作进程会对请求进行实际处理。
      nginx采用**基于事件的模型和依赖于操作系统的机制**来有效地在工作进程之间分发请求。工作进程数在配置文件中定义，可以针对给定配置进行修复，也可以自动调整为可用CPU内核数。
   -  nginx及其模块的工作方式在配置文件中确定。默认情况下，配置文件被命名nginx.conf 并放在目录 /usr/local/nginx/conf中 /etc/nginx，或 /usr/local/etc/nginx。
   ### 启动，停止和重新加载配置
   
   -   nginx -s stop - 快速关机
   -   nginx -s quit - 优雅的关机
   -   nginx -s reload - 重新加载配置文件
   -   nginx -s reopen - 重新打开日志文件
   -   获取所有正在运行的nginx列表，     ps -ax | grep nginx
   -   删除相应的进程 nginx -s QUIT 1628
   ### 静态文件的访问
   
  - 样例代码
      ```
      服务器{
            地点 / {
                root / data / www;
            }
            location / images / {
                根/数据;
            }
        }
      ```  
  - 如果存在多个匹配location块，则nginx选择具有最长前缀的块。location上面的块提供长度为1的最短前缀，因此只有当所有其他location 块都无法提供匹配时，才会使用此块。
   ### 设置简单的代理服务器
  - 样例代码
         ```
             服务器{
                 地点 / {
                     proxy_pass http：// localhost：8080;
                 }
             
                 location / images / {
                     根/数据;
                 }
             }
         ``` 
        
  ## 四、nginx 的使用
  
   - 负载均衡服务器
       >请求转发，按照一定的策略转发，降低单个服务器的压力；避免服务器单节点故障；
   - 反向代理服务器
       >正向代理： vpn, 客户端通过vpn访问谷歌服务器，vpn代理了客户端；
       
       >反向代理： 固定电话，拨打着打通后，接到总机，总机负责转接到对应的接听者。 总机代理的就是接听者。
   - 静态代理 
       > 目前通常用作静态处理服务器，实现动静分离；
   - 限流
       >基于漏桶算法实现的,在高并发的场景下非常实用
   - 缓存
   - 黑白名单
   
   ----
   ##  五、负载均衡策略
   
   - 轮询
   - 加权轮询
   - ip_hash
   - 随机
   - least_conn(最小连接数)
   
   
   ## 备注
   - 一 日志文件
      >access.log，记录每个HTTP请求信息
      
      >error.log，记录Nginx运行中的错误，用于排错
   