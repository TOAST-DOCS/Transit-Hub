## Network > Transit Hub > API v2 가이드

API를 사용하려면 API 엔드포인트와 토큰 등이 필요합니다. [API 사용 준비](/Compute/Compute/ko/identity-api/)를 참고하여 API 사용에 필요한 정보를 준비합니다.

트랜짓 허브 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
|---|---|---|
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>일본 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://jp1-api-network-infrastructure.nhncloudservice.com |

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
| resource_id | Query | UUID | - | 조회할 리소스 ID (VPC) |
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
| transithub_attachments.resource_id | Body | UUID | 리소스 ID (VPC) |
| transithub_attachments.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachments.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

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
| transithub_attachment.resource_id | Body | UUID | 리소스 ID (VPC) |
| transithub_attachment.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

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
| transithub_attachment.resource_id | Body | UUID | O | 리소스 ID (VPC) |
| transithub_attachment.subnet_id | Body | UUID | O | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | O | 연결이 등록될 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

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
| transithub_attachment.resource_id | Body | UUID | 리소스 ID (VPC) |
| transithub_attachment.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | 트랜짓 허브 ID |


<details><summary>예시</summary>

```json

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
| transithub_attachment.resource_id | Body | UUID | 리소스 ID (VPC) |
| transithub_attachment.subnet_id | Body | UUID | 서브넷 ID |
| transithub_attachment.transithub_id | Body | UUID | 트랜짓 허브 ID |


<details><summary>예시</summary>

```json

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
| name | Query | String | - | 조회할 라우팅 연결 이름 |
| attachment_id | Query | UUID | - | 조회할 연결 ID |
| routing_table_id | Query | UUID | - | 조회할 라우팅 테이블 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_associations | Body | Array | 라우팅 연결 정보 객체 목록 |
| transithub_routing_associations.id | Body | UUID | 라우팅 연결 ID |
| transithub_routing_associations.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_associations.name | Body | String | 라우팅 연결 이름 |
| transithub_routing_associations.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_associations.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_associations.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

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
| transithub_routing_association.name | Body | String | 라우팅 연결 이름 |
| transithub_routing_association.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

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
| transithub_routing_association.name | Body | String | - | 라우팅 연결 이름 |
| transithub_routing_association.description | Body | String | - | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | O | 라우팅 연결이 등록될 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_association | Body | Object | 라우팅 연결 정보 객체 |
| transithub_routing_association.id | Body | UUID | 라우팅 연결 ID |
| transithub_routing_association.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_association.name | Body | String | 라우팅 연결 이름 |
| transithub_routing_association.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

```
</details>

---
### 라우팅 연결 수정하기

```
PUT /v2.0/gateways/transithub_routing_associations/{routingAssociationId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingAssociationId | URL | UUID | O | 라우팅 연결 ID |
| transithub_routing_association | Body | Object | O | 라우팅 연결 정보 객체 |
| transithub_routing_association.name | Body | String | - | 라우팅 연결 이름 |
| transithub_routing_association.description | Body | String | - | 라우팅 연결 설명 |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_association | Body | Object | 라우팅 연결 정보 객체 |
| transithub_routing_association.id | Body | UUID | 라우팅 연결 ID |
| transithub_routing_association.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_association.name | Body | String | 라우팅 연결 이름 |
| transithub_routing_association.description | Body | String | 라우팅 연결 설명 |
| transithub_routing_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_association.routing_table_id | Body | UUID | 라우팅 테이블 ID |


<details><summary>예시</summary>

```json

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
| name | Query | String | - | 조회할 라우팅 전파 이름 |
| attachment_id | Query | UUID | - | 조회할 연결 ID |
| routing_table_id | Query | UUID | - | 조회할 라우팅 테이블 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_propagations | Body | Array | 라우팅 전파 정보 객체 목록 |
| transithub_routing_propagations.id | Body | UUID | 라우팅 전파 ID |
| transithub_routing_propagations.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_propagations.name | Body | String | 라우팅 전파 이름 |
| transithub_routing_propagations.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagations.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagations.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

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
| transithub_routing_propagation.name | Body | String | 라우팅 전파 이름 |
| transithub_routing_propagation.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

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
| transithub_routing_propagation.name | Body | String | - | 라우팅 전파 이름 |
| transithub_routing_propagation.description | Body | String | - | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | O | 라우팅 전파가 등록될 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_propagation | Body | Object | 라우팅 전파 정보 객체 |
| transithub_routing_propagation.id | Body | UUID | 라우팅 전파 ID |
| transithub_routing_propagation.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_propagation.name | Body | String | 라우팅 전파 이름 |
| transithub_routing_propagation.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

```
</details>

---
### 라우팅 전파 수정하기

```
PUT /v2.0/gateways/transithub_routing_propagations/{routingPropagationId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingPropagationId | URL | UUID | O | 라우팅 전파 ID |
| transithub_routing_propagation | Body | Object | O | 라우팅 전파 정보 객체 |
| transithub_routing_propagation.name | Body | String | - | 라우팅 전파 이름 |
| transithub_routing_propagation.description | Body | String | - | 라우팅 전파 설명 |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_propagation | Body | Object | 라우팅 전파 정보 객체 |
| transithub_routing_propagation.id | Body | UUID | 라우팅 전파 ID |
| transithub_routing_propagation.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_propagation.name | Body | String | 라우팅 전파 이름 |
| transithub_routing_propagation.description | Body | String | 라우팅 전파 설명 |
| transithub_routing_propagation.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_propagation.routing_table_id | Body | UUID | 라우팅 테이블 ID |


<details><summary>예시</summary>

```json

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
| name | Query | String | - | 조회할 라우팅 룰 이름 |
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
| transithub_routing_rules.name | Body | String | 라우팅 룰 이름 |
| transithub_routing_rules.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rules.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rules.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rules.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rules.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rules.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rules.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |

<details><summary>예시</summary>

```json

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
| transithub_routing_rule.name | Body | String | 라우팅 룰 이름 |
| transithub_routing_rule.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rule.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rule.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rule.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rule.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rule.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |

<details><summary>예시</summary>

```json

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
| transithub_routing_rule.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rule.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | 라우팅 룰이 등록될 라우팅 테이블 ID |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_rule | Body | Object | 라우팅 룰 정보 객체 |
| transithub_routing_rule.id | Body | UUID | 라우팅 룰 ID |
| transithub_routing_rule.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_rule.name | Body | String | 라우팅 룰 이름 |
| transithub_routing_rule.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rule.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rule.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rule.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rule.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rule.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |

<details><summary>예시</summary>

```json

```
</details>

---
### 라우팅 룰 수정하기

```
PUT /v2.0/gateways/transithub_routing_rules/{routingRuleId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| routingRuleId | URL | UUID | O | 라우팅 룰 ID |
| transithub_routing_rule | Body | Object | O | 라우팅 룰 정보 객체 |
| transithub_routing_rule.name | Body | String | - | 라우팅 룰 이름 |
| transithub_routing_rule.description | Body | String | - | 라우팅 룰 설명 |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_routing_rule | Body | Object | 라우팅 룰 정보 객체 |
| transithub_routing_rule.id | Body | UUID | 라우팅 룰 ID |
| transithub_routing_rule.tenant_id | Body | String | 테넌트 ID |
| transithub_routing_rule.name | Body | String | 라우팅 룰 이름 |
| transithub_routing_rule.description | Body | String | 라우팅 룰 설명 |
| transithub_routing_rule.cidr | Body | String | 라우팅 룰 IP 대역 |
| transithub_routing_rule.action | Body | Enum | 라우팅 룰 액션<br>`FORWARD`, `BLACKHOLE` 중 하나 |
| transithub_routing_rule.rule_type | Body | Enum | 라우팅 룰 타입<br>`STATIC`, `PROPAGATED` 중 하나 |
| transithub_routing_rule.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_routing_rule.routing_table_id | Body | UUID | 라우팅 테이블 ID |
| transithub_routing_rule.propagation_id | Body | UUID | 라우팅 전파 ID, 전파에 의해 라우팅 타입이 `PROPAGATED`인 경우 사용 |


<details><summary>예시</summary>

```json

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
| transithub_multicast_domain | Body | Object | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.name | Body | String | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | 멀티캐스트 도메인 설명 |
| transithub_multicast_domain.transithub_id | Body | UUID | 멀티캐스트 도메인을 등록할 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

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
| transithub_multicast_domain | Body | Object | O | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.name | Body | String | - | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | - | 멀티캐스트 도메인 설명 |
| transithub_multicast_domain.transithub_id | Body | UUID | O | 멀티캐스트 도메인을 등록할 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

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

```
</details>


---
### 멀티캐스트 도메인 수정하기

```
POST /v2.0/gateways/transithub_multicast_domains/{multicastDomainId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastDomainId | URL | UUID | O | 멀티캐스트 도메인 ID |
| transithub_multicast_domain | Body | Object | O | 멀티캐스트 도메인 정보 객체 |
| transithub_multicast_domain.name | Body | String | - | 멀티캐스트 도메인 이름 |
| transithub_multicast_domain.description | Body | String | - | 멀티캐스트 도메인 설명 |

<details><summary>예시</summary>

```json

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
| transithub_multicast_associations.name | Body | String | 멀티캐스트 연결 이름 |
| transithub_multicast_associations.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_associations.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_associations.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_associations.domain_id | Body | UUID | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>
  
```json

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
| transithub_multicast_association.name | Body | String | 멀티캐스트 연결 이름 |
| transithub_multicast_association.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_association.domain_id | Body | UUID | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>

```json

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
| transithub_multicast_association.name | Body | String | - | 멀티캐스트 연결 이름 |
| transithub_multicast_association.description | Body | String | - | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | O | 연결(Attachment) ID |
| transithub_multicast_association.domain_id | Body | UUID | O | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_association | Body | Object | 멀티캐스트 연결 정보 객체 |
| transithub_multicast_association.id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_association.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_association.name | Body | String | 멀티캐스트 연결 이름 |
| transithub_multicast_association.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_association.domain_id | Body | UUID | 멀티캐스트 도메인 ID |


<details><summary>예시</summary>

```json

```
</details>


---
### 멀티캐스트 연결 수정하기

```
POST /v2.0/gateways/transithub_multicast_associations/{multicastAssociationId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| multicastAssociationId | URL | UUID | O | 멀티캐스트 연결 ID |
| transithub_multicast_association | Body | Object | O | 멀티캐스트 연결 정보 객체 |
| transithub_multicast_association.name | Body | String | - | 멀티캐스트 연결 이름 |
| transithub_multicast_association.description | Body | String | - | 멀티캐스트 연결 설명 |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_association | Body | Object | 멀티캐스트 연결 정보 객체 |
| transithub_multicast_association.id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_association.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_association.name | Body | String | 멀티캐스트 연결 이름 |
| transithub_multicast_association.description | Body | String | 멀티캐스트 연결 설명 |
| transithub_multicast_association.attachment_id | Body | UUID | 연결(Attachment) ID |
| transithub_multicast_association.subnet_id | Body | UUID | 서브넷 ID |
| transithub_multicast_association.domain_id | Body | UUID | 멀티캐스트 도메인 ID |

<details><summary>예시</summary>

```json

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
| transithub_multicast_groups.name | Body | String | 멀티캐스트 그룹 이름 |
| transithub_multicast_groups.description | Body | String | 멀티캐스트 그룹 설명 |
| transithub_multicast_groups.association_id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_groups.ipaddress | Body | UUID | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_groups.member_type | Body | String | 멀티캐스트 멤버 타입 |
| transithub_multicast_groups.source_type | Body | String | 멀티캐스트 소스 타입 |
| transithub_multicast_groups.port_id | Body | UUID | 멀티캐스트 대상 포트 ID |

<details><summary>예시</summary>
  
```json

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
| transithub_multicast_group.name | Body | String | 멀티캐스트 그룹 이름 |
| transithub_multicast_group.description | Body | String | 멀티캐스트 그룹 설명 |
| transithub_multicast_group.association_id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_group.ipaddress | Body | UUID | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_group.member_type | Body | String | 멀티캐스트 멤버 타입 |
| transithub_multicast_group.source_type | Body | String | 멀티캐스트 소스 타입 |
| transithub_multicast_group.port_id | Body | UUID | 멀티캐스트 대상 포트 ID |

<details><summary>예시</summary>

```json

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
| transithub_multicast_group.name | Body | String | - | 멀티캐스트 그룹 이름 |
| transithub_multicast_group.description | Body | String | - | 멀티캐스트 그룹 설명 |
| transithub_multicast_group.association_id | Body | UUID | O | 멀티캐스트 연결 ID |
| transithub_multicast_group.ipaddress | Body | UUID | O | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_group.member_type | Body | String | - | 멀티캐스트 멤버 타입, 멤버로 사용할 경우 `STATIC` 입력<br>멤버타입과 소스타입 중 하나 입력 필수 |
| transithub_multicast_group.source_type | Body | String | - | 멀티캐스트 소스 타입, 소스로 사용할 경우 `STATIC` 입력<br>멤버타입과 소스타입 중 하나 입력 필수 |
| transithub_multicast_group.port_id | Body | UUID | O | 멀티캐스트 대상 포트 ID |


<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| transithub_multicast_group | Body | Object | 멀티캐스트 그룹 정보 객체 |
| transithub_multicast_group.id | Body | UUID | 멀티캐스트 그룹 ID |
| transithub_multicast_group.tenant_id | Body | String | 테넌트 ID |
| transithub_multicast_group.name | Body | String | 멀티캐스트 그룹 이름 |
| transithub_multicast_group.description | Body | String | 멀티캐스트 그룹 설명 |
| transithub_multicast_group.association_id | Body | UUID | 멀티캐스트 연결 ID |
| transithub_multicast_group.ipaddress | Body | UUID | 멀티캐스트 그룹 IP 주소 |
| transithub_multicast_group.member_type | Body | String | 멀티캐스트 멤버 타입 |
| transithub_multicast_group.source_type | Body | String | 멀티캐스트 소스 타입 |
| transithub_multicast_group.port_id | Body | UUID | 멀티캐스트 대상 포트 ID |


<details><summary>예시</summary>

```json

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
