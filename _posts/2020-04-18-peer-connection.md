---
layout: post
section-type: post
title: "VPN Peer connection"
category: AWS
tags: [ 'AWS' ]
comments: true
---
제 블로그의 모든 글은 IMHO로 쓴 것입니다.
서로에 대한 존중을 담은 덧글을 남겨 소통을 하신다면 더 좋은 글로 발전이 될 수 있을 것 같습니다.
존중이 담기지 않은 덧글은 언제든 삭제될 수 있습니다.
감사합니다:)
---

피어링된 VPC 액세스

이 시나리오의 구성에는 단일 VPC 그리고 대상 VPC와 피어링된 추가 VPC가 포함됩니다. 클라이언트에게 대상 VPC 그리고 이와 피어링된 다른 VPC 내부의 리소스에 대한 액세스 권한을 부여해야 하는 경우 이 구성을 사용하는 것이 좋습니다.

이 구성을 구현하는 방법

1. VPC에 하나 이상의 서브넷이 있는지 확인합니다. VPC에서 클라이언트 VPN 엔드포인트에 연결할 서브넷을 식별하여 해당 IPv4 CIDR 범위를 메모합니다. 자세한 내용은 Amazon VPC 사용 설명서의 VPC 및 서브넷을 참조하십시오.
2. VPC의 기본 보안 그룹이 클라이언트와의 인바운드 및 아웃바운드 트래픽을 허용하는지 확인합니다. 자세한 정보는 Amazon VPC 사용 설명서의 VPC의 보안 그룹 단원을 참조하십시오.
3. VPC 사이에 VPC 피어링 연결을 설정합니다. Amazon VPC 사용 설명서의 VPC 피어링 연결 생성 및 수락에 설명되어 있는 단계를 따릅니다.
4. VPC 피어링 연결을 테스트합니다. 동일한 네트워크에 속하는 것처럼 VPC의 인스턴스가 서로 통신할 수 있는지 확인합니다. 피어링 연결이 예상대로 작동하면 다음 단계로 이동합니다.
5. 1단계에서 식별한 VPC와 동일한 리전에서 클라이언트 VPN 엔드포인트를 생성합니다. 클라이언트 VPN 엔드포인트 생성에 설명되어 있는 단계를 수행합니다.
6. 앞서 식별한 서브넷을 생성한 클라이언트 VPN 엔드포인트에 연결합니다. 이렇게 하려면 클라이언트 VPN 엔드포인트에 대상 네트워크 연결에 설명되어 있는 단계를 수행하고 서브넷 및 VPC를 선택합니다.
7. 권한 부여 규칙을 추가하여 클라이언트에 VPC에 대한 액세스 권한을 부여합니다. 이렇게 하려면 클라이언트 VPN 엔드포인트에 권한 부여 규칙 추가에 설명되어 있는 단계를 수행하고 Destination network to enable(활성화할 대상 네트워크)에 VPC의 IPv4 CIDR 범위를 입력합니다.
8. 라우팅을 추가하여 트래픽을 피어링된 VPC로 전달합니다. 이렇게 하려면 엔드포인트 라우팅 생성에 설명되어 있는 단계를 수행합니다. Route destination(라우팅 대상 주소)에 피어링된 VPC의 IPv4 CIDR 범위를 입력하고 Target VPC Subnet ID(대상 VPC 서브넷 ID)에서 클라이언트 VPN 엔드포인트에 연결한 서브넷을 선택합니다.
9. 권한 부여 규칙을 추가하여 클라이언트에 피어링된 VPC에 대한 액세스 권한을 부여합니다. 이렇게 하려면 클라이언트 VPN 엔드포인트에 권한 부여 규칙 추가에 설명되어 있는 단계를 수행합니다. Destination network(대상 네트워크)에 피어링된 VPC의 IPv4 CIDR 범위를 입력하고 Grant access to(액세스 권한 부여)에서 Allow access to all users(모든 사용자에게 액세스 허용)를 선택합니다.

---
https://docs.aws.amazon.com/ko_kr/vpn/latest/clientvpn-admin/scenario-peered.html
