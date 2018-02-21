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
  $ sudo systemctl start kibana.service
  $ sudo systemctl status kibana.service
  ```