---
layout: default
title: 📌 실시간 채팅서버 프로젝트
nav_order: 2
has_children: true
---

# **채팅 서버**

Kafka와 ELK stack을 통해 실시간 트래픽 관찰 및 안전성과 확장성을 고려한 Spring-Java 기반 채팅 백엔드/프론트 서버 프로젝트입니다 😊

* Github : [https://github.com/ghkdqhrbals/spring-chatting-server](https://github.com/ghkdqhrbals/spring-chatting-server)
* Youtube : [https://www.youtube.com/watch?v=3VqwZ17XyEQ](https://www.youtube.com/watch?v=3VqwZ17XyEQ)

## 1.  💡 아키텍처 변천사

<details><summary> V1 아키텍처 </summary><div markdown="1">

![img](../../assets/img/kafka/kafkaVersion.png)

</div></details>

<details><summary> V2, V3 아키텍처 </summary><div markdown="1">

![img](../../assets/img/es/final.png)

</div></details>

<details><summary> V4 아키텍처 </summary><div markdown="1">

![img](../../assets/img/msa/v3.1.0.png)

</div></details>

<details><summary> V5 아키텍처 </summary><div markdown="1">

![image](../../assets/img/msa/12.svg)

</div></details>

## 2.  🔨 성능 이슈 해결 및 최적화 과정

* [성능 최적화 과정 - 1](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-01-16-chatting(13)/) : **6가지 가설** 중, 도커 리소스 추가와 서버 수평 확장를 통한 성능 최적화 진행
> <details><summary> 6가지 가설 </summary><div markdown="1">
>
>  * [서버부하 툴의 속도문제] 문제였나? ❌
>  * [이벤트 흐름에서의 문제] 문제였나? ❌
>  * [백업 과정에서의 문제] 문제였나? ❌ 
>  * [과도한 replication 생성] 문제였나? ❌
>  * [제한된 CPU/MEMORY 리소스로 인한 문제] 문제였나? ✅
>  * [단일 인증 서버로 인한 병목현상] 문제였나? ✅
>
> </div></details>
* [성능 최적화 과정 - 2](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-01-17-chatting(15)/) : JPA-Batch를 통한 성능 최적화 진행
* [성능 최적화 과정 - 3](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-01-24-chatting(17)/) : JDBC-Batch 성능 그래프 확인
* [성능 최적화 과정 - 4](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-01-27-chatting(18)/) : **5가지 성능 개선 사안**들 및 적용된 값들 정리
> <details><summary> 5가지 성능 개선 사안 </summary><div markdown="1">
>
>  * [JDBC-Batch] before : 1 / after : 100
>  * [chatting_id 내부 자동 생성(네트워크 로드 감소)] before : from db sequence / after : random.UUID
>  * [db parallel processor 확장(db cpu 사용률 증가)] before : 1개 / after : 8개
>  * [쿼리 빈도 축소( sql 최적화 + lazy fetch )] before : 6번 / after : 4번
>  * [서버 수평 확장] before : 1대 / after : 2대
>
> </div></details>
* [성능 최적화 과정 - 5](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-03-05-chatting(21)/) : AWS-RDS 그래프 지표 관찰 및 db connection 증가를 통한 성능 최적화 진행
* [성능 최적화 과정 - 6](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-03-11-chatting(23)/) : 부하 테스트를 위한 툴 제작 및 실제 테스트 결과
* [성능 최적화 과정 - 7](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-03-16-chatting(25)/) : RDB 인덱싱 활성화를 통한 성능 최적화 진행
* [성능 최적화 과정 - 8](https://ghkdqhrbals.github.io/portfolios/docs/project/2023-05-01-chatting(35)/) : **6가지 가설** 중, 이벤트 전송 스레드 증가를 통한 성능 최적화 진행
> <details><summary> 6가지 가설 </summary><div markdown="1">
>
> * [Undertow 의 적은 parellel thread] 문제였나? ❌
> * [Spring Security 의 토큰 확인 절차에서 발생할 수 있는 딜레이 문제] 문제였나? ❌
> * [이벤트 트랜젝션을 관리하는 Redis 저장 성능 문제] 문제였나? ❌
> * [CPU/Memory 부족] 문제였나? ✅
> * [적은 Kafka Producer 스레드 개수] 문제였나? ✅
> * [linger.ms 와 batch_size 문제] 문제였나? ❌
>
> </div></details>

## 3.  📕 프로젝트를 수행하기 위해 따로 공부 및 정리한 포스팅 
* [메세지큐 - 1](https://ghkdqhrbals.github.io/portfolios/docs/메세지큐/2022-12-01-message-queue/) : 메세지 큐의 장점과 단점 정리
* [메세지큐 - 2](https://ghkdqhrbals.github.io/portfolios/docs/메세지큐/2022-12-02-kafka/) : Kafka 용어정리 및 구조 파악 
* [마이크로서비스 - 1(EN)](https://ghkdqhrbals.github.io/portfolios/docs/msa/2022-09-05-micro-service-architecture2/) : 기본적인 MSA 의 장단점 및 이해 정리
* [마이크로서비스 - 2](https://ghkdqhrbals.github.io/portfolios/docs/msa/2022-09-04-micro-service-architecture1/) : SAGA 패턴에 대한 이해 정리 
* [마이크로서비스 - 3](https://ghkdqhrbals.github.io/portfolios/docs/msa/2023-03-22-msa1/) : DDD 에 대한 이해와 이벤트 롤백처리에 대한 이해 정리
* [마이크로서비스 - 4(EN)](https://ghkdqhrbals.github.io/portfolios/docs/msa/2022-05-30-msa-docker-kubernetes/) : Docker/Kubernetes 이해 정리
* [웹서버 - 1](https://ghkdqhrbals.github.io/portfolios/docs/Java/6/) : Netty 아키텍처 및 동작원리 정리 
* [웹서버 - 2](https://ghkdqhrbals.github.io/portfolios/docs/Java/5/) : JVM NIO 모델에서 Reactor 모델까지의 변천사 정리
* [스프링 - 1](https://ghkdqhrbals.github.io/portfolios/docs/Java/2/) : Spring-Webflux 정리
* [스프링 - 2](https://ghkdqhrbals.github.io/portfolios/docs/Java/3/) : Reactor 모델에서의 Spring-security 인가 설정 정리
* [엘라스틱서치 - 1](https://ghkdqhrbals.github.io/portfolios/docs/elasticSearch/2022-12-31-elastic-search/) : RDB 와 ElasticSearch 비교 정리
* [엘라스틱서치 - 2](https://ghkdqhrbals.github.io/portfolios/docs/elasticSearch/2023-01-01-elastic-search(2)/) : ElasticSearch 노드 운용 방법 정리
* [엘라스틱서치 - 3](https://ghkdqhrbals.github.io/portfolios/docs/elasticSearch/2023-01-02-elastic-search(3)/) : LogStash 와 Kibana 를 붙여 하나의 스택을 통한 시각화 과정 정리
* [관계형데이터베이스 - 1](https://ghkdqhrbals.github.io/portfolios/docs/데이터베이스/db1/) : 쿼리 최적화 방법 정리
* [관계형데이터베이스 - 2](https://ghkdqhrbals.github.io/portfolios/docs/데이터베이스/2022-11-20-DB-3/) : 데이터 정합성 이론 정리
* [Golang - 1](https://ghkdqhrbals.github.io/portfolios/docs/Go언어/2022-09-18-thread-goroutine/) : 부하 테스트 툴 제작 시 필요한 경량 스레드 구조 정리
* [Java - 1](https://ghkdqhrbals.github.io/portfolios/docs/Java/java3/) : 자바의 CompletableFure 을 통한 콜백/멀티스레딩 정리
* [Java - 2](https://ghkdqhrbals.github.io/portfolios/docs/Java/java1/) : 자바의 동기/비동기 Blocking/Non-blocking 정리

## 4.  📗 프로젝트 진행 포스팅