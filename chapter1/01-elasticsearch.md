# Elastic Search 설치 및 환경구성

* 설치환경
    * RHEL 7.4
    * 참고자료: [Install Elasticsearch](https://www.elastic.co/guide/en/beats/libbeat/6.1/elasticsearch-installation.html)
---

1. 사용자 추가 및 권한 설정
  * 사용자 추가
  ```
  # useradd infra -m -d /home/infra
  # passwd infra
  ```
  * sudoer 등록
  ```
  # visudo
  ## Allow root to run any commands anywhere
  root    ALL=(ALL)       ALL
  infra     ALL=(ALL)       ALL
  ```
2. DNS 설정
  ```
  # vi /etc/resolv.conf
  nameserver x.x.x.x
  ```
3. JDK 설치(version 8)
  ```
  # su - infra
  $ sudo yum install java-1.8.0-openjdk-devel
  ```
4. JAVA_HOME 환경변수 설정
  * 환경파일에 JAVA_HOME 추가 (JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-1.b12.el7_4.x86_64")
  
    ```
    $ sudo vi ~/.bashrc
    ## Java Home
    export JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.111-2.b15.el7_3.x86_64"
    
    $ source ~/.bashrc

    $ echo $JAVA_HOME
    /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.111-2.b15.el7_3.x86_64
    ```
5. Default JDK 설정 (2개 이상 설치 된 경우)
  * 설치 목록 확인 및 변경
  ```
  $ sudo yum install alternatives
  ```
  * default 확인
  ```
  $ sudo /usr/sbin/alternatives --config java
      Selection Path Priority Status
    ------------------------------------------------------------
    0 /usr/lib/jvm/java-8-oracle/jre/bin/java 1081 auto mode
    1 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java 1081 manual mode
    * 2 /usr/lib/jvm/java-8-oracle/jre/bin/java 1081 manual mode
  ```

6. Elastic Search 다운로드 및 설치
  ```
  $ curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.1.3.rpm
  $ sudo rpm -i elasticsearch-6.1.3.rpm
  ```
7. 방화벽 오픈
  ```
  $ su -
  # firewall-cmd --zone=public --permanent --add-port=9200/tcp
  # firewall-cmd --reload
  ```
8. Elastic Search 서비스 실행/확인
  ```
  $ sudo systemctl start elasticsearch
  $ sudo systemctl status elasticsearch
  $ curl http://127.0.0.1:9200
  $ sudo tail -100f /var/log/elasticsearch/elasticsearch.log
  ```
