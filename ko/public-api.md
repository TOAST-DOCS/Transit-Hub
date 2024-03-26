## Network > Transit Hub > API v2 가이드

API를 사용하려면 API 엔드포인트와 토큰 등이 필요합니다. [API 사용 준비](/Compute/Compute/ko/identity-api/)를 참고하여 API 사용에 필요한 정보를 준비합니다.

트랜짓 허브 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
|---|---|---|
| network | 한국(판교) 리전<br>한국(평촌) 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.

## 트랜짓 허브

### 트랜짓 허브 목록 보기

```
GET /v2.0/gateways/transithubs
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 트랜짓 허브 ID |
| name | Query | String | - | 조회할 트랜짓 허브 이름 |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithubs | Body | Array | 트랜짓 허브 정보 객체 목록 |
| transithubs.id | Body | UUID | 트랜짓 허브 ID |
| transithubs.tenant_id | Body | String | 테넌트 ID |
| transithubs.name | Body | String | 트랜짓 허브 이름 |
| transithubs.description | Body | String | 트랜짓 허브 설명 |
| transithubs.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| transithubs.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부 |
| transithubs.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |

<details><summary>예시</summary>

```json
{
  "transithubs": [
    {
      "status": "ACTIVE",
      "description": null,
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:19:05",
      "multicast_enable": true,
      "updated_at": "2024-02-12 22:19:05",
      "default_propagation_enable": true,
      "default_association_enable": true,
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "name": "thub"
    }
  ]
}
```
</details>

---
### 트랜짓 허브 보기

```
GET /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transitHubId | URL | UUID | O | 트랜짓 허브 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub | Body | Object | 트랜짓 허브 정보 객체 |
| transithub.id | Body | UUID | 트랜짓 허브 ID |
| transithub.tenant_id | Body | String | 테넌트 ID |
| transithub.name | Body | String | 트랜짓 허브 이름 |
| transithub.description | Body | String | 트랜짓 허브 설명 |
| transithub.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| transithub.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부 |
| transithub.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |

<details><summary>예시</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-02-12 22:19:05",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub"
  }
}
```
</details>

---
### 트랜짓 허브 생성하기

```
POST /v2.0/gateways/transithubs
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub | Body | Object | O | 트랜짓 허브 정보 객체 |
| transithub.name | Body | String | - | 트랜짓 허브 이름 |
| transithub.description | Body | String | - | 트랜짓 허브 설명 |
| transithub.multicast_enable | Body | Boolean | O | 멀티캐스트 기능 사용 여부 |
| transithub.default_association_enable | Body | Boolean | O | 기본 라우팅 테이블 연결 기능 사용 여부 |
| transithub.default_propagation_enable | Body | Boolean | O | 기본 라우팅 테이블 전파 기능 사용 여부 |




<details><summary>예시</summary>

```json
{
  "transithub": {
    "default_propagation_enable": true,
    "default_association_enable": true,
    "multicast_enable": true,
    "name": "thub",
    "description": "test"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub | Body | Object | 트랜짓 허브 정보 객체 |
| transithub.id | Body | UUID | 트랜짓 허브 ID |
| transithub.tenant_id | Body | String | 테넌트 ID |
| transithub.name | Body | String | 트랜짓 허브 이름 |
| transithub.description | Body | String | 트랜짓 허브 설명 |
| transithub.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| transithub.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부 |
| transithub.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |


<details><summary>예시</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-02-12 22:19:05",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub"
  }
}
```
</details>

---
### 트랜짓 허브 수정하기

```
PUT /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transitHubId | URL | UUID | O | 트랜짓 허브 ID |
| transithub | Body | Object | O | 트랜짓 허브 정보 객체 |
| transithub.name | Body | String | - | 트랜짓 허브 이름 |
| transithub.description | Body | String | - | 트랜짓 허브 설명 |

<details><summary>예시</summary>

```json
{
  "transithub": {
    "name": "thub1",
    "description": "test1"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub | Body | Object | 트랜짓 허브 정보 객체 |
| transithub.id | Body | UUID | 트랜짓 허브 ID |
| transithub.tenant_id | Body | String | 테넌트 ID |
| transithub.name | Body | String | 트랜짓 허브 이름 |
| transithub.description | Body | String | 트랜짓 허브 설명 |
| transithub.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| transithub.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부 |
| transithub.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |


<details><summary>예시</summary>

```json
{
  "transithub": {
    "status": "ACTIVE",
    "description": "test1",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "multicast_enable": true,
    "updated_at": "2024-03-04 01:59:00.961621",
    "default_propagation_enable": true,
    "default_association_enable": true,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub1"
  }
}
```
</details>

---
### 트랜짓 허브 삭제하기

```
DELETE /v2.0/gateways/transithubs/{transitHubId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transitHubId | URL | UUID | O | 트랜짓 허브 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.










## 연결

### 연결 목록 보기

```
GET /v2.0/gateways/transithub_attachments/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 연결 ID |
| name | Query | String | - | 조회할 연결 이름 |
| resource_id | Query | UUID | - | 조회할 리소스 ID(VPC) |
| subnet_id | Query | UUID | - | 조회할 서브넷 ID |
| transithub_id | Query | UUID | - | 조회할 트랜짓 허브 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_attachments | Body | Array | 연결 정보 객체 목록 |
| transithub_attachments.id | Body | UUID | 연결 ID |
| transithub_attachments.tenant_id | Body | String | 테넌트 ID |
| transithub_attachments.name | Body | String | 연결 이름 |
| transithub_attachments.description | Body | String | 연결 설명 |
| transithub_attachments.resource_id | Body | UUID | 리소스 ID(VPC) |
| transithub_attachments.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachments.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_attachments": [
    {
      "status": "ACTIVE",
      "remote": false,
      "name": "thub-attachment",
      "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:22:09",
      "updated_at": "2024-02-13 01:22:11",
      "resource_cidr": "172.16.0.0/12",
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
      "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": null
    }
  ]
}
```
</details>

---
### 연결 보기

```
GET /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| attachmentId | URL | UUID | O | 연결 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_attachment | Body | Object | 연결 정보 객체  |
| transithub_attachment.id | Body | UUID | 연결 ID |
| transithub_attachment.tenant_id | Body | String | 테넌트 ID |
| transithub_attachment.name | Body | String | 연결 이름 |
| transithub_attachment.description | Body | String | 연결 설명 |
| transithub_attachment.resource_id | Body | UUID | 리소스 ID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": null
  }
}
```
</details>

---
### 연결 생성하기

```
POST /v2.0/gateways/transithub_attachments/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_attachment | Body | Object | O | 로드 밸런서 정보 객체 |
| transithub_attachment.name | Body | String | - | 연결 이름 |
| transithub_attachment.description | Body | String | - | 연결 설명 |
| transithub_attachment.resource_id | Body | UUID | O | 리소스 ID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | O | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | O | 연결이 등록될 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_attachment": {
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-attachment",
    "description": null
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_attachment | Body | Object | 연결 정보 객체  |
| transithub_attachment.id | Body | UUID | 연결 ID |
| transithub_attachment.tenant_id | Body | String | 테넌트 ID |
| transithub_attachment.name | Body | String | 연결 이름 |
| transithub_attachment.description | Body | String | 연결 설명 |
| transithub_attachment.resource_id | Body | UUID | 리소스 ID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | 트랜짓 허브 ID |


<details><summary>예시</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": null
  }
}
```
</details>

---
### 연결 수정하기

```
PUT /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| attachmentId | URL | UUID | O | 연결 ID |
| transithub_attachment | Body | Object | O | 연결 정보 객체 |
| transithub_attachment.name | Body | String | - | 연결 이름 |
| transithub_attachment.description | Body | String | - | 연결 설명 |

<details><summary>예시</summary>

```json
{
  "transithub_attachment": {
    "name": "thub-attachment1",
    "description": "test1"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_attachment | Body | Object | 연결 정보 객체  |
| transithub_attachment.id | Body | UUID | 연결 ID |
| transithub_attachment.tenant_id | Body | String | 테넌트 ID |
| transithub_attachment.name | Body | String | 연결 이름 |
| transithub_attachment.description | Body | String | 연결 설명 |
| transithub_attachment.resource_id | Body | UUID | 리소스 ID(VPC) |
| transithub_attachment.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | 트랜짓 허브 ID |


<details><summary>예시</summary>

```json
{
  "transithub_attachment": {
    "status": "ACTIVE",
    "remote": false,
    "name": "thub-attachment1",
    "resource_id": "8eabc2c1-78a2-41e2-b03d-c1021042701f",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:09",
    "updated_at": "2024-02-13 01:22:11",
    "resource_cidr": "172.16.0.0/12",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "port_id": "eecaf943-fdcc-40da-bda2-45949026f668",
    "id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "test1"
  }
}
```
</details>

---
### 연결 삭제하기

```
DELETE /v2.0/gateways/transithub_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| attachmentId | URL | UUID | O | 연결 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.










## 라우팅 테이블

### 라우팅 테이블 목록 보기

```
GET /v2.0/gateways/transithub_routing_tables/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 라우팅 테이블 ID |
| name | Query | String | - | 조회할 라우팅 테이블 이름 |
| transithub_id | Query | UUID | - | 조회할 트랜짓 허브 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_tables | Body | Array | 라우팅 테이블 정보 객체 목록 |
| transithub_routing_tables.id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_tables.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_tables.name | Body | String | 라우팅 테이블 이름 |
| transithub_routing_tables.description | Body | String | 라우팅 테이블 설명 |
| transithub_routing_tables.transithub_id | Body | UUID | 트랜짓 허브 ID |
| transithub_routing_tables.default_table | Body | Boolean | 기본 라우팅 테이블 여부 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_tables": [
    {
      "status": "ACTIVE",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:19:05",
      "updated_at": "2024-02-12 22:19:08",
      "default_table": true,
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "f5b96823-260a-415f-a162-d1914341137e",
      "name": "default-9d01afbb-0e"
    }
  ]
}
```
</details>

---
### 라우팅 테이블 보기

```
GET /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingTableId | URL | UUID | O | 라우팅 테이블 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_table | Body | Object | 라우팅 테이블 정보 객체 |
| transithub_routing_table.id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_table.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_table.name | Body | String | 라우팅 테이블 이름 |
| transithub_routing_table.description | Body | String | 라우팅 테이블 설명 |
| transithub_routing_table.transithub_id | Body | UUID | 트랜짓 허브 ID |
| transithub_routing_table.default_table | Body | Boolean | 기본 라우팅 테이블 여부 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_table": {
    "status": "ACTIVE",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:19:05",
    "updated_at": "2024-02-12 22:19:08",
    "default_table": true,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "f5b96823-260a-415f-a162-d1914341137e",
    "name": "default-9d01afbb-0e"
  }
}
```
</details>

---
### 라우팅 테이블 생성하기

```
POST /v2.0/gateways/transithub_routing_tables/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_routing_table | Body | Object | O | 라우팅 테이블 정보 객체 |
| transithub_routing_table.name | Body | String | - | 라우팅 테이블 이름 |
| transithub_routing_table.description | Body | String | - | 라우팅 테이블 설명 |
| transithub_routing_table.transithub_id | Body | UUID | O | 라우팅 테이블이 등록될 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_table": {
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-routing-table",
    "description": null
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_table | Body | Object | 라우팅 테이블 정보 객체 |
| transithub_routing_table.id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_table.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_table.name | Body | String | 라우팅 테이블 이름 |
| transithub_routing_table.description | Body | String | 라우팅 테이블 설명 |
| transithub_routing_table.transithub_id | Body | UUID | 트랜짓 허브 ID |
| transithub_routing_table.default_table | Body | Boolean | 기본 라우팅 테이블 여부 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_table": {
    "status": "BUILD",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-05 22:38:41",
    "updated_at": "2024-03-05 22:38:41",
    "default_table": false,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "051eabf3-30f1-4e7a-a9bc-973c64f3c24a",
    "name": "thub-routing-table"
  }
}
```
</details>

---
### 라우팅 테이블 수정하기

```
PUT /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingTableId | URL | UUID | O | 라우팅 테이블 ID |
| transithub_routing_table | Body | Object | O | 라우팅 테이블 정보 객체 |
| transithub_routing_table.name | Body | String | - | 라우팅 테이블 이름 |
| transithub_routing_table.description | Body | String | - | 라우팅 테이블 설명 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_table": {
    "name": "thub-routing-table1",
    "description": "test"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_table | Body | Object | 라우팅 테이블 정보 객체 |
| transithub_routing_table.id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_table.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_table.name | Body | String | 라우팅 테이블 이름 |
| transithub_routing_table.description | Body | String | 라우팅 테이블 설명 |
| transithub_routing_table.transithub_id | Body | UUID | 트랜짓 허브 ID |
| transithub_routing_table.default_table | Body | Boolean | 기본 라우팅 테이블 여부 |


<details><summary>예시</summary>

```json
{
  "transithub_routing_table": {
    "status": "ACTIVE",
    "description": "test",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-05 22:38:41",
    "updated_at": "2024-03-05 22:40:44.303417",
    "default_table": false,
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "051eabf3-30f1-4e7a-a9bc-973c64f3c24a",
    "name": "thub-routing-table1"
  }
}
```
</details>

---
### 라우팅 테이블 삭제하기

```
DELETE /v2.0/gateways/transithub_routing_tables/{routingTableId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingTableId | URL | UUID | O | 라우팅 테이블 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.











## 라우팅 연결

### 라우팅 연결 목록 보기

```
GET /v2.0/gateways/transithub_routing_associations/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 라우팅 연결 ID |
| attachment_id | Query | UUID | - | 조회할 연결 ID |
| routing_table_id | Query | UUID | - | 조회할 라우팅 테이블 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_associations | Body | Array | 라우팅 연결 정보 객체 목록 |
| transithub_routing_associations.id | Body | UUID | 라우팅 연결 ID |
| transithub_routing_associations.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_associations.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_associations.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_associations.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_associations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "created_at": "2024-02-13 01:22:09",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "56f5c3d2-2a9f-4ada-a358-356c6387de76",
      "updated_at": "2024-02-13 01:22:09"
    }
  ]
}
```
</details>

---
### 라우팅 연결 보기

```
GET /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingAssociationId | URL | UUID | O | 라우팅 연결 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_association | Body | Object | 라우팅 연결 정보 객체 |
| transithub_routing_association.id | Body | UUID | 라우팅 연결 ID |
| transithub_routing_association.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_association.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-02-13 01:22:09",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "56f5c3d2-2a9f-4ada-a358-356c6387de76",
    "updated_at": "2024-02-13 01:22:09"
  }
}
```
</details>

---
### 라우팅 연결 생성하기

```
POST /v2.0/gateways/transithub_routing_associations/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_routing_association | Body | Object | O | 라우팅 연결 정보 객체 |
| transithub_routing_association.description | Body | String | - | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | O | 라우팅 연결이 등록될 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_association": {
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_association | Body | Object | 라우팅 연결 정보 객체 |
| transithub_routing_association.id | Body | UUID | 라우팅 연결 ID |
| transithub_routing_association.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_association.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-03-05 22:51:48",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "a5532ee9-1d7b-44bd-a622-85198171ee98",
    "updated_at": "2024-03-05 22:51:48"
  }
}
```
</details>

---
### 라우팅 연결 삭제하기

```
DELETE /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingAssociationId | URL | UUID | O | 라우팅 연결 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.











## 라우팅 전파

### 라우팅 전파 목록 보기

```
GET /v2.0/gateways/transithub_routing_propagations/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 라우팅 전파 ID |
| attachment_id | Query | UUID | - | 조회할 연결 ID |
| routing_table_id | Query | UUID | - | 조회할 라우팅 테이블 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_propagations | Body | Array | 라우팅 전파 정보 객체 목록 |
| transithub_routing_propagations.id | Body | UUID | 라우팅 전파 ID |
| transithub_routing_propagations.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_propagations.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagations.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagations.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_propagations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "created_at": "2024-02-13 01:22:09",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "6bf0efaa-6d32-4fef-a341-7662e9bf1eb1",
      "updated_at": "2024-02-13 01:22:09"
    }
  ]
}
```
</details>

---
### 라우팅 전파 보기

```
GET /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingPropagationId | URL | UUID | O | 라우팅 전파 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_propagation | Body | Object | 라우팅 전파 정보 객체 |
| transithub_routing_propagation.id | Body | UUID | 라우팅 전파 ID |
| transithub_routing_propagation.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_propagation.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_propagation": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-02-13 01:22:09",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "6bf0efaa-6d32-4fef-a341-7662e9bf1eb1",
    "updated_at": "2024-02-13 01:22:09"
  }
}
```
</details>

---
### 라우팅 전파 생성하기

```
POST /v2.0/gateways/transithub_routing_propagations/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_routing_propagation | Body | Object | O | 라우팅 전파 정보 객체 |
| transithub_routing_propagation.description | Body | String | - | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | O | 라우팅 전파가 등록될 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_propagation": {
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_propagation | Body | Object | 라우팅 전파 정보 객체 |
| transithub_routing_propagation.id | Body | UUID | 라우팅 전파 ID |
| transithub_routing_propagation.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_propagation.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_propagation": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "created_at": "2024-03-05 22:56:58",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "d1b54e63-0032-44dc-bb31-22d5723782ee",
    "updated_at": "2024-03-05 22:56:58.825231"
  }
}
```
</details>

---
### 라우팅 전파 삭제하기

```
DELETE /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingPropagationId | URL | UUID | O | 라우팅 전파 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.











## 라우팅 룰

### 라우팅 룰 목록 보기

```
GET /v2.0/gateways/transithub_routing_rules/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 라우팅 룰 ID |
| action | Query | Enum | - | 조회할 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| rule_type | Query | Enum | - | 조회할 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| attachment_id | Query | UUID | - | 조회할 연결(Attachment) ID |
| routing_table_id | Query | UUID | - | 조회할 라우팅 테이블 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_rules | Body | Array | 라우팅 룰 정보 객체 목록 |
| transithub_routing_rules.id | Body | UUID | 라우팅 룰 ID |
| transithub_routing_rules.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_rules.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rules.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rules.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rules.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rules.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rules.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rules.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_rules": [
    {
      "status": "ACTIVE",
      "rule_type": "PROPAGATED",
      "attachment_id": "ea9bb603-893c-4955-a7bb-64b6438a6f5b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-12 22:35:48",
      "updated_at": "2024-02-12 22:35:48",
      "action": "FORWARD",
      "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
      "cidr": "172.16.0.0/12",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "propagation_id": "7a5d3159-a3a6-495b-bb0f-522c4d8a9933",
      "id": "3d10d565-8813-4c3c-9f1c-1af96eee9f14"
    }
  ]
}
```
</details>

---
### 라우팅 룰 보기

```
GET /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingRuleId | URL | UUID | O | 라우팅 룰 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_rule | Body | Object | 라우팅 룰 정보 객체 |
| transithub_routing_rule.id | Body | UUID | 라우팅 룰 ID |
| transithub_routing_rule.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_rule.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rule.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rule.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rule.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rule.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rule.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_rule": {
    "status": "ACTIVE",
    "rule_type": "PROPAGATED",
    "attachment_id": "ea9bb603-893c-4955-a7bb-64b6438a6f5b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-12 22:35:48",
    "updated_at": "2024-02-12 22:35:48",
    "action": "FORWARD",
    "routing_table_id": "f5b96823-260a-415f-a162-d1914341137e",
    "cidr": "172.16.0.0/12",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "propagation_id": "7a5d3159-a3a6-495b-bb0f-522c4d8a9933",
    "id": "3d10d565-8813-4c3c-9f1c-1af96eee9f14"
  }
}
```
</details>

---
### 라우팅 룰 생성하기

```
POST /v2.0/gateways/transithub_routing_rules/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_routing_rule | Body | Object | O | 라우팅 룰 정보 객체 |
| transithub_routing_rule.name | Body | String | - | 라우팅 룰 이름 |
| transithub_routing_rule.description | Body | String | - | 라우팅 룰 설명 |
| transithub_routing_rule.cidr | Body | String | O | 라우팅 룰 IP 대역 |
| transithub_routing_rule.action | Body | Enum | - | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나<br>입력하지 않을 경우 `FORWARD` |
| transithub_routing_rule.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | O | 라우팅 룰이 등록될 라우팅 테이블 ID |

<details><summary>예시</summary>

```json
{
  "transithub_routing_rule": {
    "routing_table_id": "e5cb6442-4b5d-4298-84e2-adc9289c650e",
    "cidr": "1.1.1.0/24",
    "attachment_id": "6489cee8-0b5f-4053-b72d-1aa8b2921962"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_rule | Body | Object | 라우팅 룰 정보 객체 |
| transithub_routing_rule.id | Body | UUID | 라우팅 룰 ID |
| transithub_routing_rule.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_rule.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rule.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rule.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rule.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rule.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rule.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |

<details><summary>예시</summary>

```json
{
  "transithub_routing_rule": {
    "status": "ACTIVE",
    "rule_type": "STATIC",
    "attachment_id": "6489cee8-0b5f-4053-b72d-1aa8b2921962",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:00:05",
    "updated_at": "2024-03-06 23:00:05",
    "action": "FORWARD",
    "routing_table_id": "e5cb6442-4b5d-4298-84e2-adc9289c650e",
    "cidr": "1.1.1.0/24",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "propagation_id": null,
    "id": "3f765a36-bd6a-450a-9e05-366ecb8446c3"
  }
}
```
</details>

---
### 라우팅 룰 삭제하기

```
DELETE /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingRuleId | URL | UUID | O | 라우팅 룰 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.












## 멀티캐스트 도메인

### 멀티캐스트 도메인 목록 보기

```
GET /v2.0/gateways/transithub_multicast_domains/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 멀티캐스트 도메인 ID |
| name | Query | String | - | 조회할 멀티캐스트 도메인 이름 |
| transithub_id | Query | UUID | - | 조회할 트랜짓 허브 ID |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_domains | Body | Array | 멀티캐스트 도메인 정보 객체 목록 |
| transithub_multicast_domains.id | Body | UUID | 멀티캐스트 도메인 ID |
| transithub_multicast_domains.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_domains.name | Body | String | 멀티캐스트 도메인 이름 |
| transithub_multicast_domains.description | Body | String | 멀티캐스트 도메인 설명 |
| transithub_multicast_domains.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>
  
```json
{
  "transithub_multicast_domains": [
    {
      "status": "ACTIVE",
      "description": null,
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:20:31",
      "updated_at": "2024-02-13 01:20:32",
      "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
      "name": "thub-domain"
    }
  ]
}
```
</details>

---
### 멀티캐스트 도메인 보기

```
GET /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastDomainId | URL | UUID | O | 멀티캐스트 도메인 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| tokenId | Header | String | 토큰 ID |
| transithub_multicast_domain | Body | Object | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.name | Body | String | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | 멀티캐스트 도메인 설명 |
| transithub_multicast_domain.transithub_id | Body | UUID | 멀티캐스트 도메인을 등록할 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "ACTIVE",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:20:31",
    "updated_at": "2024-02-13 01:20:32",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "d55022de-947f-4db3-a7b0-5a4cee9a2369",
    "name": "thub-domain"
  }
}
```
</details>



---
### 멀티캐스트 도메인 생성하기

```
POST /v2.0/gateways/transithub_multicast_domains/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_multicast_domain | Body | Object | O | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.name | Body | String | - | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | - | 멀티캐스트 도메인 설명 |
| transithub_multicast_domain.transithub_id | Body | UUID | O | 멀티캐스트 도메인을 등록할 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_domain": {
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "name": "thub-domain1"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_domain | Body | Object | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.id | Body | UUID | 멀티캐스트 도메인 ID |
| transithub_multicast_domain.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_domain.name | Body | String | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | 멀티캐스트 도메인 설명 |
| transithub_multicast_domain.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "BUILD",
    "description": null,
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:03:07",
    "updated_at": "2024-03-06 23:03:07",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "fba53b77-431b-466f-8a31-784942649e73",
    "name": "thub-domain1"
  }
}
```
</details>


---
### 멀티캐스트 도메인 수정하기

```
PUT /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastDomainId | URL | UUID | O | 멀티캐스트 도메인 ID |
| transithub_multicast_domain | Body | Object | O | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.name | Body | String | - | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | - | 멀티캐스트 도메인 설명 |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_domain": {
    "name": "thub-domain",
    "description": "test"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_domain | Body | Object | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.id | Body | UUID | 멀티캐스트 도메인 ID |
| transithub_multicast_domain.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_domain.name | Body | String | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | 멀티캐스트 도메인 설명 |
| transithub_multicast_domain.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_domain": {
    "status": "ACTIVE",
    "description": "test",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-06 23:03:07",
    "updated_at": "2024-03-06 23:06:18.031473",
    "transithub_id": "9d01afbb-0e95-423e-9360-15a3f2e9a233",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "fba53b77-431b-466f-8a31-784942649e73",
    "name": "thub-domain"
  }
}
```
</details>


---
### 멀티캐스트 도메인 삭제하기

```
DELETE /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastDomainId | URL | UUID | O | 멀티캐스트 도메인 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.









## 멀티캐스트 연결

### 멀티캐스트 연결 목록 보기

```
GET /v2.0/gateways/transithub_multicast_associations/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 멀티캐스트 연결 ID |
| name | Query | String | - | 조회할 멀티캐스트 연결 이름 |
| domain_id | Query | UUID | - | 조회할 멀티캐스트 도메인 ID |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_associations | Body | Array | 멀티캐스트 연결 정보 객체 목록 |
| transithub_multicast_associations.id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_associations.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_associations.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_associations.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_associations.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_associations.domain_id | Body | UUID | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>
  
```json
{
  "transithub_multicast_associations": [
    {
      "status": "ACTIVE",
      "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
      "description": "",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-02-13 01:22:37",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "3da29ae0-f544-4b8e-88c4-eb2ef78d0214",
      "updated_at": "2024-02-13 01:22:37",
      "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
    }
  ]
}
```
</details>


---
### 멀티캐스트 연결 보기

```
GET /v2.0/gateways/transithub_multicast_domains/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastAssociationId | URL | UUID | O | 라우팅 룰 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| tokenId | Header | String | 토큰 ID |
| transithub_multicast_association | Body | Object | 멀티캐스트 연결 정보 객체 |
| transithub_multicast_association.id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_association.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_association.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_association.domain_id | Body | UUID | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-02-13 01:22:37",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3da29ae0-f544-4b8e-88c4-eb2ef78d0214",
    "updated_at": "2024-02-13 01:22:37",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>


---
### 멀티캐스트 연결 생성하기

```
POST /v2.0/gateways/transithub_multicast_associations/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_multicast_association | Body | Object | O | 멀티캐스트 연결 정보 객체 |
| transithub_multicast_association.description | Body | String | - | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_multicast_association.domain_id | Body | UUID | O | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_association": {
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_association | Body | Object | 멀티캐스트 연결 정보 객체 |
| transithub_multicast_association.id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_association.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_association.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_association.domain_id | Body | UUID | 멀티캐스트 도메인 ID |


<details><summary>예시</summary>

```json
{
  "transithub_multicast_association": {
    "status": "ACTIVE",
    "attachment_id": "23fc5818-c667-4e90-b50b-70b9e8727f49",
    "description": "",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:22:59",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "4da8461b-6c92-4225-8368-60e1e49e3d92",
    "updated_at": "2024-03-07 00:22:59",
    "domain_id": "d55022de-947f-4db3-a7b0-5a4cee9a2369"
  }
}
```
</details>

---
### 멀티캐스트 연결 삭제하기

```
DELETE /v2.0/gateways/transithub_multicast_associations/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastAssociationId | URL | UUID | O | 멀티캐스트 연결 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.
















## 멀티캐스트 그룹

### 멀티캐스트 그룹 목록 보기

```
GET /v2.0/gateways/transithub_multicast_groups/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 멀티캐스트 그룹 ID |
| name | Query | String | - | 조회할 멀티캐스트 그룹 이름 |
| domain_id | Query | UUID | - | 조회할 멀티캐스트 그룹 ID |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_groups | Body | Array | 멀티캐스트 그룹 정보 객체 목록 |
| transithub_multicast_groups.id | Body | UUID | 멀티캐스트 그룹 ID |
| transithub_multicast_groups.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_groups.description | Body | String | 멀티캐스트 그룹 설명 |
| transithub_multicast_groups.association_id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_groups.ipaddress | Body | String | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_groups.member_type | Body | String | 멀티캐스트 멤버 타입 |
| transithub_multicast_groups.source_type | Body | String | 멀티캐스트 소스 타입 |
| transithub_multicast_groups.port_id | Body | UUID | 멀티캐스트 대상 포트 ID |

<details><summary>예시</summary>
  
```json
{
  "transithub_multicast_groups": [
    {
      "description": "",
      "updated_at": "2024-03-07 00:28:20",
      "member_type": "STATIC",
      "source_type": null,
      "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
      "ipaddress": "224.0.0.3",
      "id": "ce8c5fef-6859-4e68-8b46-4cd395c44b37",
      "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "created_at": "2024-03-07 00:28:20",
      "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
      "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b"
    }
  ]
}
```
</details>

---
### 멀티캐스트 그룹 보기

```
GET /v2.0/gateways/transithub_multicast_groups/{multicastGroupId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastGroupId | URL | UUID | O | 멀티캐스트 그룹 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_group | Body | Object | 멀티캐스트 그룹 정보 객체 |
| transithub_multicast_group.id | Body | UUID | 멀티캐스트 그룹 ID |
| transithub_multicast_group.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_group.description | Body | String | 멀티캐스트 그룹 설명 |
| transithub_multicast_group.association_id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_group.ipaddress | Body | String | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_group.member_type | Body | String | 멀티캐스트 멤버 타입 |
| transithub_multicast_group.source_type | Body | String | 멀티캐스트 소스 타입 |
| transithub_multicast_group.port_id | Body | UUID | 멀티캐스트 대상 포트 ID |

<details><summary>예시</summary>

```json
{
  "transithub_multicast_group": {
    "description": "",
    "updated_at": "2024-03-07 00:28:20",
    "member_type": "STATIC",
    "source_type": null,
    "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
    "ipaddress": "224.0.0.3",
    "id": "ce8c5fef-6859-4e68-8b46-4cd395c44b37",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:28:20",
    "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b"
  }
}
```
</details>

---
### 멀티캐스트 그룹 생성하기

```
POST /v2.0/gateways/transithub_multicast_groups/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_multicast_group | Body | Object | O | 멀티캐스트 그룹 정보 객체 |
| transithub_multicast_group.description | Body | String | - | 멀티캐스트 그룹 설명 |
| transithub_multicast_group.association_id | Body | UUID | O | 멀티캐스트 연결 ID |
| transithub_multicast_group.ipaddress | Body | String | O | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_group.member_type | Body | String | - | 멀티캐스트 멤버 타입, 멤버로 사용할 경우 `STATIC` 입력<br>멤버 타입과 소스 타입 중 하나 입력 필수 |
| transithub_multicast_group.source_type | Body | String | - | 멀티캐스트 소스 타입, 소스로 사용할 경우 `STATIC` 입력<br>멤버 타입과 소스 타입 중 하나 입력 필수 |
| transithub_multicast_group.port_id | Body | UUID | O | 멀티캐스트 대상 포트 ID |


<details><summary>예시</summary>

```json
{
  "transithub_multicast_group": {
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "port_id": "b0ca1c15-13e1-4746-b8e1-9ec8e685d228",
    "ipaddress": "224.0.0.10",
    "member_type": "STATIC"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_group | Body | Object | 멀티캐스트 그룹 정보 객체 |
| transithub_multicast_group.id | Body | UUID | 멀티캐스트 그룹 ID |
| transithub_multicast_group.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_group.description | Body | String | 멀티캐스트 그룹 설명 |
| transithub_multicast_group.association_id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_group.ipaddress | Body | String | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_group.member_type | Body | String | 멀티캐스트 멤버 타입 |
| transithub_multicast_group.source_type | Body | String | 멀티캐스트 소스 타입 |
| transithub_multicast_group.port_id | Body | UUID | 멀티캐스트 대상 포트 ID |


<details><summary>예시</summary>

```json
{
  "transithub_multicast_group": {
    "description": "",
    "association_id": "b4ba8acd-34d2-48f9-b2f6-cbfe5e92d0f8",
    "subnet_id": "4263b32d-4bc5-45cc-bb3e-fded960e8f46",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "created_at": "2024-03-07 00:40:19",
    "updated_at": "2024-03-07 00:40:19",
    "member_type": "STATIC",
    "domain_id": "27d79c71-ccce-4928-af3c-5ffa5c3ed3fd",
    "source_type": null,
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "ipaddress": "224.0.0.10",
    "id": "91b281f8-41ab-4d27-8639-da27b23d21db"
  }
}
```
</details>


---
### 멀티캐스트 그룹 삭제하기

```
DELETE /v2.0/gateways/transithub_multicast_groups/{multicastGroupId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastGroupId | URL | UUID | O | 멀티캐스트 그룹 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.







## 트랜짓 허브 공유

### 공유 허용 목록 보기

```
GET /v2.0/gateways/transithub_allow_projects/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 공유 허용 정보 ID |
| transithub_id | Query | UUID | - | 조회할 트랜짓 허브 ID |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_allow_projects | Body | Array | 공유 허용 정보 목록 |
| transithub_allow_projects.id | Body | UUID | 트랜짓 허브 허용 정보 ID |
| transithub_allow_projects.tenant_id | Body | String | 테넌트 ID |
| transithub_allow_projects.transithub_id | Body | UUID | 공유할 트랜짓 허브 ID |
| transithub_allow_projects.transithub_name | Body | String | 트랜짓 허브 이름 |
| transithub_allow_projects.target_project_id | Body | UUID | 공유 대상 프로젝트 ID |

<details><summary>예시</summary>
  
```json
{
  "transithub_allow_projects": [
    {
      "target_project_id": "cd29a534a15e46049b968dd0835b129b",
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "transithub_name": "thub1",
      "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "186717d3-8e26-40ec-ad00-67a8463ccc4c"
    }
  ]
}
```
</details>

---
### 공유 허용 정보 생성하기

```
POST /v2.0/gateways/transithub_allow_projects/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_allow_project | Body | Object | O | 공유 허용 정보 객체 |
| transithub_allow_projects.transithub_id | Body | UUID | O | 공유할 트랜짓 허브 ID |
| transithub_allow_projects.target_project_id | Body | UUID | O | 공유 대상 프로젝트 ID |


<details><summary>예시</summary>

```json
{
  "transithub_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c"
  }
}
```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_allow_project | Body | Object | 공유 허용 정보 객체 |
| transithub_allow_project.id | Body | UUID | 공유 허용 정보 ID |
| transithub_allow_project.tenant_id | Body | String | 테넌트 ID |
| transithub_allow_project.transithub_id | Body | UUID | 공유할 트랜짓 허브 ID |
| transithub_allow_project.transithub_name | Body | String | 트랜짓 허브 이름 |
| transithub_allow_project.target_project_id | Body | UUID | 공유 대상 프로젝트 ID |


<details><summary>예시</summary>

```json
{
  "transithub_allow_project": {
    "target_project_id": "cd29a534a15e46049b968dd0835b129b",
    "description": "",
    "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "transithub_name": "dj-thub1",
    "transithub_id": "efb688ea-15c2-4d36-b123-6044e3c37d8c",
    "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
    "id": "3d962640-385f-4874-8766-aa1b4480e7e4"
  }
}
```
</details>


---
### 공유 허용 정보 삭제하기

```
DELETE /v2.0/gateways/transithub_allow_projects/{allowProjectId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| allowProjectId | URL | UUID | O | 공유 허용 정보 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.



### 공유 받은 목록 보기

```
GET /v2.0/gateways/transithub_shared_lists/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithub_id | Query | UUID | - | 조회할 트랜짓 허브 ID |


#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_shared_lists | Body | Array | 공유 받은 정보 목록 |
| transithub_shared_lists.id | Body | UUID | 공유 받은 정보 ID |
| transithub_shared_lists.tenant_id | Body | String | 테넌트 ID |
| transithub_shared_lists.transithub_id | Body | UUID | 공유 받은 트랜짓 허브 ID |
| transithub_shared_lists.transithub_name | Body | String | 공유 받은 트랜짓 허브 이름 |
| transithub_shared_lists.transithub_project_id | Body | UUID | 공유 받은 트랜짓 허브의 프로젝트 ID |

<details><summary>예시</summary>
  
```json
{
  "transithub_shared_lists": [
    {
      "description": "",
      "tenant_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "transithub_project_id": "1fb0cf13afb341b699f74bbbecab2117",
      "transithub_name": "thub",
      "transithub_id": "4050efd6-b6cc-4e2d-9402-dd5e1520872f",
      "project_id": "5fdb378e72ca4aff9db04f40f7955f0b",
      "id": "51c8fd9c-ae82-474f-9664-9fc31c77a563"
    }
  ]
}
```
</details>
