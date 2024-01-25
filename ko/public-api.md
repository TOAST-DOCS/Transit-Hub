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
GET /v2.0/gateways/asterisks
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
| asterisks | Body | Array | 트랜짓 허브 정보 객체 목록 |
| asterisks.id | Body | UUID | 트랜짓 허브 ID |
| asterisks.tenant_id | Body | String | 테넌트 ID |
| asterisks.name | Body | String | 트랜짓 허브 이름 |
| asterisks.description | Body | String | 트랜짓 허브 설명 |
| asterisks.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| asterisks.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부  |
| asterisks.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |

<details><summary>예시</summary>

```json

```
</details>

---
### 트랜짓 허브 보기

```
GET /v2.0/gateways/asterisks/{transithubId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithubId | URL | UUID | O | 트랜짓 허브 ID |

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| asterisk | Body | Object | 트랜짓 허브 정보 객체 |
| asterisk.id | Body | UUID | 트랜짓 허브 ID |
| asterisk.tenant_id | Body | String | 테넌트 ID |
| asterisk.name | Body | String | 트랜짓 허브 이름 |
| asterisk.description | Body | String | 트랜짓 허브 설명 |
| asterisk.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| asterisk.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부  |
| asterisk.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |

<details><summary>예시</summary>

```json

```
</details>

---
### 트랜짓 허브 생성하기

```
POST /v2.0/gateways/asterisks
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| asterisk | Body | Object | O | 트랜짓 허브 정보 객체 |
| asterisk.name | Body | String | - | 트랜짓 허브 이름 |
| asterisk.description | Body | String | - | 트랜짓 허브 설명 |
| asterisk.multicast_enable | Body | Boolean | O | 멀티캐스트 기능 사용 여부 |
| asterisk.default_association_enable | Body | Boolean | O | 기본 라우팅 테이블 연결 기능 사용 여부 |
| asterisk.default_propagation_enable | Body | Boolean | O | 기본 라우팅 테이블 전파 기능 사용 여부 |




<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| asterisk | Body | Object | 트랜짓 허브 정보 객체 |
| asterisk.id | Body | UUID | 트랜짓 허브 ID |
| asterisk.tenant_id | Body | String | 테넌트 ID |
| asterisk.name | Body | String | 트랜짓 허브 이름 |
| asterisk.description | Body | String | 트랜짓 허브 설명 |
| asterisk.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| asterisk.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부 |
| asterisk.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |


<details><summary>예시</summary>

```json

```
</details>

---
### 트랜짓 허브 수정하기

```
PUT /v2.0/gateways/asterisks/{transithubId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithubId | URL | UUID | O | 트랜짓 허브 ID |
| asterisk | Body | Object | O | 트랜짓 허브 정보 객체 |
| asterisk.name | Body | String | - | 트랜짓 허브 이름 |
| asterisk.description | Body | String | - | 트랜짓 허브 설명 |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| asterisk | Body | Object | 트랜짓 허브 정보 객체 |
| asterisk.id | Body | UUID | 트랜짓 허브 ID |
| asterisk.tenant_id | Body | String | 테넌트 ID |
| asterisk.name | Body | String | 트랜짓 허브 이름 |
| asterisk.description | Body | String | 트랜짓 허브 설명 |
| asterisk.multicast_enable | Body | Boolean | 멀티캐스트 기능 사용 여부 |
| asterisk.default_association_enable | Body | Boolean | 기본 라우팅 테이블 연결 기능 사용 여부 |
| asterisk.default_propagation_enable | Body | Boolean | 기본 라우팅 테이블 전파 기능 사용 여부 |


<details><summary>예시</summary>

```json

```
</details>

---
### 트랜짓 허브 삭제하기

```
DELETE /v2.0/gateways/asterisks/{transithubId}
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| transithubId | URL | UUID | O | 트랜짓 허브 ID |


#### 응답
이 API는 응답 본문을 반환하지 않습니다.









## 연결

### 연결 목록 보기

```
GET /v2.0/gateways/asterisk_attachments/
X-Auth-Token: {tokenId}
```

#### 요청
이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 연결 ID |
| name | Query | String | - | 조회할 연결 이름 |
| resource_id | Query | UUID | - | 조회할 리소스 ID |
| resource_type | Query | UUID | - | 조회활 리소스 타입, 현재 `VPC` 타입만 조회 가능 |
| subnet_id | Query | UUID | - | 조회할 서브넷 ID |
| asterisk_id | Query | UUID | - | 조회할 트랜짓 허브 ID |



#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| asterisk_attachments | Body | Array | 연결 정보 객체 목록 |
| asterisk_attachments.id | Body | UUID | 연결 ID |
| asterisk_attachments.tenant_id | Body | String | 테넌트 ID |
| asterisk_attachments.name | Body | String | 연결 이름 |
| asterisk_attachments.description | Body | String | 연결 설명 |
| asterisk_attachments.resource_id | Body | UUID | 리소스 ID |
| asterisk_attachments.resource_type | Body | UUID | 리소스 타입 |
| asterisk_attachments.subnet_id | Body | UUID | 서브넷 ID |
| asterisk_attachments.asterisk_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

```
</details>

---
### 연결 보기

```
GET /v2.0/gateways/asterisk_attachments/{attachmentId}
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
| asterisk_attachment | Body | Object | 연결 정보 객체  |
| asterisk_attachment.id | Body | UUID | 연결 ID |
| asterisk_attachment.tenant_id | Body | String | 테넌트 ID |
| asterisk_attachment.name | Body | String | 연결 이름 |
| asterisk_attachment.description | Body | String | 연결 설명 |
| asterisk_attachment.resource_id | Body | UUID | 리소스 ID |
| asterisk_attachment.resource_type | Body | UUID | 리소스 타입 |
| asterisk_attachment.subnet_id | Body | UUID | 서브넷 ID |
| asterisk_attachment.asterisk_id | Body | UUID | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

```
</details>

---
### 연결 생성하기

```
POST /v2.0/gateways/asterisk_attachments/
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| asterisk_attachment | Body | Object | O | 로드 밸런서 정보 객체 |
| asterisk_attachment.name | Body | String | - | 연결 이름 |
| asterisk_attachment.description | Body | String | - | 연결 설명 |
| asterisk_attachment.resource_id | Body | UUID | O | 리소스 ID |
| asterisk_attachment.resource_type | Body | UUID | O | 리소스 타입, 현재 `VPC` 타입만 입력 가능 |
| asterisk_attachment.subnet_id | Body | UUID | O | 서브넷 ID |
| asterisk_attachment.asterisk_id | Body | UUID | O | 트랜짓 허브 ID |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| asterisk_attachment | Body | Object | 연결 정보 객체  |
| asterisk_attachment.id | Body | UUID | 연결 ID |
| asterisk_attachment.tenant_id | Body | String | 테넌트 ID |
| asterisk_attachment.name | Body | String | 연결 이름 |
| asterisk_attachment.description | Body | String | 연결 설명 |
| asterisk_attachment.resource_id | Body | UUID | 리소스 ID |
| asterisk_attachment.resource_type | Body | UUID | 리소스 타입 |
| asterisk_attachment.subnet_id | Body | UUID | 서브넷 ID |
| asterisk_attachment.asterisk_id | Body | UUID | 트랜짓 허브 ID |


<details><summary>예시</summary>

```json

```
</details>

---
### 연결 수정하기

```
PUT /v2.0/gateways/asterisk_attachments/{attachmentId}
X-Auth-Token: {tokenId}
```

#### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| attachmentId | URL | UUID | O | 연결 ID |
| asterisk_attachment | Body | Object | O | 연결 정보 객체 |
| asterisk_attachment.name | Body | String | - | 연결 이름 |
| asterisk_attachment.description | Body | String | - | 연결 설명 |

<details><summary>예시</summary>

```json

```
</details>

#### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| asterisk_attachment | Body | Object | 연결 정보 객체  |
| asterisk_attachment.id | Body | UUID | 연결 ID |
| asterisk_attachment.tenant_id | Body | String | 테넌트 ID |
| asterisk_attachment.name | Body | String | 연결 이름 |
| asterisk_attachment.description | Body | String | 연결 설명 |
| asterisk_attachment.resource_id | Body | UUID | 리소스 ID |
| asterisk_attachment.resource_type | Body | UUID | 리소스 타입 |
| asterisk_attachment.subnet_id | Body | UUID | 서브넷 ID |
| asterisk_attachment.asterisk_id | Body | UUID | 트랜짓 허브 ID |


<details><summary>예시</summary>

```json

```
</details>

---
### 연결 삭제하기

```
DELETE /v2.0/gateways/asterisk_attachments/{attachmentId}
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











