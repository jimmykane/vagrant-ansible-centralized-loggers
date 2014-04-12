Vagrant Ansible Centralized Loggers
======



Vagrant - Ansible provisioned centralized Rsyslog server with Logstash, Elasticsearch, Redis and Kibana.
----

**Platform**: Tested on **Ubuntu Saucy x64** / **CentOS 6.x x64**

**Prerequisites**: At least 1GB Ram required. 2GB is better

**Logging Logic**: Clients => Rsyslog Tcp 514 => Logstash => Redis => Logstash => Elasticsearch => Kibana

![Picture](http://www.servermanaged.it/wp-content/uploads/2013/10/Setup-Logstash-Elasticsearch-Kibana.png)


Install
--------


- Install [Vagrant](https://www.vagrantup.com/downloads.html)

- Clone this repo: ```git clone https://github.com/jimmykane/vagrant-ansible-centralized-loggers.git```

- Get into it ```cd vagrant-ansible-centralized-loggers```

- Do ```vagrant up```

- Wait until provisioning is done

- Visit ```192.168.33.11/kibana``` with your favourite browser. Username is: ```myuser``` and pass is ```mypass```

You are all setup with the latest Ubuntu Saucy, Rsyslog, Redis, ElsticSearch, Logstash, Kibana.


Customization
-----

- Go to ```/group_vars/all ``` and set the correct settings for you. Eg timezone or what else is needed. 
Further instruction on how to go on production will come soon. 
- Setup your target host in hosts
- Add your custom domain in ```/etc/hosts``` on your local box. Example: ```192.168.33.11 logger.dev```

### Variables

 -  **apt_valid_cache_time**: How often to refresh apt-cache. Default 6hours (21600s)
 -  **locale/timezone**: The locale and timezone for the server
 -  **usname** : username of the Apache user.
 -  **domain** : domain name of Apache vhost. Example: logger
 -  **pass** : password for Apache auth


TODO
----
- Add support for Graylog2
- User management
- Ansible-Pull crons
- Remove unused and untested hosts inventory and replace it with a better structure
- Regarding the above 2 structures: dev and production


### Credits

[Ansible](http://www.ansibleworks.com/)

[Logstash](http://www.logstash.net/)

[Elasticsearch](http://www.elasticsearch.org/)

[Kibana](http://www.elasticsearch.org/overview/kibana/)

[Redis](http://redis.io/)

[Ansible Fan Community](https://plus.google.com/u/0/communities/108222183653550371543)

[Ansible Logstash by Valentino Gagliardi](https://github.com/valentinogagliardi/ansible-logstash)