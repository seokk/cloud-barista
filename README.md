# Cloud-Barista 

The Multi-Cloud Service Platform.

Cloub-Barista consists of multiple frameworks (sub-systems) to accommodate microservice architecture (MSA).

Main frameworks are as follow,

1. CB-Spider (connects all clouds in a single interface)
1. CB-Tumblebug (manages multi-cloud resource and provides multi-cloud infra services)
1. CB-Tumblebug/cb-milkyway (CB-Tumblebug benchmark agent)
1. CB-Dragonfly (monitors multi-cloud service)
1. CB-Waterstrider/cb-webtool (provides a GUI to Cloud-Barista users)
1. CB-Bridge/cb-operator (operation tool for Cloud-Barista system runtime)
1. CB-Bridge/cb-store (provides an unified DB interface for meta info of Cloud-Barista)
1. CB-Bridge/cb-log (provides log system)

The frameworks are listed in the root directory.

```
[NOTE]
Cloub-Barista is currently under development. (the latest version is 0.2.0-cappuccino)
So, we do not recommend using the current release in production.
Please note that the functionalities of Cloub-Barista are not stable and secure yet.
If you have any difficulties in using Cloub-Barista, please let us know.
(Open an issue or Join the Cloub-Barista Slack)
```

***

## [목    차]

1. [설치 환경](#설치-환경)
1. [설치 및 실행](#설치-및-실행)
1. [API 및 문서](#API-및-문서)
1. [특이 사항](#특이-사항)
1. [사용 방법 및 예시](#사용-방법-및-예시)

***

## [설치 환경]

- 리눅스(검증시험: Ubuntu 18.04)

## [설치 및 실행]

- Cloud-Barista 플랫폼 통합 실행 (Docker 이미지 기반)
  - cb-operator 를 통해 Cloud-Barista 전체 FW를 통합 실행할 수 있음
    - 참고: [cloud-barista/cb-operator](/cb-operator/)

- Cloud-Barista 플랫폼 개별 FW 소스 다운로드 및 설치
  - CB-Log 설치
    - [cloud-barista/cb-log README를 참고하여 설치](/cb-log/)
  
  - CB-Store 설치
    - [cloud-barista/cb-store README를 참고하여 설치](/cb-store/)

  - CB-Spider 설치 및 실행
    - [cloud-barista/cb-spider README를 참고하여 설정, 설치](/cb-spider/)
    - cb-spider 실행 (cb-spider API 서버 실행)

  - CB-Tumblebug 설치 및 실행
    - [cloud-barista/cb-tumblebug README를 참고하여 설정, 설치](/cb-tumblebug/)
      - cb-spider API 서버 주소를 cb-tumblebug의 setup.env에 설정
    - cb-tumblebug 실행 (cb-tumblebug API 서버 실행)

  - CB-Dragonfly 설치 및 실행
    - [cloud-barista/cb-dragonfly README를 참고하여 설정, 설치](/cb-dragonfly/)
    - cb-dragonfly 실행 (cb-dragonfly API 서버 실행)

  - CB-Webtool 설치 및 실행
    - [cloud-barista/cb-webtool README를 참고하여 설정, 설치](/cb-webtool/)
    - cb-webtool 실행 (cb-webtool GUI 서버 실행)



## [API 및 문서]
- 문서 통합 Repository
  - [github.com/cloud-barista/docs](https://github.com/cloud-barista/docs)
- API 규격
  - [github.com/cloud-barista/docs/blob/master/technical_docs/API/User-REST-API(v0.2.0-cappuccino).md](https://github.com/cloud-barista/docs/blob/master/technical_docs/API/User-REST-API(v0.2.0-cappuccino).md)

## [특이 사항]
- 개발상태: 초기 기능 중심 개발 추진 중 / 기술 개발용 / 상용 활용시 보완필요
- CSP별 연동 검증 상태
  - CB-Tumblebug 기준 테스트 완료된 CSP는 AWS, GCP, Azure, Alibaba 임
  - 현재는 개발 단계의 버전이므로 안정성에는 문제가 발생할 수 있음

## [사용 방법 및 예시]

### [사용 방법 1] 각 FW의 REST API를 통한 운용
- CB-Spider API를 통해 클라우드 인프라 연동 정보 등록
   - [cloud-barista.github.io/rest-api/v0.2.0/spider/ccim/](https://cloud-barista.github.io/rest-api/v0.2.0/spider/ccim/)
- CB-Tumblebug 멀티 클라우드 네임스페이스 관리 API를 통해서 Namespace 생성
   - [cloud-barista.github.io/rest-api/v0.2.0/tumblebug/namespace/](https://cloud-barista.github.io/rest-api/v0.2.0/tumblebug/namespace/)
- CB-Tumblebug 멀티 클라우드 인프라 자원(MCIR) 관리 API를 통해서 VM 생성을 위한 자원 (MCIR) 생성
   - [cloud-barista.github.io/rest-api/v0.2.0/tumblebug/mcir/](https://cloud-barista.github.io/rest-api/v0.2.0/tumblebug/mcir/)
- CB-Tumblebug 멀티 클라우드 인프라 서비스(MCIS) 관리 API를 통해서 MCIS 생성, 조회, 제어, 원격명령수행, 종료
   - [cloud-barista.github.io/rest-api/v0.2.0/tumblebug/mcis/](https://cloud-barista.github.io/rest-api/v0.2.0/tumblebug/mcis/)

### [사용 방법 2] CB-Tumblebug 테스트 스크립트를 통한 운용
- [cloud-barista/cb-tumblebug/test/official/](/cb-tumblebug/test/official/)
   - 클라우드 인증 정보, 테스트 기본 정보 입력
   - 개별 수동 제어: 클라우드정보, Namespace, MCIR, MCIS 등 제어 (개별 시험시, 오브젝트들의 의존성 고려 필요))
   - 통합 자동 제어: 의존성을 고려한 자동 통합 제어 (추천 테스트 방법)
     - [cloud-barista/cb-tumblebug/test/official/sequentialFullTest](/cb-tumblebug/test/official/sequentialFullTest)

#### 1) 클라우드 인증 정보, 테스트 기본 정보 입력
- [cloud-barista/cb-tumblebug/test/official/](/cb-tumblebug/test/official/) 이동
- [credentials.conf](/cb-tumblebug/test/official/credentials.conf)  # Cloud 정보 등록을 위한 CSP별 인증정보 (사용자에 맞게 수정 필요)
   - 기본적인 클라우드 타입 (AWS, GCP, AZURE, ALIBABA)에 대해 템플릿 제공
- [conf.env](/cb-tumblebug/test/official/conf.env)  # CB-Spider 및 Tumblebug 서버 위치, 클라우드 리젼, 테스트용 이미지명, 테스트용 스팩명 등 테스트 기본 정보 제공
   - 특별한 상황이 아니면 수정이 불필요함. (CB-Spider와 CB-TB의 위치가 localhost가 아닌 경우 수정 필요)
   - 클라우드 타입(CSP)별 약 1~3개의 기본 리전이 입력되어 있음
     - 이미지와 스팩은 리전에 의존성이 있는 경우가 많으므로, 리전별로 지정이 필요

#### 2) 개별 수동 제어 또는 통합 자동 제어

##### [개별 수동 제어] 클라우드정보, Namespace, MCIR, MCIS 등 개별 제어
- 제어하고 싶은 리소스 오브젝트에 대해, 해당 디렉토리로 이동하여 필요한 제어 수행
  - 오브젝트는 서로 의존성이 있으므로, 번호를 참고하여 오름차순으로 수행하는 것이 바람직함
    - 0.settingSpider  # 클라우드 정보 등록 관련 스크립트 모음
    - 0.settingTB  # 네임스페이스 관련 스크립트 모음
    - 1.vNet  # MCIR vNet 생성 관련 스크립트 모음
    - 2.securityGroup  # MCIR securityGroup 생성 관련 스크립트 모음
    - 3.sshKey  # MCIR sshKey 생성 관련 스크립트 모음
    - 4.image  # MCIR image 등록 관련 스크립트 모음
    - 5.spec  # MCIR spec 등록 관련 스크립트 모음
    - 6.mcis  # MCIS 생성 및 제어 관련 스크립트 모음

##### [통합 자동 제어] 의존성을 고려한 자동 통합 제어 (추천 테스트 방법)
- [sequentialFullTest](/cb-tumblebug/test/official/sequentialFullTest) 에 포함된 [testAll-mcis-mcir-ns-cloud.sh](/cb-tumblebug/test/official/sequentialFullTest/testAll-mcis-mcir-ns-cloud.sh) 을 수행하면 모든 것을 한번에 제어 및 테스트 가능
```
└── sequentialFullTest  # Cloud 정보 등록, NS 생성, MCIR 생성, MCIS 생성까지 한번에 자동 테스트
    ├── cleanAll-mcis-mcir-ns-cloud.sh  # 모든 오브젝트 역으로 제어
    ├── command-mcis.sh  # 생성된 MCIS(다중VM)에 원격 명령 수행
    ├── deploy-nginx-mcis.sh  # 생성된 MCIS(다중VM)에 Nginx 자동 배포
    ├── executionStatus  # 수행이 진행된 테스트 로그 (testAll 수행시 정보가 추가되며, cleanAll 수행시 정보가 제거됨)
    ├── testAll-mcis-mcir-ns-cloud.sh  # Cloud 정보 등록, NS 생성, MCIR 생성, MCIS 생성까지 한번에 자동 테스트
    ├── test-cloud.sh
    ├── test-mcir-ns-cloud.sh
    └── test-ns-cloud.sh
```
- 사용 예시
  - 생성 테스트
    - ./testAll-mcis-mcir-ns-cloud.sh aws 1 shson       # aws의 1번 리전에 shson이라는 개발자명으로 테스트 수행
    - ./testAll-mcis-mcir-ns-cloud.sh aws 2 shson       # aws의 2번 리전에 shson이라는 개발자명으로 테스트 수행
    - ./testAll-mcis-mcir-ns-cloud.sh aws 3 shson       # aws의 3번 리전에 shson이라는 개발자명으로 테스트 수행
    - ./testAll-mcis-mcir-ns-cloud.sh gcp 1 shson       # gcp의 1번 리전에 shson이라는 개발자명으로 테스트 수행
    - ./testAll-mcis-mcir-ns-cloud.sh gcp 2 shson       # gcp의 2번 리전에 shson이라는 개발자명으로 테스트 수행
    - ./testAll-mcis-mcir-ns-cloud.sh azure 1 shson     # azure의 1번 리전에 shson이라는 개발자명으로 테스트 수행
    - ./testAll-mcis-mcir-ns-cloud.sh alibaba 1 shson   # alibaba의 1번 리전에 shson이라는 개발자명으로 테스트 수행
  - 제거 테스트 (이미 수행이 진행된 클라우드타입/리전/개발자명 으로만 삭제 진행이 필요)
    - ./cleanAll-mcis-mcir-ns-cloud.sh aws 1 shson       # aws의 1번 리전에 shson이라는 개발자명으로 제거 테스트 수행
    - ./cleanAll-mcis-mcir-ns-cloud.sh aws 2 shson       # aws의 2번 리전에 shson이라는 개발자명으로 제거 테스트 수행
    - ./cleanAll-mcis-mcir-ns-cloud.sh aws 3 shson       # aws의 3번 리전에 shson이라는 개발자명으로 제거 테스트 수행
    - ./cleanAll-mcis-mcir-ns-cloud.sh gcp 1 shson       # gcp의 1번 리전에 shson이라는 개발자명으로 제거 테스트 수행
    - ./cleanAll-mcis-mcir-ns-cloud.sh gcp 2 shson       # gcp의 2번 리전에 shson이라는 개발자명으로 제거 테스트 수행
    - ./cleanAll-mcis-mcir-ns-cloud.sh azure 1 shson     # azure의 1번 리전에 shson이라는 개발자명으로 제거 테스트 수행
    - ./cleanAll-mcis-mcir-ns-cloud.sh alibaba 1 shson   # alibaba의 1번 리전에 shson이라는 개발자명으로 제거 테스트 수행
<details>
<summary>입출력 예시 보기</summary>

```
~/go/src/github.com/cloud-barista/cb-tumblebug/test/official/sequentialFullTest$ ./testAll-mcis-mcir-ns-cloud.sh aws 1 shson
####################################################################
## Create MCIS from Zero Base
####################################################################
[Test for AWS]
####################################################################
## 0. Create Cloud Connction Config
####################################################################
[Test for AWS]
{
   "ProviderName" : "AWS",
   "DriverLibFileName" : "aws-driver-v1.0.so",
   "DriverName" : "aws-driver01"
}
..........
   "RegionName" : "aws-us-east-1"
}
{
   "CredentialName" : "aws-credential01",
   "RegionName" : "aws-us-east-1",
   "DriverName" : "aws-driver01",
   "ConfigName" : "aws-us-east-1",
   "ProviderName" : "AWS"
}
####################################################################
## 0. Namespace: Create
####################################################################
{
   "message" : "The namespace NS-01 already exists."
}
####################################################################
## 1. vpc: Create
####################################################################
[Test for AWS]
{
   "subnetInfoList" : [
      {
         "IId" : {
            "SystemId" : "subnet-0ab25b7090afa97b7",
            "NameId" : "aws-us-east-1-shson"
         },
................
   "status" : "",
   "name" : "aws-us-east-1-shson",
   "keyValueList" : null,
   "connectionName" : "aws-us-east-1",
   "cspVNetId" : "vpc-0e3004f28e8a89057"
}
Dozing for 10 : 1 2 3 4 5 6 7 8 9 10 (Back to work)
####################################################################
## 2. SecurityGroup: Create
####################################################################
[Test for AWS]
{
   "keyValueList" : [
      {
         "Value" : "aws-us-east-1-shson-delimiter-aws-us-east-1-shson",
         "Key" : "GroupName"
      },
      {
         "Key" : "VpcID",
...........
   "name" : "aws-us-east-1-shson",
   "description" : "test description",
   "cspSecurityGroupId" : "sg-033e4b7c42671873c",
   "id" : "aws-us-east-1-shson"
}
Dozing for 10 : 1 2 3 4 5 6 7 8 9 10 (Back to work)
####################################################################
## 3. sshKey: Create
####################################################################
[Test for AWS]
{
   "name" : "aws-us-east-1-shson",
   "fingerprint" : "d2:1a:a0:6d:b3:f7:8e:b7:44:9f:13:9c:d6:e3:a8:c3:58:8c:de:27",
..............
   "id" : "aws-us-east-1-shson",
   "description" : "",
   "privateKey" : "-----BEGIN RSA PRIVATE KEY-----\nMIIEogIBAAKCAQEAopGlO3dUrB4AMcBr4XZg0OVrveecA9Hv0/a9GmxgXU5dx42YV4DwW7oq/+Dq\nPaCSXvGGtdVHuL0hoOKdGYOx89qzi+nUgNQup+pKLbQw4aU2gVbV1/3/ejt7tYRUeWNU9c4b7m7E\nfs3A0xgfmak90eoQen+TJYhkfdWcSwkmJSH61bEFRbdeyijEODCu0TAGDrtRZzdCRUzbA/N7FjsC\ns0a1C...LpszE9J0bfhLOqgmkYNGSw4oR+gPRIsipUK6SzaRH7nFnOSw=\n-----END RSA PRIVATE KEY-----",
   "username" : ""
}
####################################################################
## 4. image: Register
####################################################################
[Test for AWS]
{
   "keyValueList" : [
      {
         "Key" : "",
         "Value" : ""
      },
      {
         "Value" : "",
         "Key" : ""
      }
   ],
   "description" : "Canonical, Ubuntu, 18.04 LTS, amd64 bionic",
   "cspImageName" : "",
   "connectionName" : "aws-us-east-1",
   "status" : "",
   "creationDate" : "",
   "cspImageId" : "ami-085925f297f89fce1",
   "name" : "aws-us-east-1-shson",
   "guestOS" : "Ubuntu",
   "id" : "aws-us-east-1-shson"
}
####################################################################
## 5. spec: Register
####################################################################
[Test for AWS]
{
   "mem_MiB" : "1024",
   "max_num_storage" : "",
........
   "mem_GiB" : "1",
   "id" : "aws-us-east-1-shson",
   "num_core" : "",
   "cspSpecName" : "t2.micro",
   "storage_GiB" : "",
   "ebs_bw_Mbps" : "",
   "connectionName" : "aws-us-east-1",
   "net_bw_Gbps" : "",
   "gpu_model" : "",
   "cost_per_hour" : "",
   "name" : "aws-us-east-1-shson"
}
####################################################################
## 6. vm: Create MCIS
####################################################################
[Test for AWS]
{
   "targetAction" : "Create",
   "status" : "Running-(3/3)",
   "id" : "aws-us-east-1-shson",
   "name" : "aws-us-east-1-shson",
   "description" : "Tumblebug Demo",
   "targetStatus" : "Running",
   "placement_algo" : "",
   "vm" : [
      {
         "vmUserId" : "",
         "targetStatus" : "None",
         "subnet_id" : "aws-us-east-1-shson",
         "location" : {
            "nativeRegion" : "us-east-1",
            "cloudType" : "aws",
            "latitude" : "38.1300",
            "briefAddr" : "Virginia",
            "longitude" : "-78.4500"
         },
         "vm_access_id" : "",
         "region" : {
            "Region" : "us-east-1",
            "Zone" : "us-east-1f"
         },
         "image_id" : "aws-us-east-1-shson",
         "privateDNS" : "ip-192-168-1-108.ec2.internal",
         "vmBootDisk" : "/dev/sda1",
         "status" : "Running",
         "security_group_ids" : [
            "aws-us-east-1-shson"
         ],
         "vm_access_passwd" : "",
 .........
            "VMUserId" : "",
            "SecurityGroupIIds" : [
               {
                  "SystemId" : "sg-033e4b7c42671873c",
                  "NameId" : "aws-us-east-1-shson"
               }
            ],
            "VMBootDisk" : "/dev/sda1",
            "PrivateDNS" : "ip-192-168-1-108.ec2.internal",
            "StartTime" : "2020-05-30T18:33:42Z",
            "VMBlockDisk" : "/dev/sda1",
            "ImageIId" : {
               "SystemId" : "ami-085925f297f89fce1",
               "NameId" : "ami-085925f297f89fce1"
            }
         },
         "publicIP" : "35.173.215.4",
         "name" : "aws-us-east-1-shson-01",
         "id" : "aws-us-east-1-shson-01",
         "vnet_id" : "aws-us-east-1-shson",
         "ssh_key_id" : "aws-us-east-1-shson",
         "privateIP" : "192.168.1.108",
         "config_name" : "aws-us-east-1",
         "vmBlockDisk" : "/dev/sda1",
         "targetAction" : "None",
         "description" : "description",
         "spec_id" : "aws-us-east-1-shson",
         "publicDNS" : "",
         "vmUserPasswd" : ""
      },
      {
         "vmBlockDisk" : "/dev/sda1",
         "targetAction" : "None",
         "description" : "description",
         "spec_id" : "aws-us-east-1-shson",
         "vmUserPasswd" : "",
         ..........
      }
   ]
}
Dozing for 1 : 1 (Back to work)
####################################################################
## 6. VM: Status MCIS
####################################################################
[Test for AWS]
{
   "targetStatus" : "None",
   "id" : "aws-us-east-1-shson",
   "targetAction" : "None",
   "vm" : [
      {
         "public_ip" : "35.173.215.4",
         "native_status" : "Running",
         "csp_vm_id" : "aws-us-east-1-shson-01",
         "name" : "aws-us-east-1-shson-01",
         "status" : "Running",
         "targetAction" : "None",
         "targetStatus" : "None",
         "id" : "aws-us-east-1-shson-01"
      },
      {
         "name" : "aws-us-east-1-shson-02",
         "status" : "Running",
         "targetAction" : "None",
         "targetStatus" : "None",
         "id" : "aws-us-east-1-shson-02",
         "public_ip" : "18.206.13.233",
         "csp_vm_id" : "aws-us-east-1-shson-02",
         "native_status" : "Running"
      },
      {
         "targetAction" : "None",
         "id" : "aws-us-east-1-shson-03",
         "targetStatus" : "None",
         "name" : "aws-us-east-1-shson-03",
         "status" : "Running",
         "csp_vm_id" : "aws-us-east-1-shson-03",
         "native_status" : "Running",
         "public_ip" : "18.232.53.134"
      }
   ],
   "status" : "Running-(3/3)",
   "name" : "aws-us-east-1-shson"
}

[Logging to notify latest command history]

[Executed Command List]
[CMD] testAll-mcis-mcir-ns-cloud.sh gcp 1 shson
[CMD] testAll-mcis-mcir-ns-cloud.sh alibaba 1 shson
[CMD] testAll-mcis-mcir-ns-cloud.sh aws 1 shson
```

마지막의 [Executed Command List] 에는 수행한 커맨드의 히스토리가 포함됨. 
(cat ./executionStatus 를 통해 다시 확인 가능)
      
</details>


#### 3) MCIS 기반 애플리케이션 운용 방법 및 최종 검증

  - SSH 원격 커맨드 실행을 통해서 접속 여부 등을 확인 가능
    - [command-mcis.sh](/cb-tumblebug/test/official/sequentialFullTest/command-mcis.sh)  # 생성된 MCIS(다중VM)에 원격 명령 수행
    - 예시: command-mcis.sh aws 1 shson # aws의 1번 리전에 배치된 MCIS의 모든 VM에 IP 및 Hostname 조회를 수행
  - Nginx를 분산 배치하여, 웹서버 접속 시험이 가능
    - [deploy-nginx-mcis.sh](/cb-tumblebug/test/official/sequentialFullTest/deploy-nginx-mcis.sh)  # 생성된 MCIS(다중VM)에 Nginx 자동 배포
    - 예시: command-mcis.sh aws 1 shson # aws의 1번 리전에 배치된 MCIS의 모든 VM에 Nginx 및 웹페이지 설치 (접속 테스트 가능)
      ```
      ~/go/src/github.com/cloud-barista/cb-tumblebug/test/official/sequentialFullTest$ ./deploy-nginx-mcis.sh aws 1 shson
      ####################################################################
      ## Command (SSH) to MCIS 
      ####################################################################
      [Test for AWS]
      {
        "result_array" : [
            {
              "vm_ip" : "35.173.215.4",
              "vm_id" : "aws-us-east-1-shson-01",
              "result" : "WebServer is ready. Access http://35.173.215.4",
              "mcis_id" : "aws-us-east-1-shson"
            },
            {
              "vm_ip" : "18.206.13.233",
              "vm_id" : "aws-us-east-1-shson-02",
              "result" : "WebServer is ready. Access http://18.206.13.233",
              "mcis_id" : "aws-us-east-1-shson"
            },
            {
              "mcis_id" : "aws-us-east-1-shson",
              "result" : "WebServer is ready. Access http://18.232.53.134",
              "vm_id" : "aws-us-east-1-shson-03",
              "vm_ip" : "18.232.53.134"
            }
        ]
      }
      ```

<details>
<summary>테스트 스크립트 디렉토리 전체 Tree 보기</summary>

```
~/go/src/github.com/cloud-barista/cb-tumblebug/test/official$ tree
.
├── 0.settingSpider  # 클라우드 정보 등록 관련 스크립트 모음
│   ├── get-cloud.sh
│   ├── list-cloud.sh
│   ├── register-cloud.sh
│   └── unregister-cloud.sh
├── 0.settingTB  # 네임스페이스 관련 스크립트 모음
│   ├── create-ns.sh
│   ├── delete-ns.sh
│   ├── get-ns.sh
│   └── list-ns.sh
├── 1.vNet  # MCIR vNet 생성 관련 스크립트 모음
│   ├── create-vNet.sh
│   ├── delete-vNet.sh
│   ├── get-vNet.sh
│   ├── list-vNet.sh
│   └── spider-get-vNet.sh
├── 2.securityGroup  # MCIR securityGroup 생성 관련 스크립트 모음
│   ├── create-securityGroup.sh
│   ├── delete-securityGroup.sh
│   ├── get-securityGroup.sh
│   ├── list-securityGroup.sh
│   └── spider-get-securityGroup.sh
├── 3.sshKey  # MCIR sshKey 생성 관련 스크립트 모음
│   ├── create-sshKey.sh
│   ├── delete-sshKey.sh
│   ├── get-sshKey.sh
│   ├── list-sshKey.sh
│   ├── spider-delete-sshKey.sh
│   └── spider-get-sshKey.sh
├── 4.image  # MCIR image 등록 관련 스크립트 모음
│   ├── get-image.sh
│   ├── list-image.sh
│   ├── register-image.sh
│   └── unregister-image.sh
├── 5.spec  # MCIR spec 등록 관련 스크립트 모음
│   ├── fetch-specs.sh
│   ├── get-spec.sh
│   ├── list-spec.sh
│   ├── lookupSpecList.sh
│   ├── lookupSpec.sh
│   ├── register-spec.sh
│   ├── spider-get-speclist.sh
│   ├── spider-get-spec.sh
│   └── unregister-spec.sh
├── 6.mcis  # MCIS 생성 및 제어 관련 스크립트 모음
│   ├── create-mcis.sh
│   ├── get-mcis.sh
│   ├── just-terminate-mcis.sh
│   ├── list-mcis.sh
│   ├── reboot-mcis.sh
│   ├── resume-mcis.sh
│   ├── spider-create-vm.sh
│   ├── spider-delete-vm.sh
│   ├── spider-get-vm.sh
│   ├── spider-get-vmstatus.sh
│   ├── status-mcis.sh
│   ├── suspend-mcis.sh
│   └── terminate-and-delete-mcis.sh
├── conf.env  # CB-Spider 및 Tumblebug 서버 위치, 클라우드 리젼, 테스트용 이미지명, 테스트용 스팩명 등 테스트 기본 정보 제공
├── credentials.conf  # Cloud 정보 등록을 위한 CSP별 인증정보 (사용자에 맞게 수정 필요)
├── README.md
└── sequentialFullTest  # Cloud 정보 등록, NS 생성, MCIR 생성, MCIS 생성까지 한번에 자동 테스트
    ├── cleanAll-mcis-mcir-ns-cloud.sh  # 모든 오브젝트 역으로 제어
    ├── command-mcis.sh  # 생성된 MCIS(다중VM)에 원격 명령 수행
    ├── deploy-nginx-mcis.sh  # 생성된 MCIS(다중VM)에 Nginx 자동 배포
    ├── executionStatus  # 수행이 진행된 테스트 로그 (testAll 수행시 정보가 추가되며, cleanAll 수행시 정보가 제거됨)
    ├── testAll-mcis-mcir-ns-cloud.sh  # Cloud 정보 등록, NS 생성, MCIR 생성, MCIS 생성까지 한번에 자동 테스트
    ├── test-cloud.sh
    ├── test-mcir-ns-cloud.sh
    └── test-ns-cloud.sh
```

</details>
