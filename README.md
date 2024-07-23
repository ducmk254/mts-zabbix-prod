##### Step 1: clone repo

##### Step 2: trong thư mục chính của repo, tạo file .env
Ví dụ:  
MYSQL_USER=zabbix-user  
MYSQL_DATABASE=zabbixdb  
MYSQL_PASSWORD=MktLocal@2025!@!  
MYSQL_ROOT_PASSWORD=MktLocal@2025!@!  
USER_ADMIN_ZABBIX=zabbix  

##### Step 3: docker compose up -d

##### Step 4: Truy cập http://docker_host_ip:8087 ( ip 192.168.56.222 )
Chờ khoảng 3p để hệ thống boot vào trang login  
user: Admin/zabbix  

##### Step 5: trên docker host, cài đặt zabbix agent 2  
Link tham khảo : https://www.zabbix.com/download?zabbix=7.0&os_distribution=centos&os_version=9&components=agent_2&db=&ws=

- chỉnh sửa repo epel :  
vi /etc/yum.repos.d/epel.repo  
thêm dòng sau vào cuối file:  
excludepkgs=zabbix*  
- cài zabbix repo :  
rpm -Uvh https://repo.zabbix.com/zabbix/7.0/centos/9/x86_64/zabbix-release-7.0-4.el9.noarch.rpm  
dnf clean all  
- cài zabbix agent 2  
dnf install -y zabbix-agent2 zabbix-agent2-plugin-*  
systemctl restart zabbix-agent2  
systemctl enable zabbix-agent2  

##### Step 6: chỉnh sửa host Zabbix server với IP là ip của docker host ( 192.168.56.222)
        chỉnh sửa template là Linux by agent active và Zabbix server health  
