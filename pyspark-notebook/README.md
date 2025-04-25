# 주피터 PySpark 노트북 도커 이미지 (Python, Scala, R, Spark Stack)
> 본 프로젝트는 https://github.com/jupyter/docker-stacks 에서 클론 이후에 추가적인 컴포넌트 설치 및 배포를 위해 작성된 이미지입니다

## 수정내역
* v1.9 : 멀티 플랫폼 지원
 - 2025/04/20 : data-engineer-pyspark-notebook:1.9

### 멀티 플랫폼 빌드
```bash
VERSION=1.9

# 멀티플랫폼(amd64,arm64) 설정으로 빌드 및 도커허브에 푸쉬
docker buildx build --no-cache --progress=plain -t \
    --platform linux/amd64,linux/arm64 \
    -f ubuntu.22-pyspark.3.5.Dockerfile \
    -t psyoblade/data-engineer-pyspark-notebook:${VERSION} \
    --push .
```

## 도커 이미지 빌드
```bash
VERSION=1.9

# 로컬 환경에서 빌드
docker build -t local/data-engineer-pyspark-notebook:${VERSION} .

# 빌드된 노트북 테스트 
docker run --rm --name notebook -v `pwd`/notebooks:/home/jovyan/work -p 8888:8888 -d local/data-engineer-pyspark-notebook:${VERSION}

# 태그 후 도커허브에 푸시
docker tag local/data-engineer-pyspark-notebook:${VERSION} psyoblade/data-engineer-pyspark-notebook:${VERSION}
docker push psyoblade/data-engineer-pyspark-notebook:${VERSION}
```

## 도커 컴포즈를 통한 실행
```bash
$> cat .env
VERSION=1.8

$> cat docker-compose.yml
version: "3"
servcies:
  notebook:
    container_name: notebook
    user: root
    privileged: true
    image: psyoblade/data-engineer-pyspark-notebook:${VERSION}
    restart: always
    volumes:
      - ./notebooks:/home/jovyan/work
    environment:
      - GRANT_SUDO=yes
    ports:
      - "4040-4049:4040-4049"
      - "8080:8080"
      - "8888:8888"

$> docker-compose up -d
```

## 레퍼런스
- [Jupyter Docker Stacks on ReadTheDocs](http://jupyter-docker-stacks.readthedocs.io/en/latest/index.html)
- [Selecting an Image :: Core Stacks :: jupyter/all-spark-notebook](http://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-all-spark-notebook)
- [Image Specifics :: Apache Spark](http://jupyter-docker-stacks.readthedocs.io/en/latest/using/specifics.html#apache-spark)


