### Dev Tech Stack Research

- 목차

[TOC]

#### 1. OS

>  
>
>  EC2 인스턴스의 OS로 linux 많이 쓰이는 배포판 + 무료 오픈 소스 위주로 장단점을 고려해 조사해 보았다.
>
>  1. Ubuntu
>  2. CentOS

- Ubuntu와 CentOS 비교

|                | Ubuntu                       | CentOS                                                       |
| -------------- | ---------------------------- | ------------------------------------------------------------ |
| 시스템 코어    | 데비안 기반                  | Redhat 기반                                                  |
| 보안           | 양호                         | 강함                                                         |
| 지원 고려 사항 | 우수한 문서 및 많은 커뮤니티 | 좋은 문서, 상대적으로 작은 커뮤니티                          |
| 패키지관리     | apt-get                      | yum                                                          |
| 사용의 용이성  | 보통                         | 어려움                                                       |
| 속도           | 우수                         | 우수                                                         |
| 업데이트 주기  | 빈번한 업데이트              | CentOS 시리즈는 지원 종료 결정<br />CentOS 8 21년 12월 종료, 7 24년 6월 종료 |

>  위 사항에 더하여 조사결과 Ubuntu가 커뮤니티가 잘 되어 있으며, 두 배포판 모두 안정적이고 안전하지만 비교적으로 CentOS가 Ubuntu보다 더 안정적이고 안전하다고 말하며 , 제어 패널을 제공하는 점에서 기업의 서버로 적합하다고 생각할 수 있다. 하지만 지원 종료 결정 및 정보의 양을 생각하면 Ubuntu도 좋은 선택이 될 수 있다고 생각했다.



#### 2. Database

|      | SQL                                                          | NoSQL                                                        |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 장점 | 1. 범용적, 고성능, 안정적, 일관성, 무결성 보장<br />2. 정규화를 전제로 하기 때문에 업데이트시 비용이 적다.<br />3. 데이터베이스 설계시 불필요한 중복을 방지<br />4. 복잡한 형태의 쿼리가 가능하여 원하는 데이터를 볼 수 있다. (Join, Group By 등)<br />5. 성숙한 기술 | 1. 데이터 모델이 독립적이여서 분산에 용이<br />2. 복제 및 Recovery에 용이<br />3. 데이터를 고속으로 처리할 경우 용이<br />4. 스키마의 정해진 형태가 없기 때문에 유연한 모델 변경 가능<br />5. Document 형식으로 많은 데이터를 저장 가능 |
| 단점 | 1. 대량의 입력처리에서 성능 이슈<br />2. 이미 만들어진 스키마 변경 시 데이터 조작이 까다롭다.<br />3. 개발 단계에서 엔티티가 확실하지 않을 경우 곤란하다. | 1. 다양한 솔루션에 따른 이해가 필요. 학습곡선이 높다.<br />2. 비교적 새로운 기술로 노하우 부족<br />3.비교적 버그가 많고 불안정하다.<br />4. 보안에 취약하기 때문에 별도의 보안체계 마련 필요<br />5. 효율적인 데이터 모델링이 어렵다.<br />6. 복잡한 쿼리사용이 부적합하다. |

>   위 장단점들과 조사 결과를 바탕으로 SQL은 복잡한 쿼리나 리포트를 만들거나, 높은 부하가 예상되거나, 데이터가 어마하게 쌓이지 않을것 같을 때 사용하면 적절하고, NoSQL의 경우 지속적인 기능이 추가되어 데이터셋을 사전정의 하기 힘든 경우나 데이터가 너무 많을 경우에 사용하면 속도면에서 이점을 가진다.



#### 3. Web Server

> 현재 NginX와 Apache가 인터넷 트래픽의 50% 이상을 제공하고 있다. 가장 많이 쓰이는 오픈소스 웹서버 라고 할 수 있으며, 참고할 수 있는 정보들이 많다고 생각하여 조사하여 정리해 보았다.
>
> NginX vs Apache
>
> | Apache                                       | NginX                                     |
> | -------------------------------------------- | ----------------------------------------- |
> | 요청 당 쓰레드 또는 프로세스가 처리하는 구조 | 비동기 이벤트 기반으로 요청 처리          |
> | 모듈의 다양성을 제공                         | 비교적 적은 모듈                          |
> | 접속자가 많아질 수록 프로세스사용량이 늘어남 | 하나의 프로세스로 많은 접속자들 대응 가능 |
> | 분산/ 중앙 집중식 구성                       | 중앙 집중식 구성                          |
> | 확장성, 호환성 우세                          | 안정성, 성능 우세                         |
>
> 각각의 다른 방식을 가지고 있고, 장점과 단점을 현재 상황에 맞는 혹은 편한 소프트웨어를 사용하는게 좋다.
>
> 서버 부담을 줄이고자 하는 중소규모 서버에서는 NginX를 이용하여 서버에 대한 부담을 낮출 수 있다고 말한다.
>
> Web server 쪽은 직접 구축 및 사용경험이 없음으로 사용경험을 제외하고 결정 후 진행한다.
>
> 추가
>
> Nginx는 Master와 Worker로 구성되며 이벤트 발생 시 Worker에게 전달, 오버헤드가 상대적으로 적음.
>
> Apache는 리퀘스트 당 프로세스/쓰레드 생성, 프로세스/쓰레드 변경 간 컨텍스트 스위치 발생, 오버헤드 발생.
>



#### 4. Java

> 현재 많은 사용자들이 Java 8 사용 또는 Java 8 에서 11 로 전환하여 사용중이다. Java 11에서는 다양한 특징들이 새로 추가되고 JVM 및 핵심 라이브러리의 성능이 향상되었지만 아직 다양한 라이브러리들이 java 8 까지 지원하는 하거나 모듈 참조에 의한 이슈들이 종종 발생할 수 있기 때문에 안정성을 고려하면 java 8을 사용하는 것도 좋은 선택이 될 수 있다.
>
> - Java 8 특징
> - 기본 GC -> 병렬 GC
>   - Lambda Expression
>   - Repeating Annotation
>   - Stream API
> 
> - Java 11 특징
> - GC -> G1GC (가비지 우선 가비지 수집기)
>   - 람다 파리미터에 대한 지역 변수 문법
>   - 앱실론 가비지 컬렉터
>   - HTTP Client 표준화
>   - 모듈 업데이트(java 9에서 도입, 모듈에서 호환 문제가 가끔 발생)
>   - Docker 컨테이너와 java간 지원 기능 향상



#### 5. Framework

> **아키텍처를 정해 나감에 있어 추가 및 삭제 보완하기**
>
> - Spring Boot( tomcat embedded )
> - Hibernate  vs Mybatis
>
> |             | Hibernate                                | MyBaits                                          |
> | ----------- | ---------------------------------------- | ------------------------------------------------ |
> | Product     | Object 중심적                            | Database 중심적                                  |
> | 개념        | ORM<br />(java classes - database table) | SQL Mapping<br />(SQL statement - Java methods)  |
> | 복잡한 쿼리 | 상대적으로 약함                          | SQL을 직접 작성함으로<br />복잡한 쿼리 사용 가능 |
> | 생산성      | 높음                                     | 보통                                             |
> | 학습 난이도 | 높음                                     | 보통                                             |
> | 사용 경험   | 적음                                     | 보통                                             |
>
>  프로덕트의 중심이 되는 부분, 상대적으로 복잡한 쿼리, 사용 경험 등 여러가지를 고려하여 적절한 선택을 해야한다.
>
> - SLF4J ( Logging )



#### 6. Build

> 
>
> Maven vs Gradle
>
> - Maven
>   - 빌드를 쉽게 (Making the build process easy)
>   - pom.xml을 이용한 정형화된 빌드 시스템
>   - 새로운 기능을 쉽게 설치 하고 업데이트 가능
>   - 사용 경험 있음
> - Gardle
>   - 유연한 범용 빌드 도구
>   - 멀티 프로젝트에 사용하기 좋음
>   - 그루비 문법 사용
>   - 사용 경험 없음
> - 빌드의 규모가 커질수록 Gradle의 속도가 빠르다.
> - Maven의 경우 완전한 이해를 바탕으로 하지 않지만, 구축 및 사용 경험이 있으나, Gradle의 경우 사용 경험이 없음으로 구조 및 그루비 문법을 새로 익히는데 시간이 필요하다.
> - 실제로 성능이 Gradle이 우수하지만  구글 트렌드 지수 및 여러 사용 지표들을 보면 Maven이 Gradle을 앞서고 있다.  Gradle 도입으로 생기는 팀의 학습비용이 크다는 영향이 큰 것으로 보인다.



#### 7. deploy (추후 도입)

local -> dev -> ( integration ) -> testing -> staging -> production



#### 8. ETC

- ###### System Monitoring

> Spring Boot + Slack + Logback을 이용하여 서버 애플리케이션에서 오류 발생 시 슬랙 메시지로 오류에 관한 정보(stacktrace, error 내용, 발생 시간, 시스템 명, HTTP 정보, 사용자 정보 등)를 전송해 주는 모니터링 시스템을 구축함으로 모니터링 및 장애대응을 신속하게 한다.

- ###### Swagger - API Document

> Swagger를 도입함으로 인해 API의 Specification을 시각적으로 한눈에 파악하고 변경 관리 할 수 있고, 객체들에 대한 정보도 제공할 수 있으며 api 테스트도 진행해 볼 수 있다. 하지만 단점으로는 프로덕션 코드의 가독성을 떨어뜨리거나 어플리케이션의 무게가 무거워 질 수 있으며, Swagger 관련 어노테이션 등에 대한 학습도 이루어 져야 한다.
