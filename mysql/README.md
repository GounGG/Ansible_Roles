## install
检测/usr/local/mysql目录是否存在，如果存在，则skip跳过安装过程。

## cluster
当主机注册了id变量后，则会添加集群的基础配置，如:server_id
```shell
cat host_vars/db1 
---
id: 1

cat host_vars/db2
---
id: 2
```

j2模板
```jinja2
{% if id is none %}
{% else %}
server-id={{ id }}
replicate-wild-ignore-table=mysql.%
replicate-wild-ignore-table=test.%
replicate-wild-ignore-table=information.%
{% endif %}
```
