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
