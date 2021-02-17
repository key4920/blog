---
title: "Mac OS에 스파크 3.0 설치 및 pyspark 시작"
metaAlignment: center
autoThumbnailImage: false
thumbnailImagePosition: left
thumbnailImage: /post/images/2021-02-14/spark_thumbnail.png
date: 2021-02-14
categories:
- Apache-spark
tags:
- spark
- 스파크
- 스파크설치
---

맥북 Mac OS에 Spark를 설치해보고 주피터 노트북에서 pyspark를 실행해보자!

<!--more-->

## STEP1. 스파크 버전 선택 후 다운로드

[Downloads | Apache Spark](http://spark.apache.org/downloads.html)


![download_spark_version.png](/post/images/2021-02-14/download_spark_version.png)


원래는 Spark 2.4.7 을 선택해서 설치했었다.  
하지만 로컬의 Java 버전이 11이었으므로, 그냥 이참에 Spark3.0을 시도해보기로 했다!

(참고) Spark3.0은 Java 11을 지원하고, Spark2.X는 Java 8을 지원한다.

우선 원하는 Spark 버전 선택하여 'Download Spark' 를 클릭해주면 다음과 같은 화면으로 넘어간다.

![download_spark_mirror.png](/post/images/2021-02-14/download_spark_mirror.png)

mirror sites 중 한개를 선택해 다운로드해주는데, 그냥 최상단 링크를 눌러 다운로드 해준다.

NT. Java 와 Python은 설치 돼있다는 가정으로 진행한다.

## STEP2. 다운로드한 압축 파일을 home directory에 풀어준다.

```bash
tar -zxvf spark-3.0.1-bin-hadoop3.2.tar
```

## STEP3. ~/.bash_profile 환경변수 수정

어떤 directory에서도 spark notebook 열 수 있도록 환경변수 설정해준다.

```bash
## .bash_profile 있는지 확인
ls -a 
## .bash_profile 파일 열기
nano .bash_profile
## 또는 
vi .bash_profile
```

 

아래 환경변수 추가로 써준다.

```bash
## 버전 맞게 써주기
export SPARK_PATH=~/spark-3.0.1-bin-hadoop3.2 
## PySpark Shell을 주피터 노트북에서 열 수 있도록 설정
export PYSPARK_DRIVER_PYTHON="jupyter"
export PYSPARK_DRIVER_PYTHON_OPTS="notebook"

## 파이썬 3를 사용한다면 아래 설정 추가해 주어야 에러가 나지 않음
export PYSPARK_PYTHON=python3

## sparknb는 명령어 마음대로 써준 것이므로, 원하는 이름으로 수정 가능
## local[2] 는 로컬 코어 2개를 사용한다는 뜻으로 본인 로컬 환경에 맞게 수정 가능
alias sparknb='$SPARK_PATH/bin/pyspark --master local[2]'
```

만약 nano .bash_profile 했었으면  ^x —> Y —> enter 로 저장하고 빠져나오기

vi .bash_profile 했었으면 :wq 입력 후 저장하고 빠져나오기

```bash
source .bash_profile
```

## 이제 모두 완료됐으니, 간단한 실습해보자!

```bash
## 터미널에서 sparknb입력하여 주피터 노트북 실행
## 다른 이름으로 설정했다면, 해당 이름으로 실행
sparknb
```
![test_first_example_1.png](/post/images/2021-02-14/test_first_example_1.png)

![test_first_example_2.png](/post/images/2021-02-14/test_first_example_2.png)

## Reference

[Install Spark on Mac (PySpark)](https://medium.com/@GalarnykMichael/install-spark-on-mac-pyspark-453f395f240b)

[[mac] Apache Spark Study -1 ( Spark설치(HomeBrew) )](https://kingname.tistory.com/159)

[apache-spark@3.0.1 설치](https://parkaparka.tistory.com/27)