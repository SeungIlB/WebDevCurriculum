# Quest 17-B. 배포 파이프라인

## Introduction
* 이번 퀘스트에서는 CI/CD 파이프라인이 왜 필요한지, 어떻게 구축할 수 있는지 등에 대해 다룹니다.

## Topics
* Continuous Integration
* Continuous Delivery
* AWS Codebuild

## Resources
* [AWS: Continuous Integration](https://aws.amazon.com/ko/devops/continuous-integration/)
* [AWS: Continuous Delivery](https://aws.amazon.com/ko/devops/continuous-delivery/)
* [AWS Codebuild](https://aws.amazon.com/ko/codebuild/getting-started/)

## Checklist
* CI/CD는 무엇일까요? CI/CD 시스템을 구축하면 어떤 장점이 있을까요?
    * CI/CD는 지속적 통합 (Continuous Integration)과 지속적 배포 (Continuous Deployment 또는 Delivery)를 의미합니다. 소프트웨어 개발 프로세스에서 코드 변경 사항을 자동으로 빌드, 테스트 및 배포하는 것을 자동화함으로써 소프트웨어 개발 및 배포의 효율성과 안정성을 높이는 것을 목적으로 합니다.

    * CI/CD를 구축하면 다음과 같은 장점이 있습니다.

    * 코드 품질 개선: CI/CD 시스템을 통해 코드 변경 사항이 자동으로 빌드되고 테스트되므로 오류를 조기에 발견하고 수정할 수 있습니다. 이로 인해 코드의 품질이 개선되고 버그의 수가 줄어듭니다.

    * 소프트웨어 배포의 안정성 확보: CI/CD 시스템을 사용하면 자동으로 빌드, 테스트, 배포를 수행하므로 배포 과정에서 인간의 실수나 간과할 수 있는 문제를 사전에 방지할 수 있습니다.

    * 개발과 운영의 통합: CI/CD 시스템을 사용하면 개발자와 운영팀 간의 협력이 원활해지며, 더 빠르고 안정적인 소프트웨어 배포가 가능해집니다.

    * 빠른 소프트웨어 개발과 배포: CI/CD 시스템을 사용하면 개발자들은 더 빠르게 코드 변경 사항을 테스트하고 프로덕션 환경에 더 빠르게 배포할 수 있습니다.

    * 개발자 생산성 향상: CI/CD 시스템을 사용하면 개발자는 소프트웨어 배포 프로세스의 자동화로 인해 반복적인 작업을 줄일 수 있으며, 더욱 효율적으로 개발할 수 있습니다.

* CI 시스템인 Travis CI, Jenkins, Circle CI, Github Actions, AWS Codebuild 의 차이점과 장단점은 무엇일까요?
    * Travis CI, Jenkins, Circle CI, Github Actions, AWS Codebuild 모두 CI/CD 시스템으로 자동화된 빌드, 테스트 및 배포를 지원하는 도구입니다. 각각의 시스템은 다음과 같은 특징을 가지고 있습니다.
    ```
    Travis CI
    무료 및 유료 서비스 제공
    깃헙과 연동되어 사용하기 쉽고 Github 저장소에 대한 지원이 우수함
    단순한 빌드 및 배포 프로세스에 적합함
    더 복잡한 CI/CD 프로세스에 대한 확장성이 떨어질 수 있음
    ```
    ```
    Jenkins
    오픈소스로 무료로 사용 가능
    대부분의 플러그인과 도구 지원
    다양한 통합 및 배포 시스템과 연동 가능
    다양한 커뮤니티 지원 및 다양한 튜토리얼, 문서 제공
    초기 설정이 복잡하고 유지보수가 필요함
    ```
    ```
    Circle CI
    클라우드 기반의 서비스로 무료와 유료 버전이 있음
    깃헙과 연동되어 사용하기 쉬움
    사용자 친화적인 웹 인터페이스 제공
    복잡한 CI/CD 프로세스에 대한 확장성이 높음
    ```
    ```
    Github Actions
    깃헙과 연동되어 사용하기 쉬움
    다양한 운영체제와 프로그래밍 언어 지원
    Github에서 바로 CI/CD 시스템을 사용할 수 있어서 개발자들이 가장 많이 사용하는 CI/CD 시스템 중 하나
    무료로 사용 가능
    ```
    ```
    AWS Codebuild
    아마존 웹 서비스(AWS)의 서비스 중 하나
    AWS 클라우드 환경에서 작동하며 AWS의 다른 서비스와 연동이 용이함
    다양한 커스터마이징 및 구성 옵션 제공
    비교적 복잡한 설정 및 구성이 필요하며 비용이 발생할 수 있음
    각각의 시스템은 다양한 특징과 장단점을 가지고 있으며, 프로젝트의 요구사항에 따라 선택할 수 있습니다.
    ```


## Quest
* AWS Codebuild를 이용하여, 특정 브랜치에 푸시를 하면 린트와 테스트를 거쳐 서버 이미지를 빌드한 뒤, 직전 퀘스트의 EC2 인스턴스에 배포되는 시스템을 만들어 보세요.

## Advanced
* 빅테크 회사들이 코드를 빌드하고 배포하는 시스템은 어떻게 설계되고 운영되고 있을까요?
