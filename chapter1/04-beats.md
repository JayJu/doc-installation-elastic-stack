# Beats (Metricbeat) 설치 및 환경구성

* 설치환경
    * RHEL 6.6
    * 참고자료: [Getting started with Metricbeat](https://www.elastic.co/guide/en/beats/metricbeat/6.1/metricbeat-getting-started.html)
---

#### 1. Metricbeat 다운로드 및 설치 - 클라이언트에 설치
  ```
  $ curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-6.1.3-x86_64.rpm
  $ sudo rpm -vi metricbeat-6.1.3-x86_64.rpm
  ```
#### 2. 환경설정
  * OUTPUT 설정 - Kibana와 Logstach 로 Metric 정보 전송하도록 host:port 정보 입력
  ```
  $ cd /etc/metricbeat/
  $ sudo vi metricbeat.yml
  setup.kibana:
  host: "10.x.x.x:5601"
  output.logstash:
  hosts: ["10.x.x.x:5044"]
  ```
  * Module Enable
  ```
  $ cd /etc/metricbeat/modules.d
  $ sudo mv system.yml.disabled system.yml
  ```
  * Kibana Dashboard Setup
  ```
  sudo metricbeat setup --dashboards
  ```
#### 3. Logstash 서비스 실행/확인
  ```
  $ sudo service metricbeat start (6.6 이라 systemd 사용불가)
  $ sudo service metricbeat status
  $ sudo tail -20f /var/log/metricbeat/metricbeat
  ```
  
#### 4. Kibana 대시보드 확인
![](/chapter1/img/kibana-dashboard.jpg)