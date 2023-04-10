# Quest 18-B. 서비스의 운영: 로깅과 모니터링

## Introduction
* 이번 퀘스트에서는 서비스의 운영을 위해 로그를 스트리밍하는 법에 대해 다루겠습니다.

## Topics
* ElasticSearch
* AWS ElasticSearch Service
* Grafana

## Resources
* [ElasticSearch](https://www.elastic.co/kr/what-is/elasticsearch)
* [ElasticSearch 101](https://www.elastic.co/kr/webinars/getting-started-elasticsearch)
* [Grafana Panels](https://grafana.com/docs/grafana/latest/panels/)

## Checklist
* ElasticSearch는 어떤 DB인가요? 기존의 RDB와 어떻게 다르고 어떤 장단점을 가지고 있나요?
    * Elasticsearch는 오픈 소스 분산 검색 및 분석 엔진으로, 실시간으로 대규모 데이터를 저장하고 검색, 분석, 시각화할 수 있는 기능을 제공하는 NoSQL 데이터베이스입니다.

    * RDB와는 달리 Elasticsearch는 스키마리스(schemalist) 데이터베이스입니다. 이는 데이터베이스에 데이터를 추가할 때 미리 정의된 테이블 스키마가 필요하지 않다는 것을 의미합니다. 대신, Elasticsearch는 데이터가 색인(index)될 때 필드 구조를 자동으로 결정하고 저장합니다. 이는 대규모 분산 데이터베이스에서 유연성을 제공하고, 빠르고 쉬운 데이터 검색을 가능하게 합니다.

    * 또한 Elasticsearch는 검색 쿼리의 효율성을 위해 역색인(inverted index)이라는 구조를 사용합니다. 이 구조는 각 용어(단어)가 문서에서 어디에서 발견되는지를 기록하는 것으로, 검색 쿼리에 대한 결과를 빠르게 생성할 수 있도록 도와줍니다.

    * 장점으로는 다음과 같은 것들이 있습니다.

    * 대규모 분산 데이터베이스에서 빠르고 쉬운 검색, 분석, 시각화 가능
    * 스키마리스 데이터베이스로 유연한 데이터 모델링 가능
    * 역색인 구조로 효율적인 검색 쿼리 처리 가능
    * 높은 가용성과 확장성을 제공하는 클러스터링 기능

    * 단점으로는 다음과 같은 것들이 있습니다.

    * 데이터 일관성이 RDB에 비해 낮을 수 있음
    * 검색 결과가 정확하지 않을 수 있음
    * 분산 환경에서의 데이터 백업, 복구, 보안에 대한 고민이 필요함

* AWS의 ElasticSearch Service는 어떤 서비스인가요? ElasticSearch를 직접 설치하거나 elastic.co에서 직접 제공하는 클라우드 서비스와 비교하여 어떤 장단점이 있을까요?
    * AWS의 ElasticSearch Service는 AWS에서 제공하는 ElasticSearch 관리형 서비스입니다. ElasticSearch를 설치, 설정, 운영하는 부분을 대신 처리해주어 사용자는 ElasticSearch 클러스터의 스케일링, 모니터링, 로그 수집 등의 기능에 집중할 수 있습니다.

    * AWS ElasticSearch Service의 주요 장점은 다음과 같습니다.

    * 쉬운 설정 및 관리: ElasticSearch Service는 인터페이스를 통해 쉽게 클러스터를 설정하고 관리할 수 있습니다. 클러스터의 스케일링, 복제, 백업, 모니터링 등에 대한 지원을 제공하여 사용자는 ElasticSearch 클러스터의 운영에 대해 걱정하지 않고 데이터를 처리할 수 있습니다.
    * 높은 가용성: ElasticSearch Service는 데이터의 가용성을 보장하기 위해 여러 가용 영역에 걸쳐 클러스터를 자동으로 분산시키고 자동 복제 기능을 제공합니다.
    * 높은 보안성: ElasticSearch Service는 VPC(Virtual Private Cloud) 내에서 클러스터를 실행하며, AWS Identity and Access Management(IAM)과 통합하여 보안성을 강화합니다.
    * 반면, Elastic.co에서 제공하는 클라우드 서비스인 Elastic Cloud는 ElasticSearch를 직접 설치하고 운영하는 경우와 비교하여 ElasticSearch의 전체 기능을 사용할 수 있으며, 더 많은 유연성과 제어권을 제공합니다. 또한 ElasticSearch Service보다 비용이 높을 수 있으며, 클러스터 운영에 대한 책임이 사용자에게 있습니다.

* Grafana의 Panel 형식에는 어떤 것이 있을까요? 로그를 보기에 적합한 판넬은 어떤 형태일까요?
    * Grafana의 Panel 형식에는 다양한 유형이 있습니다.

    * Graph Panel: 데이터를 그래프로 표현합니다.
    * Singlestat Panel: 특정 값의 수치를 보여줍니다.
    * Table Panel: 데이터를 표로 보여줍니다.
    * Heatmap Panel: 열 지도 형식으로 데이터를 시각화합니다.
    * Text Panel: 텍스트 형식으로 데이터를 표시합니다.
    * Alert List Panel: 알림 목록을 보여줍니다.
    * Dashlist Panel: 대시보드 목록을 보여줍니다.
    * Plugin Panels: 사용자가 개발한 또는 제3자가 제공하는 패널입니다.
    * 로그를 보기에 적합한 판넬은 로그 데이터를 시간순으로 나열할 수 있는 Graph Panel과 Log Panel이 있습니다. Graph Panel은 시간에 따른 로그 데이터의 변화를 쉽게 확인할 수 있습니다. Log Panel은 로그 데이터를 텍스트 형식으로 보여주며, 필터링 기능을 통해 원하는 로그만 볼 수 있도록 도와줍니다.


## Quest
* 우리의 웹 서버가 stdout으로 적절한 로그를 남기도록 해 보세요.
* ElasticSearch Service 클러스터를 작은 사양으로 하나 만들고, 도커 컨테이너의 stdout으로 출력된 로그가 ElasticSearch로 스트리밍 되도록 해 보세요.
* Grafana를 이용해 ElasticSearch의 로그를 실시간으로 볼 수 있는 페이지를 만들어 보세요.

## Advanced
* ElasticSearch와 Grafana는 어떤 라이센스로 배포되고 있을까요? AWS와 같은 클라우드 제공자들이 이러한 오픈소스를 서비스화 하는 것을 둘러싼 논란은 어떤 논점일까요?
