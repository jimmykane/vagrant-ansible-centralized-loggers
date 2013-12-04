### Ansible Playbook for automate the setup and configuration of a centralized Rsyslog server with Logstash, Elasticsearch, Redis and Kibana.

**Platform**: Tested on **Debian 7 x64** / **CentOS 6.4 x64**

**Disclaimer**: do not run this Playbook on a live production system!! Use a dedicated instance instead.

**Prerequisites**: At least 1GB Ram required. 2GB is better

**Logging Logic**: Clients => Rsyslog Tcp 514 => logstash2redis => Redis => redis2elasticsearch => Elasticsearch => Kibana

![Picture](http://www.servermanaged.it/wp-content/uploads/2013/10/Setup-Logstash-Elasticsearch-Kibana.png)

### Preparation

1. Setup your target host in hosts

2. Customize Logstash filters (if needed) in roles/logstash/templates/filters_log2redis.conf.j2

3. Add your custom domain in /etc/hosts on your local box. Example: 11.11.11.11 logger

### Variables

**usname** : username of the Apache user 

**domain** : domain name of Apache vhost. Example: logger

**pass** : password for Apache auth

**myip**: ip address of the client authorized to connect at http://$domain/kibana-3.0.0milestone4/

### Use

`ansible-playbook site.yml --extra-vars="usname= domain= pass= myip="`

use **--skip-tags** if you want to skip a role, shorewall for example: --skip-tags=shorewall

Et voila, your centralized logging server is up and running!

Browse **http://$domain/kibana-3.0.0milestone4/** and happy logging!

![Picture](http://www.elasticsearch.org/content/uploads/2013/08/BQIielHCAAAs2So.png)
Image credit: elasticsearch.org

At this point you can authorize some clients in roles/shorewall/templates/rules.j2 and reload Shorewall.

You may want to setup individual roles step by step too. Example:

`ansible-playbook central-logs.yml -t rsyslog-server`

See central-logs.yml for all tags available. Please note that tags must be launched in appearance order.

This is what the Playbook do:

1. Setup and configure Rsyslog to listen on tcp 514

2. Setup and configure Redis

3. Setup and configure two Logstash instances (managed by Supervisord)

4. Setup and configure Elasticsearch with a simple Logstash mapping. Install Open-Jdk

5. Setup and configure Supervisord to manage Logstash instances

6. Setup and configure Apache and Kibana 3 with simple HTTP authentication

7. Setup and configure Shorewall (optional but recommended)

### TODO

Add support for Statsd and Librato

Shorewall role for CentOS

Rsyslog-server role can be extended with TLS support. See http://www.rsyslog.com/doc/rsyslog_tls.html


### PS

At some point in future you will need to update Elasticsearch and Logstash version in vars/default.yml

If you like this project feel free to report a bug or contribute with a pull requests!

### Links

[Ansible](http://www.ansibleworks.com/)

[Logstash](http://www.logstash.net/)

[Elasticsearch](http://www.elasticsearch.org/)

[Kibana](http://www.elasticsearch.org/overview/kibana/)

[Redis](http://redis.io/)

[Supervisord](http://supervisord.org/)

[Ansible Fan Community](https://plus.google.com/u/0/communities/108222183653550371543)
