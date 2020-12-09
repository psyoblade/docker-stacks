[![docker pulls](https://img.shields.io/docker/pulls/jupyter/all-spark-notebook.svg)](https://hub.docker.com/r/jupyter/all-spark-notebook/)
[![docker stars](https://img.shields.io/docker/stars/jupyter/all-spark-notebook.svg)](https://hub.docker.com/r/jupyter/all-spark-notebook/)
[![image metadata](https://images.microbadger.com/badges/image/jupyter/all-spark-notebook.svg)](https://microbadger.com/images/jupyter/all-spark-notebook "jupyter/all-spark-notebook image metadata")

# 주피터 노트북 도커 이미지 (Python, Scala, R, Spark Stack)
> 본 프로젝트는 https://github.com/jupyter/docker-stacks 에서 클론 이후에 추가적인 컴포넌트 설치 및 배포를 위해 작성된 이미지입니다

## 도커 이미지 빌드
```bash
$> docker build -t psyoblade/all-spark-notebook .
```

## 도커를 통한 실행 
```bash
$> docker run --rm --name notebook -v notebooks:/home/jovyan/work -p 8888:8888 -d psyoblade/all-spark-notebook
```

## 도커 컴포즈를 통한 실행
```bash
$> cat docker-compose.yml
version: "3"
servcies:
  notebook:
    container_name: notebook
    user: root
    privileged: true
    image: psyoblade/all-spark-notebook
    restart: always
    volumes:
      - ./notebooks:/home/jovyan/work
    environment:
      - GRANT_SUDO=yes
    ports:
      - "4040:4040"
      - "4041:4041"
      - "8888:8888"

$> docker-compose up -d
```


## 레퍼런스
- [Jupyter Docker Stacks on ReadTheDocs](http://jupyter-docker-stacks.readthedocs.io/en/latest/index.html)
- [Selecting an Image :: Core Stacks :: jupyter/all-spark-notebook](http://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-all-spark-notebook)
- [Image Specifics :: Apache Spark](http://jupyter-docker-stacks.readthedocs.io/en/latest/using/specifics.html#apache-spark)
