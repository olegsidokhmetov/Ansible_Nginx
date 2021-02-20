# Ansible_Nginx

Install nginx service with Ansible

Playbook file
root@ip-172-31-11-19:/etc/ansible/playbooks# nano nginx.yaml
---
- name: Configure nginx
  hosts: webservers
  become: yes

  tasks:

    - name: install nginx
      apt: name=nginx update_cache=yes

    - name: restart nginx
      service: name=nginx state=restarted


Log of installation
root@ip-172-31-11-19:/etc/ansible/playbooks# ansible-playbook nginx.yaml

PLAY [Configure nginx] *************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************
ok: [15.188.146.84]

TASK [install nginx] ***************************************************************************************************************************************
ok: [15.188.146.84]

TASK [restart nginx] ***************************************************************************************************************************************
changed: [15.188.146.84]

PLAY RECAP *************************************************************************************************************************************************
15.188.146.84              : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0



Check status nginx on server 15.188.146.84 
root@ip-172-31-2-64:/usr/share/nginx/html# systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2021-02-20 19:24:02 UTC; 2min 0s ago
       Docs: man:nginx(8)
    Process: 18583 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 18594 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 18595 (nginx)
      Tasks: 2 (limit: 1160)
     Memory: 3.1M
     CGroup: /system.slice/nginx.service
             ├─18595 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             └─18596 nginx: worker process

Feb 20 19:24:02 ip-172-31-2-64 systemd[1]: nginx.service: Succeeded.
Feb 20 19:24:02 ip-172-31-2-64 systemd[1]: Stopped A high performance web server and a reverse proxy server.
Feb 20 19:24:02 ip-172-31-2-64 systemd[1]: Starting A high performance web server and a reverse proxy server...
Feb 20 19:24:02 ip-172-31-2-64 systemd[1]: Started A high performance web server and a reverse proxy server.


