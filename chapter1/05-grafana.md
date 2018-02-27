# Grafana 설치 및 환경구성

* 설치환경
    * RHEL 7.4
    * 참고자료: [Installing on RPM-based Linux (CentOS, Fedora, OpenSuse, RedHat)](http://docs.grafana.org/installation/rpm/)
---

#### 1. Grafana 다운로드 및 설치
  ```
  $ wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.6.3-1.x86_64.rpm
  $ sudo rpm -Uvh grafana-4.6.3-1.x86_64.rpm
  ```
#### 2. 환경설정
  * port 변경 (세미콜론 제거)
  ```
  $ sudo vi /etc/grafana/grafana.ini
  http_port = 5000
  root_url = http://localhost:5000
  ```
  
#### 3. 서비스 실행/확인


#### 4. 방화벽 오픈
  ```
  $ su -
  # firewall-cmd --zone=public --permanent --add-port=5000/tcp
  # firewall-cmd --reload
  ```

#### 4. Kibana 대시보드 확인
