# Spark 클러스터 실습 환경

Apache Spark 분산 처리 클러스터를 Docker Compose로 구성한 학습 환경입니다.

## 구성

- Spark Master × 1
- Spark Worker × 2  
- Jupyter Lab (Python 3.8 + PySpark 3.5.0)

## 시스템 요구사항

- Docker Desktop 설치
- RAM: 8GB 이상 권장
- CPU: 4코어 이상 권장

## 시작 방법
```bash
# 클러스터 시작 (첫 실행 시 이미지 빌드로 5분 소요)
docker-compose up -d --build

# 상태 확인
docker-compose ps

# graceful 종료 이후 재시작
docker-compose start
```

## 접속 정보

- Spark Master UI: http://localhost:8080
- Spark Worker 1: http://localhost:8081
- Spark Worker 2: http://localhost:8082
- Jupyter Lab: http://localhost:8888 (토큰 불필요)

## Jupyter에서 Spark 사용하기
```python
from pyspark.sql import SparkSession

# Spark Session 생성
spark = SparkSession.builder \
    .appName("MyFirstSparkApp") \
    .master("spark://spark-master:7077") \
    .getOrCreate()

# 간단한 테스트
data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
df = spark.createDataFrame(data, ["Name", "Age"])
df.show()
```

## 종료 방법
```bash
# Graceful 종료
docker-compose stop

# 완전 삭제
docker-compose down
```

## 데이터 영속성

- `./notebooks` - Jupyter 노트북 저장

## 기술 스택

- Apache Spark 3.5.0
- Python 3.8
- Jupyter Lab
- Docker & Docker Compose

## 문제 해결

### 포트 충돌
```bash
docker-compose down
docker-compose up -d
```

### 완전 재시작
```bash
docker-compose down -v
docker-compose up -d --build
```

### Python 버전 확인
```bash
docker exec jupyter-pyspark python --version
docker exec spark-worker-1 python3 --version
```

## 주의사항

- 모든 컨테이너가 동일한 Python 3.8 버전을 사용합니다
- Jupyter는 커스텀 Dockerfile로 빌드되어 Spark 클러스터와 완벽히 호환됩니다
