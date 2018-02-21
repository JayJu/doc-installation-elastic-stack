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
  ```
  $ cd /etc/logstash/conf.d
  $ sudo vi beats.conf
  ```
  * 아래 내용 입력
  ```
  input {
    beats {
    port => 5044
    }
  }
  output {
    elasticsearch {
      hosts => "localhost:9200"
      manage_template => false
      index => "%{[@metadata][beat]}-%{[@metadata][version]}-%{+YYYY.MM.dd}"
      document_type => "%{[@metadata][type]}"
    }
  }
  ```
  * Beats input 플러그인 업데이트
  ```
  $ cd /usr/share/logstash
  $ sudo ./bin/logstash-plugin update logstash-input-beats
  ```
3. 방화벽 오픈
  ```
  $ su -
  # firewall-cmd --zone=public --permanent --add-port=5044/tcp
  # firewall-cmd --reload
  ```
4. Logstash 서비스 실행/확인
  ```
  $ sudo systemctl start logstash
  $ sudo systemctl status logstash
  $ cd /var/log/logstash
  $ tail -100f ./logstash-plain.log
  $ netstat -anp |grep LISTEN|grep 5044
  ```
