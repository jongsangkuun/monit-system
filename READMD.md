# 프로젝트 목표
1. CPU, MEMORY, Disk, Network traffic 을 모니터링하는 도구
2. 수집된 데이터는 Postgres에 저장하여 로깅 기능
3. 수집된 데이터를 Grafana 또는 직접 만든 모니터링 페이지로 확인
4. 각 모듈별 임계치값 이상이 올라올 경우 메일로 모니터링 요청
5. 모든 모듈은 docker 구성
6. 프로토타입 완성 시 CI/CD 자동화를 통해 테스트 코드 통과 후 반영


# 하드웨어 정보
github.com/shirou/gopsutil 라이브러리 사용

# DB 스키마
CPU_INFO

| Table_name | Type      | Description    |
|------------|-----------|----------------|
| id         | uuid      | uuid           |
| cpu_name   | text      | CPU 이름         |
| cpu_core   | text      | CPU 코어 갯수      |
| is_deleted | bool      | soft_delete 구현 |
| created_at | datetime  | 생성 시간          |
| updated_at | datetime  | 업데이트 시간        |

MEMORY_INFO

| Table_name      | Type     | Description |
|-----------------|----------|-------------|
| id              | uuid     | uuid        |
| memory_name     | text     | 메모리 이름      |
| physical_memory | text     | 물리적 메모리 크기  |
| is_deleted      | bool     | soft_delete |
| created_at      | datetime | 생성 시간       |
| updated_at      | datetime | 업데이트 시간     |

DISK_INFO

| Table_name  | Type     | Description |
|-------------|----------|-------------|
| id          | uuid     | uuid        |
| disk_name   | text     | 디스크 이름      |
| file_system | text     | 파일시스템 이름    |
| Mounted     | text     | 마운트 위치      |
| size        | text     | 디스크 크기      |
| is_deleted  | bool     | soft_delete |
| created_at  | datetime | 생성 시간       |
| updated_at  | datetime | 업데이트 시간     |


NETWORK_INFO

| Table_name        | Type     | Description   |
|-------------------|----------|---------------|
| id                | uuid     | uuid          |
| network_interface | text     | 네트워크 인터페이스 이름 |
| is_deleted        | bool     | soft_delete   |
| created_at        | datetime | 생성 시간         |
| updated_at        | datetime | 업데이트 시간       |

---
CPU_LOG

| Table_name | Type      | Description    |
|------------|-----------|----------------|
| id         | uuid      | uuid           |
| cpu_name   | text      | CPU 이름         |
| cpu_usage  | text      | CPU 사용량        |
| is_deleted | bool      | soft_delete 구현 |
| created_at | datetime  | 생성 시간          |
| updated_at | datetime  | 업데이트 시간        |