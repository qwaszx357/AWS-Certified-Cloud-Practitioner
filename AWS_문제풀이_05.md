# AWS 문제 풀이

### 2022.11.15

#### #71

솔루션 아키텍트가 다가올 음악 행사를 위해 웹사이트를 최적화하고 있습니다. 공연 영상은 실시간으로 스트리밍되며 주문형으로 제공된다. 이 행사는 전 세계 온라인 청중을 끌어들일 것으로 예상됩니다.
실시간 및 주문형 스트리밍의 성능을 모두 향상시키는 서비스는 무엇입니까?

- A. 아마존 클라우드프론트

> CloudFront를 사용하여 모든 HTTP 오리진을 사용하여 주문형 비디오(VOD) 또는 라이브 스트리밍 비디오를 제공할 수 있습니다. 클라우드에서 비디오 워크플로를 설정할 수 있는 한 가지 방법은 CloudFront를 AWS Media Services와 함께 사용하는 것입니다.

#### #72

회사에 3계층 이미지 공유 애플리케이션이 있습니다. 프런트 엔드 계층에 Amazon EC2 인스턴스를 사용하고, 백엔드 계층에 또 다른 인스턴스를 사용하고, MySQL 데이터베이스에 세 번째 인스턴스를 사용합니다. 솔루션 설계자는 가용성이 높고 응용 프로그램에 최소한의 변경만 필요한 솔루션을 설계하는 임무를 맡았습니다.
이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

- D. 프런트엔드 및 백엔드 계층에 로드 밸런싱된 다중 AZ AWS Elastic Beanstalk 환경을 사용합니다. 다중 AZ 배포를 통해 데이터베이스를 Amazon RDS 인스턴스로 이동합니다. Amazon S3를 사용하여 사용자 이미지를 저장하고 제공합니다.

> "가용성이 높으며 응용 프로그램에 대한 변경이 가장 적습니다."입니다. 따라서 "고가용성"의 경우: 다중 AZ 및 "애플리케이션에 대한 최소 변경 사항"의 경우: Elastic Beanstalk가 용량 프로비저닝, 로드 밸런싱, 자동 확장에서 애플리케이션 상태 모니터링에 이르기까지 배포를 자동으로 처리합니다.

#### #73

솔루션 설계자는 시장이 폐쇄된 동안 금융 시장의 성과를 분석하는 시스템을 설계하고 있습니다. 시스템은 매일 밤 4시간 동안 일련의 컴퓨팅 집약적인 작업을 실행합니다. 컴퓨팅 작업을 완료하는 시간은 일정하게 유지될 것으로 예상되며 일단 시작된 작업은 중단될 수 없습니다. 완료되면 시스템은 최소 1년 동안 실행될 것으로 예상됩니다.
시스템 비용을 줄이기 위해 어떤 유형의 Amazon EC2 인스턴스를 사용해야 합니까?

- D. 예약된 예약 인스턴스

> "표준 예약 인스턴스"는 워크로드가 하루에 4시간 동안만 실행되므로 더 비쌉니다. "온디맨드 인스턴스"는 할인이 적용되지 않기 때문에 훨씬 더 비쌀 수 있으므로 올바르지 않습니다.  워크로드가 일단 시작되면 중단될 수 없으므로 "스팟 인스턴스"는 올바르지 않습니다. 스팟 인스턴스를 사용하면 스팟 가격이 변경되거나 용량이 필요한 경우 워크로드를 종료할 수 있습니다.

#### #74

한 회사에서 사용자 데이터를 캡처하고 향후 분석을 위해 저장하는 음식 주문 애플리케이션을 구축했습니다. 애플리케이션의 정적 프런트 엔드는 Amazon EC2 인스턴스에 배포됩니다. 프런트 엔드 애플리케이션은 별도의 EC2 인스턴스에서 실행되는 백엔드 애플리케이션에 요청을 보냅니다. 그런 다음 백엔드 애플리케이션은 데이터를 Amazon RDS에 저장합니다.
아키텍처를 분리하고 확장 가능하게 만들기 위해 솔루션 설계자는 무엇을 해야 합니까?

- D. Amazon S3를 사용하여 정적 프런트 엔드 애플리케이션을 제공하고 요청을 Amazon SQS 대기열에 쓰는 Amazon API Gateway로 요청을 보냅니다. 백엔드 인스턴스를 Auto Scaling 그룹에 배치하고 대기열 깊이에 따라 확장하여 Amazon RDS에서 데이터를 처리하고 저장합니다.

> 정적 프런트 엔드이므로 S3를 사용하고 싶으므로 C를 자동으로 배제합니다. 여기에서 키워드는 SQS를 찾을 때마다 "분리"입니다.

#### #75

솔루션 설계자는 고성능 머신 러닝 기능을 포함하는 회사 애플리케이션용 관리형 스토리지 솔루션을 설계해야 합니다. 이 애플리케이션은 AWS Fargate에서 실행되며 연결된 스토리지는 파일에 동시에 액세스하고 고성능을 제공해야 합니다.
솔루션 설계자는 어떤 스토리지 옵션을 권장해야 합니까?

- C. Amazon Elastic File System(Amazon EFS) 파일 공유를 생성하고 Fargate가 Amazon Elastic File System(Amazon EFS)과 통신할 수 있도록 IAM 역할을 설정합니다.

> Fargat는 광택에 대해 지원되지 않으며 "동시 파일 액세스를 지원하고 우수한 성능을 제공해야 합니다." 그것은 HPC를 말하지 않았다

#### #76

자전거 공유 회사는 피크 운영 시간 동안 자전거의 위치를 추적하기 위해 다층 아키텍처를 개발하고 있습니다. 회사는 기존 분석 플랫폼에서 이러한 데이터 포인트를 사용하려고 합니다. 솔루션 설계자는 이 아키텍처를 지원하기 위해 가장 실행 가능한 다중 계층 옵션을 결정해야 합니다. 데이터 포인트는 REST API에서 액세스할 수 있어야 합니다.
위치 데이터 저장 및 검색에 대한 이러한 요구 사항을 충족하는 작업은 무엇입니까?

- D. Amazon Kinesis Data Analytics와 함께 Amazon API Gateway를 사용합니다.

> Athena는 쿼리를 실행하기 위해 REST API를 제공하고 질문에서 요청한 대로 데이터 포인트를 노출하지 않습니다.

#### #77

솔루션 아키텍트는 ALB(Application Load Balancer) 뒤의 Amazon EC2 인스턴스에서 실행될 웹 애플리케이션을 설계하고 있습니다. 회사는 응용 프로그램이 악의적인 인터넷 활동 및 공격에 대해 복원력이 있고 새로운 일반적인 취약성 및 노출로부터 보호할 것을 엄격히 요구합니다.
솔루션 설계자는 무엇을 추천해야 합니까?

- C. AWS Shield Advanced에 가입하고 일반적인 취약성과 노출이 차단되었는지 확인합니다.

> 관리형 규칙은 위협 및 취약성에 대한 광범위한 최신 지식을 보유한 보안 전문가가 작성합니다. 규칙은 많은 고객에게서 관찰된 위협을 기반으로 작성됩니다. AWS WAF 관리형 규칙은 새로운 취약성과 악의적인 행위자가 나타나면 AWS 판매자가 자동으로 업데이트합니다.

#### #78

회사에 AWS Lambda 함수를 호출하는 애플리케이션이 있습니다. 코드 검토 결과 데이터베이스 자격 증명이 Lambda 함수의 소스 코드에 저장되어 회사의 보안 정책을 위반하는 것으로 나타났습니다. 자격 증명은 안전하게 저장되어야 하며 보안 정책 요구 사항을 충족하기 위해 지속적으로 자동 교체되어야 합니다.
가장 안전한 방식으로 이러한 요구 사항을 충족하기 위해 솔루션 설계자는 무엇을 권장해야 합니까?

- B. AWS Secrets Manager에 암호를 저장합니다. 비밀 ID를 사용하여 Secrets Manager에서 암호를 검색할 수 있는 역할과 Lambda 함수를 연결합니다. Secrets Manager를 사용하여 암호를 자동으로 교체하십시오.

> AWS Secrets Manager Secrets Manager - 암호화해야 하는 기밀 정보(예: 데이터베이스 자격 증명, API 키)용으로 특별히 설계되었으므로 암호 항목 생성 시 기본적으로 암호화가 활성화됩니다. 또한 키 회전과 같은 추가 기능을 제공합니다.

#### #79

회사는 온프레미스에서 의료 기록을 관리하고 있습니다. 회사는 이러한 기록을 무기한으로 유지하고 일단 저장되면 기록에 대한 수정을 비활성화하고 모든 수준에서 세분화된 액세스를 감사해야 합니다. 최고 기술 책임자(CTO)는 이미 수백만 개의 레코드가 어떤 애플리케이션에서도 사용되지 않고 있고 현재 인프라의 공간이 부족하기 때문에 우려하고 있습니다. CTO는 솔루션 설계자에게 기존 데이터를 이동하고 향후 기록을 지원하는 솔루션을 설계하도록 요청했습니다.
이러한 요구 사항을 충족하기 위해 솔루션 설계자가 추천할 수 있는 서비스는 무엇입니까?

- A. AWS DataSync를 사용하여 기존 데이터를 AWS로 이동합니다. Amazon S3를 사용하여 기존 데이터와 새 데이터를 저장합니다. Amazon S3 객체 잠금을 활성화하고 데이터 이벤트로 AWS CloudTrail을 활성화합니다.

> "AWS DataSync를 사용하여 기존 데이터를 Amazon S3로 마이그레이션한 다음 AWS Storage Gateway의 파일 게이트웨이 구성을 사용하여 마이그레이션된 데이터에 대한 액세스 권한을 유지하고 온프레미스 파일 기반 애플리케이션에서 지속적으로 업데이트합니다." 기존 데이터를 이동하고 향후 레코드를 지원하는 솔루션이 필요하므로 마이그레이션에 AWS DataSync를 사용해야 합니다. 모든 수준에서 세분화된 감사 액세스 필요 -> 데이터 이벤트는 CloudTrail에서 사용해야 하며 관리 이벤트는 기본적으로 활성화됩니다.

#### #80

회사에서 온프레미스 데이터 세트의 보조 사본으로 Amazon S3를 사용하려고 합니다. 회사는 이 복사본에 액세스할 필요가 거의 없습니다. 스토리지 솔루션의 비용은 최소화되어야 합니다.
이러한 요구 사항을 충족하는 스토리지 솔루션은 무엇입니까?

- D. S3 One Zone-Infrequent Access(S3 One Zone-IA)

> S3 One Zone-Infrequent Access(S3 One Zone-IA) 최소 비용입니다. 복원력에 대한 언급이 없으므로 S3 Standard IA가 필요하지 않습니다.