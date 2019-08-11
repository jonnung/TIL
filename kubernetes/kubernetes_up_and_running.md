# 도서 리뷰 - 쿠버네티스 시작하기

Link: http://www.yes24.com/Product/Goods/61335395
Tags: kubernetes

![](http://image.kyobobook.co.kr/images/book/xlarge/733/x9791161751733.jpg)

# 목차

- [x]  1장. 쿠버네티스 소개
- [x]  2장. 컨테이너 생성과 실행
- [x]  3장. 쿠버네티스 클러스터 배포
- [x]  4장. 일반적인 `kubectl` 명령
- [x]  5장. 포드
- [x]  6장. 라벨과 애노테이션
- [ ]  7장. 서비스 탐색
- [ ]  8장. 레플리카세트
- [ ]  9장. 데몬세트
- [ ]  10장. 잡
- [ ]  11장. ConfigMap과 시크릿
- [ ]  12장. 디플로이먼트
- [ ]  13장. 스토리지 솔루션과 쿠버네티스 연계
- [ ]  14장. 실제 애플리케이션 배포
- [ ]  부록 A. 라즈베리파이 쿠버네티스 클러스터 구축

# 1장. 쿠버네티스 소개

## ▶︎ 컨테이너와 쿠버네티스를 사용하는 이점

### #속도

속도는 시간당이나 일별로 제공할 수 있는 기능의 수가 아닌, 높은 가용성으로 서비스를 유지하며 제공할 수 있는 항목의 수로 측정한다.

컨테이너와 쿠버네티스는 가용성을 확보한 상태에서 작업을 빨리 할 수 있는 도구를 제공한다.

핵심 개념은 불변성(immutablility), 선언형 설정(declarative configuration), 온라인 자가 치유 시스템(online self-healing system)으로 서로 연관되어 소프트웨어의 안정성을 유지하며 배포 속도를 획기적으로 향상한다.

### #불변의 가치

불변형 인프라(immutable infrastructure)에서는 시스템에 아티팩트(artifact)가 발생하더라도 사용자의 수정을 통해 변경하지 않는다.

불변형 시스템에서는 일련의 증분 업데이트와 변경이 아닌, 완전하고 새로운 이미지가 생성되고 단 한 번의 실행으로 이 이미지를 새로운 버전의 이미지로 교체할 수 있다.

아티팩트(artifact)의 생성과 생성 시 방법에 대한 기록을 토대로 새로운 버전에서 변경된 부분에 오류가 있는 경우 변경된 부분과 함께 해결 방법을 쉽고 명확하게 확인할 수 있다.

또한 기존 이미지를 수정하는 것보다 새로운 이미지를 만들면 기존 이미지를 유지할 수 있기 때문에 오류 발생 시 즉시 되돌릴 수 있다는 장점이 있다.

### #선언형 설정

쿠버네티스에 포함된 구성요소는 요구하는 시스템 상태를 나타내는 선언형 설정 객체(declarative configuration object)다. 

실제 상태와 요구 상태를 일치 시켜주는 것이 쿠버네티스의 역할이다.

대비되는 명령형 설정(imperative configuration)은 동작을 정의하는 반면, 선언형 설정은 상태를 정의한다.

선언형 설정은 실제 상태를 기술하고 있으므로 해석을 위한 실행이 필요없다. 설정의 영향을 구체적으로 선언하고 실행 이전에 해석하므로 오류 발생 가능성이 더 적다. 

### #자가 치유 시스템

요구하는 상태 설정을 받으면 한번에 현재 상태를 요구된 상태와 일치 시키려고 하지 않는다. 오히려 현재 상태를 요구된 상태로 일치 시키려고 끊임없이 확인한다. 

## ▶︎ 서비스와 팀의 확장성

쿠버네티스는 분리된 아키텍처(decoupled architecture)를 지향한다.

### #분리

...

### #쉬운 애플리케이션 및 클러스터 확장

불변적인 선언적 속성으로 서비스를 쉽게 확장할 수 있다. 단순히 복제본을 증가 시키려면 선언형 설정에 포함되어 있는 숫자만 변경하면 쿠버네티스가 알아서 한다. (클러스터 내부에 가용한 자원이 있다는 가정하에)

컨테이너는 애플리케이션을 머신 세부사항과 분리하므로 새로운 자원(머신)을 클러스터에 추가하기만 하면 된다. 이 작업은 몇 가지 명령으로 가능하다.

### #마이크로서비스를 통한 개발 팀 확장

...

### #일관성과 확장성에 대한 고려사항 분리

...

## ▶︎ 인프라 추상화

개발자가 컨테이너 이미지 방식으로 애플리케이션을 개발하고 이식 가능한 쿠버네티스 방식으로 배포할 경우, 선언형 설정을 새로운 클러스터로 보내면 애플리케이션을 두 환경 간 전송하거나 하이브리드 환경에서 실행할 수 있다.

## ▶︎ 효율성

개발자는 더 이상 머신을 고려하지 않아도 되며, 여러 애플리케이션을 동일한 머신에 배치해도 애플리케이션에 영향을 주지 않는다.

모든 개발자가 네임스페이스를 통해 단일 테스트 클러스터를 쉽게 공유하고, 훨씬 적은 수의 머신으로 사용량을 통합할 수 있게 됐다. 

각 배포 비용을 여러 대의 가상 머신이 아닌 소수의 컨테이너로 측정할 경우 테스트에 드는 비용은 급격히 줄어든다.

## ▶︎ 요약

쿠버네티스는 클라우드에서 애플리케이션을 구축하고 배포하는 방식을 변혁하기 위해 만들었다. 
기본적으로 개발자에게 더 효율적인 속도, 효율성, 민첩성을 안겨주도록 설계됐다.

---

# 2장. 컨테이너 생성과 실행

단일 머신에 여러 애플리케이션을 실행하는 전통적인 방법은 시스템에서 모든 프로그램이 동일한 버전의 공유 라이브러리를 공유해야 한다. 여러 애플리케이션이 각기 다른 팀과 조직에서 개발되면 공유 종속성은 개발 팀 간에 불필요한 복잡성과 결합도(coupling)를 증가시킨다.

컨테이너 이미지는 애플리케이션과 애플리케이션에 종속된 파일을 루트 파일시스템에서 하나의 아티팩트(artifact)로 패키징한다. 

## ▶︎ 컨테이너 이미지

컨테이너 이미지(container image)는 운영체제의 컨테이너 내부에서 애플리케이션을 실행하기 위해 필요한 모든 파일을 캡슐화한 바이너리 패키지다. 

### # 도커 이미지 포맷

가장 많이 사용되고 보급된 컨테이너 이미지 포맷은 도커 이미지 포맷이다.

도커 이미지 포맷은 사실상 표준(De Facto)으로 지속적으로 활용되고 있으며, 일련의 파일시스템 계층으로 구성된다. 각 계층은 파일시스템의 이전 계층으로부터 파일 추가, 제거 또는 수정한다. 이것은 오버레이(overlay) 파일시스템의 예다.

컨테이너 이미지는 일련의 파일시스템 계층으로 구성되며, 각 계층은 이전 계층을 상속하고 수정한다. 개념적으로 각 컨테이너 이미지 계층은 이전 컨테이너 계층을 기반으로 한다. 각 부모 계층에 대한 참조는 포인터를 활용한다. 

컨테이너는 크게 두 가지 범주로 구분할 수 있다.

- 시스템 컨테이너
- 애플리케이션 컨테이너

    : 시스템 컨테이너와 다르게 일반적인 단일 애플리케이션을 실행한다. 컨테이너당 하나의 애플리케이션을 실행하는 것은 불필요한 제약조건처럼 보일 수 있으나 확장 가능한 애플리케이션을 완벽한 수준으로 세분화해 구성할 수 있으며, 포드(pod)가 주는 장점을 최대한 활용할 수 있는 디자인 철학이다.

## ▶︎ 도커를 활용한 애플리케이션 이미지 생성

### # 도커 파일

도커 파일(dockerfile)을 사용해 도커 컨테이너 이미지를 자동으로 생성할 수 있다.

    FROM alpine
    COPY bin/kuard /kuard
    ENTRYPOINT ["/kuard"]

▽ 이미지 생성 명령어

    $ docker build -t kuard-amd64:1

### # 이미지 보안

이미지의 모든 계층에서 하드코딩된 패스워드를 포함하는 컨테이너의 생성을 금지해야 한다. 하나의 계층에서 파일을 삭제해도 이전 계층의 해당 파일은 삭제되지 않기 때문이다.

### # 이미지 크기 최적화

시스템의 하위 계층에서 제거된 파일이 실제 이미지에 여전히 존재한다.

각 계층은 그 하위 계층과 독립적인 변경분임을 기억해야 한다. 상위 계층이 변경될 때마다 모든 하위 계층을 변경해야 한다. 상위 계층의 변경은 이미지를 개발 환경에 배포하기 위해 다시 빌드, 올리기, 가져오기 작업을 할 필요가 있음을 의미한다.

    (1)
    -- A 계층: 기본 운영체제 컨테이너
      -- B 계층: 소스 코드 server.js 추가 
        -- C 계층: node 패키지 설치 

    (2)
    -- A 계층: 기본 운영체제 컨테이너
      -- B 계층: node 패키지 설치
        -- C 계층: 소스 코드 server.js 추가

위 두 가지 이미지에서 `server.js` 변경 시 하나의 경우에는 pull을 하거나 push를 해야하는 변경 뿐이지만, 다른 경우에는 node 계층이 서버에 종속되어 있기 때문에 `server.js`와 node 패키지를 제공하는 계층 모두 pull한 후 push 해야 한다. 그 이유는 node 계층이 `server.js` 계층에 종속되어 있기 때문이다.

일반적으로 push, pull 하는 이미지의 크기를 최적화 하기 위해 **변경 가능성이 가장 적은 계층부터 변경 가능성이 높은 계층 순서로 지정한다.**

## ▶︎ 도커 컨테이너 런타임

쿠버네티스는 애플리케이션 배포를 위해 API를 제공한다. 그뿐 아니라 컨테이너 런타임에 의존하여 대상 운영체제별로 고유한 컨테이너 API를 사용해 애플리케이션 컨테이너를 설정한다. 리죽스 시스템의 경우 cgroup과 네임스페이스의 구성을 의미한다.

### # 도커로 컨테이너 실행

▽ `[gcr.io/kuar-demo/kuard-amd64:1](http://gcr.io/kuar-demo/kuard-amd64:1)` 이미지에서 컨테이너를 배포 명령어

    $ docker run -d --name kuard \
        --publish 8080:8080 \
        gcr.io/kuar-demo/kuard-amd64:1

### # 자원 사용량 제한

도커는 리눅스 커널이 제공하는 기본 cgroup 기술을 활용해 애플리케이션이 자원 사용량을 제한하는 기능을 제공한다.

***메모리 자원 제한***

컨테이너에서 애플리케이션을 실행해 얻을 수 있는 주요 이점 중 하나는 자원 사용을 제한할 수 있다는 것.
이 기능을 통해 여러 애플리케이션을 동일한 하드웨어에 공존시킬 수 있고 공정한 사용을 보장할 수 있다.

    $ docker run -d --name kuard \ 
        --publish 8080:8080 \
        --memory 200m \
        --memory-swap 1G \
        gcr.io/kuar-demo/kuard-amd64:1

***CPU 자원 제한***

    $ docker run -d --name kuard \ 
        --publish 8080:8080 \
        --memory 200m \
        --memory-swap 1G \
        --cpu-shares 1024 \
        gcr.io/kuar-demo/kuard-amd64:1

### # 이미지 정리

새로운 이미지를 만드는 작업을 반복할 때마다 컴퓨터에서 불필요한 공간을 차지하는 많은 이미지를 생성한다.

[docker-gc](https://github.com/spotify/docker-gc) 도구를 이용해 생성하는 이미지 수에 따라 반복적인 크론 작업을 하루에 한번 또는 시간당 한번 실행할 수 있다.

---

# 3장. 쿠버네티스 클러스터 배포

## 쿠버네티스 클라이언트

공식적인 쿠버네티스 클라이언트는 쿠버네티스 API와 상호작용하기 위한 명령줄 도구인 `kubectl`이다. 

**클러스터 상태 확인**

`$ kubectl version` 버전 확인 결과로 서로 다르더라도 kubectl과 클러스터 간 2개의 마이너 버전 차이 내에 있고, 이전 버전의 클러스터에서 새로운 기능을 사용하지 않으면 정/역방향 버전별 상위 또는 하위 호환성을 제공한다.

**클러스터 진단하기**

`$ kubectl get componentstatuses` 

    NAME                 STATUS    MESSAGE              ERROR
    scheduler            Healthy   ok
    controller-manager   Healthy   ok
    etcd-2               Healthy   {"health": "true"}
    etcd-0               Healthy   {"health": "true"}
    etcd-1               Healthy   {"health": "true"}

**컨트롤러 관리자(controller-manager)**는 **클러스터 동작을 제어**하는 다양한 컨트롤러를 실행하는 역할을 한다. 예를 들어 서비스 모든 복제본(replica)에 대해 사용 가능 여부와 정상 동작 여부를 확인한다. 

**스케줄러(scheduler)**는 클러스터의 다른 노드에 다른 포드를 배치한다.

**etcd 서버**는 모든 API 객체가 저장된 클러스터의 저장소다.

**클러스터 워커 노드 목록 조회**

쿠버네티스 노드는 클러스터를 관리하는 **API 서버**

스케줄러 같은 컨테이너를 포함하는 **마스터 노드**

컨테이너가 실행되는 **워커 노드**

▶︎ `kubectl describe nodes node-1`  결과 하단 일부

    Non-terminated Pods:         (4 in total)
      Namespace                  Name                                 CPU Requests  CPU Limits  Memory Requests  Memory Limits  AGE
      ---------                  ----                                 ------------  ----------  ---------------  -------------  ---
      kube-system                calico-node-ds6dn                    250m (15%)    0 (0%)      0 (0%)           0 (0%)         106d
      kube-system                kube-proxy-k8s-campaign-haraka002    150m (9%)     300m (18%)  64M (6%)         256M (27%)     106d
      kube-system                node-exporter-97g8x                  10m (0%)      30m (1%)    50Mi (5%)        50Mi (5%)      106d
      live                       bulk-haraka-66bd5f7c7c-vmq24         0 (0%)        0 (0%)      0 (0%)           0 (0%)         106d
    Allocated resources:
      (Total limits may be over 100 percent, i.e., overcommitted.)
      Resource           Requests         Limits
      --------           --------         ------
      cpu                410m (25%)       330m (20%)
      memory             116428800 (12%)  308428800 (33%)
      ephemeral-storage  0 (0%)           0 (0%)

각 포드가 요청하는 CPU, 메모리 자원에 대한 정보를 확인할 수 있다. 

쿠버네티스가 머신에서 실행되는 각 포드의 자원 요청(request)과 제한(limit)이 있다. 포드가 요청한 자원은 노드에 존재함을 보장한다. 그러나 포드의 보장 제한은 포드가 소비할 수 있는 주어진 자원의 최대량이다. 

포드의 한계는 요청보다 클 수 있으며, 이러한 경우 여분의 자원 중 제공 가능한 수준까지 제공된다. 하지만 여분의 자원이 노드 상에 존재하는 것이 보장 되지는 않는다.

## 클러스터 구성 요소

쿠버네티스 클러스터를 구성하는 많은 구성요소는 실제로 쿠버네티스를 통해 배포된다. 이 모든 구성 요소들은 **kube-system** 네임스페이스에서 실행된다. 

### 쿠버네티스 프록시

쿠버네티스 클러스터 내 서비스의 로드밸런싱을 위해 네트워크 트래픽을 라우팅한다. 이 작업 수행은 클러스터의 모든 노드에 프록시가 있어야 가능하다. 

쿠버네티스는 데몬셋(DaemonSet) API 객체를 갖고 있고, 이 객체는 많은 클러스터에서 프록시 기능을 수행한다. 

    $ kubectl get daemonSets --namespace=kube-system kube-proxy

### 쿠버네티스 DNS

클러스터에 정의된 서비스의 이름 지정과 검색을 제공하는 DNS 서버를 실행한다. 클러스터 크기에 따라 클러스터에 하나 이상의 DNS 서버가 실행될 수 있다. DNS 서비스는 복제본을 관리하는 Deployment로 실행된다. 

    $ kubectl get deployments --namespace=kube-system kube-dns

DNS 서버에 대한 로드밸런싱을 수행하는 쿠버네티스 서비스도 있다. 

    $ kubectl get services --namespace=kube-system kube-dns

### 쿠버네티스 UI

GUI, 단일 복제본으로 실행되며, 신뢰성과 업그레이드를 위해 Deployment로 관리된다.

`$ kubectl proxy` 명령을 통해 localhost:8001로 동작하는 서버를 실행해서 쿠버네티스 웹 UI를 볼 수 있다.

---

# 4장. 일반적인 kubectl 명령

## ▶︎ 네임스페이스

네임스페이스(namespace)로 내부 객체를 관리한다. kubectl  명령어는 기본 네임스페이스(default namespace)와 상호작용 한다. 네임스페이스를 변경하려면 `--namespace` 플래그를 사용한다.

## ▶︎ 컨텍스트

기본 네임스페이스를 영구적으로 변경하려면 컨텍스트(context)를 사용한다. 아래 명령은 `$HOME/.kube/config` 에 있는 kubectl 설정 파일에 저장된다.

    $ kubectl config set-context my-context --namespace=mystuff
    
    # 실제 새로운 컨텍스트를 사용하기 위해
    $ kubectl config use-context my-context

## ▶︎ 쿠버네티스 API 객체 보기

쿠버네티스는 자신 내부에 있는 모든 자원(쿠버네티스 객체)를 RESTful 자원으로 표현한다. 각 쿠버네티스 객체는 고유한 HTTP 경로를 갖는다. kubectl 명령은 HTTP 요청을 작성해 이런 URL에 있는 쿠버네티스 객체로 접근한다.

기본적으로 kubectl은 API 서버 응답을 사람이 읽을 수 있는 형태로 보여준다. 하지만 터미널 줄에 맞춤으로 많은 정보가 누락된다. `-o wide` 옵션을 사용해서 더 많은 정보를 볼 수 있다. 각 객체의 모든 정보를 보고 싶은 경우 `-o json` 또는 `-o yaml` 플래그를 사용한다.

헤더(header)를 제거하는 옵션은 `--no-header` 이고, 객체에서 특정 필드를 추출하려면 JSONPath쿼리 언어를 사용할 수 있다.

    $ kubectl get pods my-pod -o jsonpath --templage={.status.podIP}

## ▶︎ 쿠버네티스 객체 생성, 업데이트, 삭제

쿠버네티스 API의 객체는 JSON이나 YAML 파일 형태로 표현된다. 다음 명령을 사용해 쿠버네티스에 객체를 생성하거나 업데이트 할 수 있다.

    $ kubectl apply -f obj.yaml

아래 명령으로 객체를 삭제할 수 있지만, 즉시 삭제되기 때문에 주의해야 한다.

    $ kubectl delete -f obj.yaml

## ▶︎ 라벨과 어노테이션

    $ kubectl label pods bar color=red

label과 annotate 명령은 기본적으로 이미 존재하는 라벨에 대한 덮어쓰기를 수행할 수 없다. 덮어쓰려면 `--overwrite` 플래그를 사용해야 한다.

## ▶︎ 디버깅 명령

동작중인 컨테이너의 로그를 보려면...

    $ kubectl logs <포드 이름>

다수 컨테이너가 있는 경우 `-c` 플래그를 사용하면 특정 컨테이너를 선택해서 로그를 볼 수 있다.

동작중인 컨테이너에 다른 명령을 실행할 수 있다. 

    $ kubectl exec -it <포드 이름> -- bash

컨테이너에서 파일 복사하기

    $ kubectl cp <포드 이름>:/path/to/remote/file /path/to/local/file

---

# 5장. 포드

포드는 동일한 실행 환경에서 실행되는 **애플리케이션 컨테이너**와 **볼륨**으로 구성된 집합체다. 포드는 쿠버네티스 클러스터에서 **배포 가능한 가장 작은 아티팩트(artifact)**다. 즉, 포드에 있는 모든 컨테이너는 동일한 머신에 있음을 뜻한다.

포드에 있는 각 컨테이너는 각자의 cgroup을 운영하지만 몇가지 리눅스 네임스페이스를 공유한다.
동일한 포드에서 동작하는 애플리케이션은 동일한 IP 주소와 포드를 공유하고, 동일한 호스트네임을 갖는다.
또한 System V IPC나 POSIX 메시지 큐를 통해 기본 프로세스간 통신 채널을 사용해 서로 통신할 수 있다.

하지만 서로 다른 포드에 있는 애플리케이션은 각기 다른 IP 주소와 호스트네임을 갖는다.

## ▶︎ 포드에 대한 고찰

"포드에 무엇을 담아야 하나요?"

일반적으로 포드를 설계할 때 고민해야 하는 부분은 "**각 컨테이너가 서로 다른 머신에 있어도 동작할까?**"

"아니오"라면, 해당 컨테이너는 동일한 포드에 있어야 한다. 

"예"라면 여러 포드로 사용하는 것이 적합하다. 

## ▶︎ 포드 매니페스트

포드 매니페스트(Pod manifest)를 쿠버네티스 API 객체를 선언형 설정(declarative configuration) 형태로 텍스트 파일로 표현한 것이다. 

## ▶︎ 포드 실행

포드는 쿠버네티스 API 서버에 포드 매니페스트를 제출하고, 그 후 쿠버네티스 시스템은 클러스터에서 상태가 양호한 노드의 포드를 실행하기 위해 스케줄링 할 것이다. 그리고 kubelet 데몬 프로세스를 이용해 노드를 모니터링 할 것이다.

## ▶︎ 포드 접속

### # 포트 포워딩 사용

종종 간단히 특정 포드에 접속해야 할 때 쿠버네티스 API에서 자체적으로 지원하는 포트 포워딩(port forwarding)과 명령줄 도구를 사용해 포드에 접속할 수 있다.

다음 명령으로 로컬 머신에서부터 쿠버네티스 마스터를 거쳐 워커 노드에서 동작하는 포드 인스턴스까지 보안 채널이 생성된다.

    $ kubectl port-forward kuard 8080:8080

### # 로그에서 더 많은 정보 확인

`kubectl logs` 명령은 실행 중인 인스턴스에서 로그를 다운로드 한다.
`-f` 플래그를 추가해서 로그를 스트림으로 받을 수 있다.
`--previous` 플래그를 사용하면 컨테이너의 이전 인스턴스에서 로그를 가져온다.

## ▶︎ 상태 검사

활성 상태 검사(liveness)는 애플리케이션에 특화된 로직(예: 웹 페이지 불러오기)을 실행해 단순히 애플리케이션의 동작 여부만 검사하는 것이 아니라 정상 기능 수행 여부까지 확인한다. 애플리케이션별로 특화 되어야 하므로 반드시 포드 매니페이스에 정의해야 한다.

### # 활성 프로브

활성 프로브는 컨테이너별로 정의되고, 포드의 각 컨테이너는 개별적으로 상태 검사를 한다.

    apiVersion: v1
    kind: Pod
    metadata:
      name: kuard
    spec:
      containers:
        - image: gcr.io/kuar-demo/kuard-amd64:1
          name: kuard
          livenessProbe:
            httpGet:
              path: /healthy
              port: 8080
            initialDelaySeconds: 5
            timeoutSeconds: 1
            periodSeconds: 10
            failureThreshold: 3
          ports:
            - containerPort: 8080
              name: http
              protocol: TCP

이 포드는 8080 포트를 사용해 HTTP GET 요청을 `/healthy` 경로로 보내고, `initalDelaySeconds` 설정을 5로 했기 때문에 포드의 모든 컨테이너가 생성되고 5초 후에 호출될 것이다. 
`timeoutSeconds` 설정을 1로 했기 때문에 1초 이내 반드시 HTTP Status 200 ~ 400 응답을 해야 한다. 이 프로브는 10초마다(`periodSeconds`) 호출될 것이며, 프로브가 3번 이상 실패하면 컨테이너는 중지되고, 재시작 될 것이다.(`failureThreshold`)

### # 준비 프로브

활성(liveness)은 애플리케이션의 정상 동작 여부를 검사한다. 활성 검사를 통과하지 못한 컨테이너는 재시작된다.

준비(readness)는 사용자 요청의 처리 준비 여부를 검사한다. 이 검사를 통과하지 못한 컨테이너는 서비스 로드밸런서에서 제외된다.

정산적인 컨테이너만 클러스터에서 동작하게 하려면 준비 프로브와 활성 프로브를 함께 사용해야 한다.

### # 상태 검사 유형

HTTP 검사 외에도 TCP 소켓을 여는 `tcpSocket` 상태 검사와 exec 프로브도 지원한다. 

exec 프로브는 스크립트나 프로그램을 실행해서 0을 반환하면 코드를 종료하고 프로브는 성공으로 인식한다.

## ▶︎ 자원 관리

일반적으로 효율성은 사용률(utilization)으로 측정한다. 사용률은 구매한 자원을 사용 중인 자원으로 나누어 얻는 결과 값이다. 예를 들어, 1 코어 머신을 구매했고 애플리케이션이 코어의 1/10 만 사용하면 효율성은 10%다.

쿠버네티스처럼 자원을 묶어서 관리하는 시스템은 이 효율성을 50% 이상 끌어올릴 수 있다. 

### # 요청(request) 제한(limit)

쿠버네티스 스케줄러는 노드에 있는 모든 포드의 요청 자원의 합이 노드의 수용량을 넘지 않게 한다. 따라서 포드는 노드에서 동작할 때 적어도 요청한 자원만은 가질 수 있도록 보장한다.

예를들어 모든 사용 가능한 CPU 코어를 사용하는 컨테이너가 있다. 이 컨테이너를 갖는 포드를 생성하고 0.5 CPU를 요청했고, 쿠버네티스는 이 포드를 2개의 CPU 코어를 갖는 머신으로 스케줄링 했다.

두번째 포드를 동일한 머신에 실행하면 각 포드는 1 CPU씩 할당 받게 된다. 세번째 포드가 스케줄링 되면 각 포드는 0.66 CPU씩, 네번째가 포드가 추가 되면 0.5 CPU가 할당되고, 해당 노드는 더이상 추가 요청을 받을 수 없는 상태가 된다.

컨테이너에 limits 설정을 하면 커널은 이 설정 값을 초과할 수 없다.

## ▶︎ 볼륨에서 데이터 유지

### # 포드로 볼륨 사용

포드 매니페스트에 볼륨을 추가하는 두 가지 방법.

1. `spec.volumes` 섹션을 사용. 포드 매니페스트에 있는 모든 컨테이너가 접근할 수 있도록 모든 볼륨을 정의한다. 하지만 모든 컨테이너가 이 볼륨을 마운트할 필요는 없다.
2. 컨테이너 정의 부분에 `volumeMounts`를 추가. 특정 컨테이너에 마운트되는 볼륨과 각 볼륨이 마운트되는 경로를 정의

### # 포드에서 볼륨을 사용하는 다른 방법

**커뮤니케이션/동기화**

포드 안에 두 컨테이너가 공유 볼륨을 이용하기 위해 `emptyDir` 볼륨을 사용할 수 있다.

**영구 데이터**

쿠버네티스는 NFS나 iSCSI 같은 프로토콜 외에도 Amazon Elastic Block Store, Azure Files/Disk Storage, Google Persistant Disk 같은 네트워크 스토리지를 위한 원격 네트워크 스토리지 볼륨을 제공한다.

**호스트 파일 시스템 마운트**

`hostDir` 볼륨을 이용해 워커 노드에 있는 임시 위치를 컨테이너로 마운트 할 수 있다.

---

# 6장. 라벨과 애노테이션

라벨(label)은 포드(pod)와 레플리카세트(replicaset) 같은 쿠버네티스 객체에 첨부할 수 있도록 키(key)/값(value) 쌍으로 구성된다. 라벨은 임의적이며 쿠버네티스 객체에 식별 정보를 제공하고, 객체를 그룹화 하는 기초가 된다.

애노테이션(annotation)은 라벨과 유사하다. 도구와 라이브러리에서 활용할 수 있게 식별 불가능한 정보를 저장하기 위해 설계된 키/값 쌍의 구조다.

## ▶︎ 라벨

라벨의 키는 선택적 접두사와 슬래시(/)로 구분한다. 접두사를 지정하는 경우 253자로 된 DNS 하위 도메인으로 구성해야 하며, 필수적인 키 이름은 63자보다 짧아야 한다. 키 이름은 영문자로 시작하고, 문자 사이에 대시(-), 밑줄(_), 점(.)을 사용할 수 있다. 라벨의 값은 최대 63자인 문자열이다.

[예시](https://www.notion.so/7b6ba742e1694ea4976c800568f2488b)

### 라벨 적용 예제

    $ kubectl run alpaca-prod \
      --image=gcr.io/kuar-demo/kuard-amd64:1 \
      --replicas=2 \
      --labels="ver=1,app=alpaca,env=prod"
    
    $ kubectl run alpaca-test \
      --image=gcr.io/kuar-demo/kuard-amd64:2 \
      --replicas=1 \
      --labels="ver=2,app=alpaca,env=test"

    $ kubectl run bandicoot-prod \
      --image=gcr.io/kuar-demo/kuard-amd64:2 \
      --replicas=2 \
      --labels="ver=2,app=bandicoot,env=prod"
    
    $ kubectl run bandicoot-staging \
      --image=gcr.io/kuar-demo/kuard-amd64:2 \
      --replicas=1 \
      --labels="ver=2,app=bandicoot,env=staging"

**Deployment 라벨 확인**

    $ kubectl get deploy --show-labels
    
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE   LABELS
    alpaca-prod         2/2     2            2           72s   app=alpaca,env=prod,ver=1
    alpaca-test         1/1     1            1           58s   app=alpaca,env=test,ver=2
    bandicoot-prod      2/2     2            2           48s   app=bandicoot,env=prod,ver=2
    bandicoot-staging   1/1     1            1           26s   app=bandicoot,env=staging,ver=2

**Deployment 라벨 수정**

 `kubectl label` 명령어는 deployment 라벨만 변경한다.

    $ kubectl label deploy alpaca-test "canary=true"
    
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE     LABELS
    alpaca-prod         2/2     2            2           2m48s   app=alpaca,env=prod,ver=1
    alpaca-test         1/1     1            1           2m34s   app=alpaca,canary=true,env=test,ver=2
    bandicoot-prod      2/2     2            2           2m24s   app=bandicoot,env=prod,ver=2
    bandicoot-staging   1/1     1            1           2m2s    app=bandicoot,env=staging,ver=2

**라벨을 열(컬럼)으로 표시하기**

    $ kubectl get deploy -L canary
    
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE     CANARY
    alpaca-prod         2/2     2            2           4m14s
    alpaca-test         1/1     1            1           4m      true
    bandicoot-prod      2/2     2            2           3m50s
    bandicoot-staging   1/1     1            1           3m28s

**라벨 제거 (접미어에 대시(-) 추가)**

    $ kubectl label deploy alpaca-test "canary-"

## ▶︎ 라벨 선택기 (selector)

라벨의 집합을 기반으로 쿠버네티스 객체를 필터링. 간단한 boolean을 사용한다. 라벨 선택기는 kubectl 같은 도구를 사용하는 최종 사용자나 다른 유형의 쿠버네티스 객체에 의해 사용된다.

**라벨 직접 지정(복수개)**

    $ kubectl get deploy --selector="ver=2" --show-labels
    
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE   LABELS
    alpaca-test         1/1     1            1           12m   app=alpaca,env=test,ver=2
    bandicoot-prod      2/2     2            2           12m   app=bandicoot,env=prod,ver=2
    bandicoot-staging   1/1     1            1           12m   app=bandicoot,env=staging,ver=2
    
    
    $ kubectl get deploy --selector="app=bandicoot,ver=2" --show-labels
    
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE   LABELS
    bandicoot-prod      2/2     2            2           12m   app=bandicoot,env=prod,ver=2
    bandicoot-staging   1/1     1            1           12m   app=bandicoot,env=staging,ver=2

**라벨 OR 조건으로 지정**

    $ kubectl get deploy --selector="app in (alpaca, bandicoot)" --show-labels
    
    NAME                READY   UP-TO-DATE   AVAILABLE   AGE   LABELS
    alpaca-prod         2/2     2            2           14m   app=alpaca,env=prod,ver=1
    alpaca-test         1/1     1            1           14m   app=alpaca,env=test,ver=2
    bandicoot-prod      2/2     2            2           14m   app=bandicoot,env=prod,ver=2
    bandicoot-staging   1/1     1            1           14m   app=bandicoot,env=staging,ver=2

[선택기에 사용할 수 있는 연산자](https://www.notion.so/5857d1e342fe4794a7e92044fdaa0dab)

## ▶︎ API 객체의 라벨 선택기

역사적인 이유로 쿠버네티스는 두가지 버전의 API 호환성을 제공한다. 

`app-alpaca, ver in (1, 2)`의 선택기는 다음과 같이 변환된다.

    selector:
      matchLabels:
        app: alpaca
    matchExpresstions:
      - {key: ver, operator: In, values: [1, 2]}

모두 AND 연산자로 평가된다. != 연산자를 나타내는 유일한 방법은 단일 값을 사용한 `NotIn` 형식이다.

## ▶︎ 애노테이션

**도구와 라이브러리를 지원하려는 목적**으로 쿠버네티스 객체에 추가적인 메타데이터를 저장하는 장소를 제공한다.

라벨을 사용해 객체를 식별하고 그룹화하는 동안 애노테이션은 객체의 출처, 객체의 사용 방법 또는 객체에 대한 추가 정보를 제공하는 데 사용한다.

애노테이션과 라벨은 일부 기능이 겹친다. 확실하지 않은 경우 객체 애노테이션으로 정보를 추가하고, 선택기에서 사용하려는 경우 애노테이션을 라벨로 만들어 사용한다.

애노테이션은 쿠버네티스 여러 곳에서 사용되고 있으며, 롤링 배포(rolling deployment)에 주로 사용한다.  **롤링 배포 동안 애노테이션은 롤 아웃 상태를 추적하고, 디플로이먼트 이전 상태로 롤백하는데 필요한 정보를 제공한다.**

애노티에션 키는 라벨 키와 동일한 형식을 사용한다. 그러나 도구 간 정보 교환에 자주 사용되기 때문에 **키의 네임스페이스 부분**이 더 중요하다.
(예: `deployment.kubenetes.io/revision`, `kubenetes.io/change-cause` )

애노테이션 값은 자유로운 문자열 필드로 구성될 수 있지만, 유효성 검사가 수행되지 않기 때문에 유의해야 한다. (예: JSON을 문자열로 인코딩해서 저장하는 경우)
