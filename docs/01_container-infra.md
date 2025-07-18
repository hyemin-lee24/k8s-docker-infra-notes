# 1장. 새로운 인프라 환경이 온다

> 1.1 컨테이너 인프라 환경이란?
> 1.2 컨테이너 인프라 환경을 지원하는 도구
> 1.3 새로운 인프라 환경의 시작
>
> > 본 문서는 1장의 일부 내용 중 **1.1 컨테이너 인프라 환경이란?** 과  **1.2 컨테이너 인프라 환경을 지원하는 도구**를 정리한 내용입니다.



## 1.1 컨테이너 인프라 환경이란?

### 컨테이너란?

- 하나의 운영 체제 커널에서 다른 프로세스에 영향을 받지 않고 독립적으로 실행되는 **프로세스 단위의 격리 환경**
- 가상 머신보다 **가볍고 빠르게 동작**

### 컨테이너 인프라 환경

- 컨테이너를 중심으로 구성된 인프라 환경
- 컨테이너 단위로 서비스가 나뉘고, 유연한 배포와 확장 가능

### 모놀리식 아키텍처

> 하나의 큰 목적을 가진 애플리케이션에 여러 기능이 통합된 구조

- **장점**: 초기 설계가 단순하고 코드 관리가 쉬움
- **단점**:
  - 수정 시 다른 서비스에 영향이 갈 가능성 큼
  - 기능 추가 시 서비스 간의 관계가 복잡해질 수 있음

### 마이크로서비스 아키텍처 (MSA)

> 모놀리식 구조의 한계를 극복하기 위한 구조.
> 개별 기능을 가진 작은 서비스를 각각 개발·운영하고, 이를 연결하여 전체 서비스를 구성

#### 등장 배경

- 특정 서비스만 증설하기 어려운 모놀리식 구조의 한계
- 일부 오류로 전체 서비스 중단 위험

#### 특징

- 각 서비스는 독립적으로 동작하는 **완결된 단위**
- 시스템 전체는 하나의 목적을 지향하지만, **구현은 분리**

#### 장점

- 서비스 간 영향도 낮음
- 재사용성 높음
- IaaS(클라우드 인프라) 환경에 적합

#### 단점

- 구조가 복잡해짐
- 서비스 간 네트워크 호출 증가로 인한 **성능 저하** 가능성

#### 구성 예시

- 각 서비스는 관련 기능과 데이터베이스를 **독립적으로 보유**
- 외부 요청은 API 게이트웨이와 REST API를 통해 처리
- 서비스 등록 및 검색은 **서비스 디스커버리**로 관리
- 서비스 간 내부 통신은 **이벤트 버스**를 통해 일원화

#### 구성 예시로부터 얻는 장점

- 각 서비스는 필요한 기능에 특화된 DB 사용 가능
- 서비스 추가 시 이벤트 버스에 연결만 하면 되어 **확장 용이**
- 이미 개발된 기능은 **다른 서비스에서 재사용 가능**

### 컨테이너 인프라 환경에 적합한 아키텍처

- 컨테이너는 **서비스 단위로 포장**되어 배포·확장에 용이
- MSA의 각 서비스는 컨테이너와 **1:1 매핑** 가능



## 1.2주요 구성 요소 및 도구

### Docker

- 컨테이너를 생성·관리하는 대표적인 도구
- 운영체제와 무관하게 일관된 실행 환경 제공

#### 그 외 컨테이너 도구

- containerd
- CRI-O
- Podman

### Kubernetes

- 여러 컨테이너를 관리하기 위한 **오케스트레이션 도구**
- 자동 배포, 헬스 체크, 확장, 복구 등의 기능 제공

### Jenkins

- **CI/CD(지속적 통합 및 배포)** 자동화 도구
- 빌드 → 테스트 → 패키징 → 배포 과정 전반 자동화
- 빠른 코드 반영 및 안정적인 배포 환경 제공

### Prometheus & Grafana

- **Prometheus**: 컨테이너 상태 데이터 수집
- **Grafana**: Prometheus 데이터를 시각화하여 대시보드로 제공
- 마이크로서비스처럼 분산된 환경에서 **중앙 모니터링 도구로 활용**