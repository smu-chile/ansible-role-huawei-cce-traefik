Huawei CCE Setup
=========

Role to setup a bastion to connect with a cce cluster



Role Variables
--------------

```
      LB_ID: id de Balanceador, se obtiene de terraform
      LB_VIP_SUBNET_ID: id de subnet de balanceador, se obtiene de terraform
      LB_PUBLIC_IP: IP publica de balanceador
      TRAEFIK_HOSTNAME: hostname donde se alojara Traefik, esto crea un registro A, apuntando a la Ip del balanceador:
      TRAEFIK_ADMIN_HOSTNAME: hostname donde se alojara el Admin Manager de Traefik, esto crea un registro CNAME apuntando a TRAEFIK_HOSTNAME
      TRAEFIK_ADMIN_PASSWD: archivo passwd para autenticación del admin de traefik, se crea utilizando passwd.
```

Example Playbook
----------------


```
- hosts: all
  become: no
  remote_user: "root"

# Uncomment "aws-eks-setup" role only if you are upgrading the cluster
  roles:
    - role: ansible-role-huawei-cce-traefik
      LB_ID: "{{ lookup('env', 'LB_ID') }}"
      LB_VIP_SUBNET_ID: "{{ lookup('env', 'LB_SUBNET_ID') }}"
      TRAEFIK_HOSTNAME: "{{ lookup('env', 'TRAEFIK_HOSTNAME') }}"
      LB_PUBLIC_IP: "{{ lookup('env', 'LB_PUBLIC_IP') }}"
      TRAEFIK_ADMIN_HOSTNAME: "{{ lookup('env', 'TRAEFIK_ADMIN_HOSTNAME') }}"
      TRAEFIK_ADMIN_PASSWD: "{{ lookup('env', 'TRAEFIK_ADMIN_PASSWD') }}"

```

License
-------

BSD

Author Information
------------------

- [César vergara](mailto:cvergarae@smu.cl)

