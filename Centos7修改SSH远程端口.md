# Centos7

## 修改ssh端口

1. 编辑ssh配置文件

   ```sh
   vi /etc/ssh/sshd_config vi /etc/ssh/sshd_config 
   ```

2. 修改端口

   ```sh
   Port 222 # 这里修改成自己设置的端口
   #Port 22
   ```

3. 添加ssh监听端口

   ```sh
   semanage port -a -t ssh_port_t -p tcp 222
   ```

4. 查看端口是否添加成功

   ```sh
   semanage port -l|grep ssh
   ```

   结果如下

   ```sh
   ssh_port_t                     tcp      222, 22
   ```

5. 将刚才修改的端口添加到防火墙规则

   ```sh
   firewall-cmd --zone=public --add-port=222/tcp --permanent  # 这里222修改成自己设置的端口
   ```

6. 重新加载防火墙策略

   ```sh
   firewall-cmd --reload
   ```

7. 重启SSH服务和防火墙，最好也重启下服务器：

  ```sh
  systemctl restart sshd
  
  systemctl restart firewalld.service
  
  shutdown -r now
  ```

8. 重新ssh连接测试
