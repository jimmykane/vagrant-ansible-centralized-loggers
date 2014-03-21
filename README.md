### Ansible Playbook for automate the setup and configuration of a centralized Rsyslog server with Logstash, Elasticsearch, Redis and Kibana.

This playbook is intended to be run against a clean server (not clients) that will be used as central logger. After the setup of the server, clients cat be instructed to redirect all logs to the central location.

**Platform**: Tested on **Debian 7 x64** / **CentOS 6.x x64**

**Disclaimer**: do not run this Playbook on a live production system!! Use a dedicated instance instead.

**Prerequisites**: At least 1GB Ram required. 2GB is better

**Logging Logic**: Clients => Rsyslog Tcp 514 => Logstash => Redis => Logstash => Elasticsearch => Kibana

![Picture](http://www.servermanaged.it/wp-content/uploads/2013/10/Setup-Logstash-Elasticsearch-Kibana.png)

### Preparation

1. Setup your target host in hosts

2. Add your custom domain in /etc/hosts on your local box. Example: 11.11.11.11 logger

### Variables

**usname** : username of the Apache user 

**domain** : domain name of Apache vhost. Example: logger

**pass** : password for Apache auth

### Use

`ansible-playbook site.yml `

use **--skip-tags** if you want to skip a role.

Et voila, your centralized logging server is up and running!

Browse **http://$domain/kibana-3.0.0milestone4/** and happy logging!

![Picture](http://www.elasticsearch.org/content/uploads/2013/08/BQIielHCAAAs2So.png)
Image credit: elasticsearch.org

See central-logs.yml for all tags available. Please note that tags must be launched in appearance order.

This is what the Playbook do:

1. Setup and configure Rsyslog to listen on tcp 514

2. Setup and configure Redis

3. Setup and configure Logstash

4. Setup and configure Elasticsearch, Install Open-Jdk

5. Setup and configure Apache and Kibana 3 with simple HTTP authentication

### TODO

Rsyslog-server role can be extended with TLS support. See http://www.rsyslog.com/doc/rsyslog_tls.html

### Credits

[Ansible](http://www.ansibleworks.com/)

[Logstash](http://www.logstash.net/)

[Elasticsearch](http://www.elasticsearch.org/)

[Kibana](http://www.elasticsearch.org/overview/kibana/)

[Redis](http://redis.io/)

[Ansible Fan Community](https://plus.google.com/u/0/communities/108222183653550371543)
