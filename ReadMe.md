- name: Install Nginx
  hosts: rrobin, web1, web2
  become: true
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 86400

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start Nginx service
      systemd:
        name: nginx
        state: started
        enabled: yes
