# Systemd vs Supervisord 

> 뜬금없이 Systemd와 Supervisord를 비교하고 싶어졌다.
> 사실 Supervisord는 직접 써본 적은 없고, 5년차 때쯤 어떨 때 쓴다 정도로 들어본 적이 있을 뿐이다.

## 설계 목적
- systemd: 전체 시스템의 부팅 프로세스와 서비스 관리를 위한 완전한 init 시스템
- supervisord: 프로세스 관리와 모니터링에 특화된 도구, 커널 수준이 아닌 일반 프로그램으로 작동

## 설치 방식
- systemd: 대부분의 최신 Linux 배포판에 기본으로 탑재
- supervisord: 외부 도구로 설치하며, 시스템 부팅 과정의 일부가 아니라 일반 프로세스로 실행

## 설정 관리
- systemd: 설정 파일 문법이 더 복잡하지만 기능이 다양함
- supervisord: 설정이 비교적 단순하고 직관적

## 주요 기능
- systemd: 서비스 관리, 소켓 활성화, 타이머(cron과 유사), 로깅, 의존성 관리 등 광범위한 기능 제공
- supervisord: 프로세스 모니터링, 재시작, 로그 관리에 집중 

## 시스템 권한
- systemd: 시스템 레벨에서 작동하며 root 권한이 필요
- supervisord: 사용자 권한으로도 실행 가능


## 선택 기준 
- systemd
	- 시스템 전체 서비스로 실행해야 하는 경우
	- 시스템 부팅 시 자동 시작이 필요한 경우
	- 다른 systemd 서비스와의 의존성 관리가 필요한 경우
- supervisord
	- 특정 사용자의 프로세스 관리가 필요한 경우
	- 여러 유사한 프로세스를 그룹으로 관리해야 하는 경우
	- systemd가 없는 오래된 시스템에서 사용하는 경우



## 실제 내가 경험한 사례 기록

### 배경
docker compose로 실행되고 있는 컨테이너의 stdout 로그를 watch(`-f`) 하면서 특정 `ERROR` 패턴이 발견되는 경우, 슬랙 알림을 보내는 간단한 Bash 스크립트를 만들었다.  
그리고 `nohup`으로 백그라운드 실행하게 하고 터미널 세션을 종료했다.  

하지만 종종 컨테이너 이미지 교체에 따른 컨테이너의 재시작으로 인해 해당 로그 스트림이 끊기게 되면 Bash 스크립트의 동작도 함께 중단되게 되었다.  

이 문제점을 해결하기 위해 해당 프로세스를 systemd 서비스로 등록하여 예기치 않게 중단되었을 때 자동으로 재시작하도록 설정했다.  

### 진행 과정

1. Bash 스크립트에 실행 권한 부여
```shell
$ chmod +x /path/to/script.sh
```

2. systemd 서비스 파일 생성
```shell
$ sudo vi /etc/systemd/system/docker-logger.service
```

3. 서비스 파일에 내용 추가
```plaintext
[Unit]
Description=Docker Log Collector
After=docker.service
Requires=docker.service

[Service]
Type=simple
ExecStart=/path/to/script.sh
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

4. systemd 리로드, 서비스 활성화 및 시작
```shell
# daemon-reload는 systemd가 서비스 설정 파일들을 다시 읽도록 하는 것으로, 실행 중인 서비스의 동작을 중단시키지 않음
$ sudo systemctl daemon-reload

$ sudo systemctl enable docker-logger.service
$ sudo systemctl start docker-logger.service
```

5. 서비스 상태 확인
```shell
$ sudo systemctl status docker-logger.service
```
