# SSL certs expiry

## Template for controlling the expiration of SSL certificates for many sites. Worked on zabbix-agent2 and zabbix-server 6.0.

How it's work:

1) Import template from file ssl_certs_expiry.yaml

1) Create next json file with sites list for SSL expiry monitoring. As example name this file /etc/zabbix/sites.json:
    ```sh
    [
        {"{#SITE}":"foo.bar"},
        {"{#SITE}":"another.foo.bar"},
        {"{#SITE}":"another.site.org"},
        {"{#SITE}":"test.domain.com"},
        {"{#SITE}":"foo2.bar"}
    ]
    ```
2) Add zabbix-agent user parameter with next file /etc/zabbix/zabbix_agent2.d/userparameters.conf:

    ```sh
    UserParameter=list.sites,cat /etc/zabbix/sites.json
    ```
3) Restart zabbix-agent2 daemon
    ```sh
    systemctl restart zabbix-agent2
    ```
4) Attach template to this host



