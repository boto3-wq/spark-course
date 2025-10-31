\# Spark 클러스터 실습 환경



Apache Spark 분산 처리 클러스터를 Docker Compose로 구성한 학습 환경입니다.



\## 구성



\- Spark Master × 1

\- Spark Worker × 2

\- Jupyter Notebook with PySpark



\## 시스템 요구사항



\- Docker Desktop 설치

\- RAM: 8GB 이상 권장

\- CPU: 4코어 이상 권장



\## 시작 방법

```bash

\# 클러스터 시작

docker-compose up -d



\# 상태 확인

docker-compose ps

```



\## 접속 정보



\- Spark Master UI: http://localhost:8080

\- Spark Worker 1: http://localhost:8081

\- Spark Worker 2: http://localhost:8082

\- Jupyter Notebook: http://localhost:8888



\### Jupyter 토큰 확인

```bash

docker logs jupyter-pyspark

```



\## 종료 방법

```bash

\# Graceful 종료

docker-compose stop



\# 완전 삭제

docker-compose down

```



\## 데이터 영속성



\- `./data` - 공유 데이터 폴더

\- `./notebooks` - Jupyter 노트북 저장



\## 문제 해결



\### 포트 충돌

```bash

docker-compose down

docker-compose up -d

```



\### 완전 재시작

```bash

docker-compose down -v

docker-compose up -d

```

