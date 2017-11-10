目前支持Nginx，MySQL，Postgresql等服务！

模板文件中有部分变量，使用到了主机变量：
state
interface
virtual_router_id
VIP

服务判断依据：
组名：
[webservers]     nginx服务
[database]       Mysql服务
[pgsql]        postgresql服务