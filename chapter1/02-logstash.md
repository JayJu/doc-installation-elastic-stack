# Logstash 설치 및 환경구성

* 설치환경
    * RHEL 7.4
    * 참고자료: [Install Logstash (Optional)](https://www.elastic.co/guide/en/beats/libbeat/6.1/logstash-installation.html)
---

1. Logstash 다운로드 및 설치
  ```
  $ curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-6.1.3.rpm
  $ sudo rpm -i logstash-6.1.3.rpm
  ```
2. 환경설정
  * Input 으로 beats 를 output 으로 elasticsearch 지정하도록 설정
3. 방화벽 오픈
  ```
  $ su -
  # firewall-cmd --zone=public --permanent --add-port=5044/tcp
  # firewall-cmd --reload
  ```
4. Elastic Search 서비스 실행/확인
