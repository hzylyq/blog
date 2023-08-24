查询端口号对应的进程
netstat -anp | grep 端口号

端口状态
netstat -aptn | grep 3334

上传文件
scp ./portal.tgz  root@192.168.1.35:/home/lvchao

后台启动进程
nohup ./worker -env=PRESSURE &

ubuntu网络图标消失
sudo service NetworkManager stop
sudo rm /var/lib/NetworkManager/NetworkManager.state
sudo service NetworkManager start

dhclient ens33 网络错误

解压时间不对报错解决 tar -xvzf portal.tgz -m

grep 匹配多个条件
``` bash
cat admin.log |  grep -P '^(?=.*taskRun)(?=.*cbljlo4f6iful983g1p)'
```

k8s ---
kubectl exec -it "podName" /bin/bash

mysqldump -u lvchao -p -h rm-m5e8n214n083l36wjno.mysql.rds.aliyuncs.com green admin_routes > admin_routes.sql

mysql 查询重复元素
select employee_name,count(*) from employee group by employee_name having count(employee_name)>1;

set global  sort_buffer_size = 2097152*4;

linux查询公网ip
curl cip.cc

问题 vmware共享文件夹失效

```sheel
vmhgfs-fuse .host:/ /mnt/hgfs -o subtype=vmhgfs-fuse,allow_other
```

执行上面命令

ssh 开启密码登陆
PasswordAuthentication yes