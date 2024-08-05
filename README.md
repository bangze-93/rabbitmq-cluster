# Install RabbitMQ Cluster (Docker) using Ansible on Ubuntu 20
### Topology
![Screenshot from 2024-08-05 21-38-30](https://github.com/user-attachments/assets/3be31347-582b-4fe0-a6c2-d9921c4b7117)
### Adjust with your env
- #### <i> vars/all.yaml </i>
```
---
rabbitmq_version: 3.13.0-management-alpine
rabbitmq_user: admin
rabbitmq_pass: MF85CtQvXDIP24Yh
rabbitmq_vol_dir: /opt/rabbitmq

haproxy_version: 2.8
haproxy_user: admin
haproxy_pass: EQEN5rj42pIW8TfQ
haproxy_rabbitmq_amqp_listen_port: 5672
haproxy_rabbitmq_mgmt_listen_port: 8080

keepalived_vip: 192.168.90.40
...
```
- #### <i> inventory/hosts </i>
```
[keepalived]
master ansible_host=192.168.90.41
slave  ansible_host=192.168.90.42

[rabbitmq]
rabbitmq01 ansible_host=192.168.90.43
rabbitmq02 ansible_host=192.168.90.44
rabbitmq03 ansible_host=192.168.90.45

[all:vars]
ansible_user=user
ansible_ssh_pass=P4s5word
ansible_become_password=P4s5word
```
### Run playbook
```
ansible-playbook playbook.yaml
```
### Access RabbitMQ management dashboard
http://192.168.90.40:8080/
![Screenshot from 2024-08-05 21-37-46](https://github.com/user-attachments/assets/f5606d09-c076-41e6-8138-47dfe333699f)

### Access HAProxy status
http://192.168.90.40:8000/stats
![Screenshot from 2024-08-05 21-35-46](https://github.com/user-attachments/assets/c1342daf-627d-410a-9926-6cfb67f7a608)

