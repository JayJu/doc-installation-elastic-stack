# Kibana 설치 및 환경구성

* 설치환경
    * RHEL 7.4
    * 참고자료: [Install Kibana](https://www.elastic.co/guide/en/beats/libbeat/6.1/kibana-installation.html)
---

#### 1. Kibana 다운로드 및 설치
  ```
  $ curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-6.1.3-x86_64.rpm
  $ sudo rpm -i kibana-6.1.3-x86_64.rpm
  $ sudo systemctl daemon-reload
  $ sudo systemctl enable kibana.service  
  ```
#### 2. 환경설정
  ```
  $ cd /etc/kibana
  $ sudo vi kibana.yml
  server.port: 5601 커멘트제거
  server.host: "10.x.x.x" 커멘트제거 후 IP 등록
  ```
#### 3. 방화벽 오픈
  ```
  $ su -
  # firewall-cmd --zone=public --permanent --add-port=5601/tcp
  # firewall-cmd --reload
  ```
#### 4. Logstash 서비스 실행/확인
  ```
  $ sudo systemctl start kibana.service
  $ sudo systemctl status kibana.service
  ```
