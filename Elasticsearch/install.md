# Elasticsearch 설치하기

### 설치 환경
1. CentOS 6.7 84_64
2. Elasticsearch 7.13.1


## 설치 Command Line
```
# install Java JDK
yum install java-1.8.0-openjdk.x86_64

# download signing key
rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch

# create repo file
vi /etc/yum.repos.d/elasticsearch.repo

# paste repo configurations
[elasticsearch-7.x]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md

# install elasticsearch
yum install elasticsearch

# set elasticsearch to run on boot
sudo chkconfig --add elasticsearch
sudo chkconfig elasticsearch on
# lookup list
sudo chkconfig --list

# open port 9200 (for http) and 9300 (for tcp)
iptables -L -n
iptables -A INPUT -p tcp -m tcp --dport 9200 -j ACCEPT
iptables -A INPUT -p tcp -m tcp --dport 9300 -j ACCEPT
service iptables save

# restart server
service elasticsearch restart

# lookup connection
curl -X GET 'localhost:9200'

# check installed elasticsearch file
ls -al /usr/share/elasticsearch
ls -al /etc/elasticsearch/
ls -al /etc/init.d/elasticsearch

# if you want to check status
# service elasticsearch status
# else if you want to stop service
# service elasticsearch stop
```


## 외부 접속 허용하기
elasticsearch는 기본적으로 설치된 서버에서만 통신이 가능하게 설정되어있다.
```
[root@localhost elasticsearch]# netstat -an | grep 9200
[root@localhost elasticsearch]# netstat -an|grep 9200
tcp        0      0 ::ffff:127.0.0.1:9200       :::*                        LISTEN      
tcp        0      0 ::1:9200                    :::*                        LISTEN      
```

TODO 작성 마저 하기
