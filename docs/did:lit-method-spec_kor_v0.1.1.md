# LIT DID Method Specification v0.1.1

해당 문서는 lit DID Method 명세서 0.1.1버전이다.

</br>

## Introduction

LEDGIS는 IBCT에서 구축한 블록체인으로 "원장"을 의미하는 LEDGER와 "수호, 방패"를 의미하는 AEGIS 두 단어의 합성어다. LEDGIS는 원장의 무결성을 수호하여 참여자의 신뢰와 이익을 지켜내는 것을 목표로 한다. Ledgis DID체인은 이를 기반으로 lit 컨트랙트를 통해 개체를 투명하고 암호학적으로 신뢰성이 보장된 `did:lit`식별체계를 제공한다.

</br>

## Abstract

Ledgis DID체인은 자기주권신원 및 검증가능한 자격증명을 위한 분산형 네트워크 시스템이다. `did:lit` 식별체계를 이용해 기존의 온라인상에서의 아이덴티티 문제와 대용량 데이터 관리에 활용되도록 설계되었다. LIT DID Method spec은 Ledgis DID체인에서 동작하는 탈중앙 식별자 및 자격증명 상태 정보 관리에 대한 내용을 담고있다.

</br>

## Status Of this document

이 문서는 W3C 표준을 기반으로 한 초안 문서이며 업데이트 될 예정이다.

</br></br>

## 1. lit DID

`did:lit` 식별체계의 lit는 LEDGIS Identity Transformation의 약어로, 중앙기관 없이 사람, 조직 또는 장치를 고유하게 식별하는 방법을 제공하기 위해 개발된 탈중앙화된 식별체계다. `did:lit` 식별체계는 DID Method는 W3C 표준을 준수한다. 이 문서에서는 `lit` 식별 DID 및 DID Document의 생성, 업데이트, 취소 방법 및 Verifiable Credential의 상태 정보 관리에 방안 대해 정의한다.

- Ledgis DID chain : [lit.ledgis.io](https://lit.ledgis.io)

- did system contract code : led.lit

  - table : did, controller, vcstatus

</br>

`lit` DID Document에는 아래와 같은 속성값이 포함된다.

- id
- controller
- authentication
- assertionMethod
- keyAgreement
- capabilityInvocation
- capabilityDelegation
- verificationMethod
- service

</br>

예시.

```json
{
  "@context": "https://www.w3.org/ns/did/v1",
  "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
  "controller": "did:lit:WTu1etB6oU5ggo7Bkrxhd1",
  "service": [],
  "authentication": ["did:lit:AEZ87t1bi5bRxmVh3ksMUi#0"],
  "assertionMethod": ["did:lit:AEZ87t1bi5bRxmVh3ksMUi#1"],
  "keyAgreement": ["did:lit:AEZ87t1bi5bRxmVh3ksMUi#2"],
  "capabilityInvocation": [],
  "capabilityDelegation": ["did:lit:AEZ87t1bi5bRxmVh3ksMUi#3"],
  "verificationMethod": [
    {
      "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#0",
      "type": "EcdsaSecp256k1VerificationKey2019",
      "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
      "publicKeyBase58": "zbPJfARDmbshQ2iSZ3fg5WxAh9VEXAoiyi6QRBJBBj2z"
    },
    {
      "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#1",
      "type": "EcdsaSecp256k1VerificationKey2019",
      "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
      "publicKeyBase58": "24YpP4L2ydSffMn92KF1EvzgwcStdzixut1CDizuCpaqD"
    },
    {
      "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#2",
      "type": "EcdsaSecp256k1VerificationKey2019",
      "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
      "publicKeyBase58": "277hEJxdh596ptwNmyApNTa1TZLMjgpEeQgXbTbXGYns1"
    },
    {
      "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#3",
      "type": "EcdsaSecp256k1VerificationKey2019",
      "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
      "publicKeyBase58": "foWWHmUrwxXFu12aEoS4GK9MdqVNTKLbpGEF9ND7wEvH"
    }
  ],
  "createdAt": "2021-03-17T07:05:14+00:00",
  "updatedAt": "2021-03-17T07:05:14+00:00"
}

```

</br>

### 1.1 lit DID Method Name

lit DID 메소드를 식별하는 이름 문자열은 `lit` 다. `did:lit` 식별체계를 이용하는 식별자는 `did:lit`접두사로 시작해야 한다. 접두사 뒤의 값은 나머지 하위 절에서 설명한다.

</br>

### 1.2 lit DID Format

`did:lit` 식별체계의 식별자는 아래의 형식으로 구성된다.

```json
lit-did = "did:lit" + lit-identifier
lit-identifier = 21, 22 (base58char)
base58char = "1" / "2" / "3" / "4" / "5" / "6" / "7" / "8" / "9" / "A" /"B" / "C"
            / "D" / "E" / "F" / "G" / "H" / "J" / "K" / "L" / "M" / "N" / "P" / "Q"
            / "R" / "S" / "T" / "U" / "V" / "W" / "X" / "Y" / "Z" / "a" / "b" / "c"
            / "d" / "e" / "f" / "g" / "h" / "i" / "j" / "k" / "m" / "n" / "o" / "p"
            / "q" / "r" / "s" / "t" / "u" / "v" / "w" / "x" / "y" / "z"
```

</br>

### 1.2.1 lit-identifier 생성 방법

`did:lit` 식별자는 아래의 규칙에 따라 정의된다. 모든 `did:lit` 식별자는 16바이트의 uuid 알파벳을 base58로 인코딩하여 사용한다. 0, O, I, l 문자에 대한 가독성 문제를 피하기 위해 base58을 사용한다.

</br>

lit 식별자값 정규 표현식은 아래와 같다

```txt
^[1-9A-HJ-NP-Za-km-z]{21,22}$
```

</br>

did를 포함한 lit DID 식별자의 정규 표현식은 아래와 같다.

```txt
^(did:lit:(?:[1-9A-HJ-NP-Za-km-z]{21,22}))$
```

</br>

유효한 `did:lit` 식별자 DID는 `did:lit:AEZ87t1bi5bRxmVh3ksMUi` 같을 수 있다.

</br>

### 1.3 did system contract

</br>

Ledgis DID체인은 계정과 권한 기반으로 동작한다. 사용자가 계정을 생성하면 기본적으로 owner, active권한이 생성된다. owner권한은 모든 계정에 대한 권한 계층의 루트에 위치한다. 즉, 계정에 매핑된 권한 중 가장 높은 권한이다. active권한은 owner권한과 관련된 키 변경을 제외하고 트랜잭션을 실행하는데 사용된다. Ledgis DID체인은 active하위 권한에 목적에 맞는 권한을 추가 생성할 수 있다. 이러한 계정, 권한의 특성을 이용하여 사용자의 SSI(Self Sovereign Identity) 실현하고자 한다. 이를 위해 `did:lit`와 관련된 모든 제어 기능을 Ledgis DID체인의 시스템 컨트랙트인 `led.lit`로 구현했다.

</br>

`led.lit` 시스템 컨트랙트를 통해 1. controller권한 및 delegator권한 생성, 2. controller did document 생성, 3. did document CRUD를 수행할 수 있다.

</br>

### 1.3.1 account with customized permission

사용자가 새로운 계정을 생성하면서 권한 생성, controller용 did document가 생성된다. 계정 생성 시 기본적으로 owner권한, active권한이 있고 controller권한과 delegator권한을 추가로 생성한다(updateauth). `led.lit` 스마트 컨트랙트의 액션을 controller권한, delegator권한에 링크하여 해당 권한으로 링크 된 스마트 컨트랙트 액션을 실행할 수 있도록 설정할 수 있다(linkauth). 링크를 통해 액션 실행 권한의 유효성 검사 시 필요한 권한을 조회할 때 유용하다. 각각의 권한의 역할은 아래와 같다.

- controller 권한

    did document에 대한 CRUD가 가능한 권한으로 did document에 대한 CRUD 트랜잭션 실행 시 Ledgis DID체인에서 반드시 확인하는 권한

- delegator 권한

    did document의 capabilityInvocation에 CRUD가 가능한 권한으로 capabilityInvocation항목에 did 추가/삭제 시 반드시 환인하는 권한

</br>

controller, delegator권한을 추가한 계정은 아래와 같이 보여진다.

```txt
user permissions: 
    owner        1:  PUBKEYVALUE   1 <Owner permission public key value>
        active       1:  PUBKEYVALUE   1 <Active permission public key value>
            controller   1:  PUBKEYVALUE   1 <Controller permission public key value>
                delegator    1:  CONTROLLER AUTHORITY   1 <User's controller permission >
```

</br>
</br>

### 1.3.2 controller did document

Ledgis DID체인에서 계정을 생성하면 controller did document가 생성된다. 우리는 did document를 수정 권한을 사용자의 계정과 did document의 controller 속성값과 연결하고자 했다. W3C표준에 따르면 controller 속성값은 did정규식을 만족해야한다. 하지만 Ledgis DID체인의 계정은 `did:lit`정규식을 만족하지 않는다. 그렇기 때문에 사용자 계정과 controller 속성값을 연결하기 위해 controller did document를 만들었다. 사용자 계정과 controller did를 매핑한 테이블은 controller테이블에 명시하고 있다.

controller did document는 별도의 키 셋 없이 did document의 id, controller값만 보유하고 있다. 이때 did document의 id와 controller값은 동일한 did값이 들어간다. controller did document의 id값과 사용자 계정을 매핑시켜 Ledgis DID체인에 기록한다. 만약 사용자가 자신의 DID Document를 수정하고자 할 경우, 노드는 DID Document에 있는 controller값을 controller테이블에서 조회한다. 매핑된 계정의 controller권한 또는 delegator권한 검사를 통해 DID Document의 CRUD가 수행된다.

</br>

controller did document 예시

```json
{
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:lit:WTu1etB6oU5ggo7Bkrxhd1",
    "controller": "did:lit:WTu1etB6oU5ggo7Bkrxhd1",
    "service": [],
    "authentication": [],
    "assertionMethod": [],
    "keyAgreement": [],
    "capabilityInvocation": [],
    "capabilityDelegation": [],
    "verificationMethod": [],
    "createdAt": "2021-06-07T05:42:12+00:00",
    "updatedAt": "2021-06-07T05:42:12+00:00"
}
```

</br>

### 1.3.3 DID Document CRUD Operation

(2절 참고)

</br></br>

## 2. DID Document CRUD Operation

</br>

DID Document에 대한 CRUD를 수행하는 `led.lit` 컨트랙트의 액션은 아래와 같다.

</br>

did document의 CRUD 액션

```json
[
    "deletedid",
    "regdid",
]
```

</br>

verification method의 CRUD 액션

```json
[
    "updatekeys",   
]
```

</br>

controller의 CRUD 액션

```json
[
    "changectrl",
]
```

</br>

verification relationship의 CRUD 액션

```json
[
    "addasserter",
    "addauth",
    "adddelegator",
    "addinvocator",
    "addkeyagrm",
    "rmasserter",
    "rmauth",
    "rmdelegator",
    "rminvocator",
    "rmkeyagrm",
]
```

</br>

service의 CRUD 액션

```json
[
    "addservice",
    "rmservice",
]
```

</br>

## Create, Update, Deactivate

### 2.1 did document

### 2.1.1 regdid

DID Document를 생성하기 위해서는 lit 컨트랙트의 regdid액션을 사용한다. regdid액션 실행 결과는 Ledgis DID체인에 저장되는 실제 did document데이터다. 상호 호환성을 위해 DID Document read작업의 결과는 W3C의 포맷에 맞게 변환하여 반환한다. create작업의 결과와 read작업의 결과가 다른것을 확인할 수 있다.

</br>

아래는 regdid액션에 필요한 파라미터에 대한 설명이다.

```txt
{
    controller: <user controller did's uuid value>,
    uuid : <lit did Identifier>,
    service : [{Service info DID subject is using}]
    verificationMethod: [{List of VerificationMethod}],
    authentication: [{PublicKey Value and Public Key Controller}],
    assertionMethod: [{PublicKey Value and Public Key Controller}],
    keyAgreement: [{PublicKey Value and Public Key Controller}],
    capabilityInvocation: [{PublicKey Value and Public KeyController}],
    capabilityDelegation: [{PublicKey Value and Public KeyController}]
}
```

</br>

regdid 파라미터 예시

```json
{
  "controller": "317158017176121438146673224759223206864",
  "uuid": "99394650071860096581833102200703088599",
  "service": [],
  "verificationMethod": [
    {
      "publicKey": "EOS7gRwd51sP9XjC1oqRCr585v2S8w68iq2rP63689anxPMQe2K2s",
      "controller": "99394650071860096581833102200703088599",
      "index": 0
    },
    {
      "publicKey": "EOS81SonGPCWvqUW4ec8DuJCreQp3uTQ2QnrAjrZyHLc9bCHT8mXN",
      "controller": "99394650071860096581833102200703088599",
      "index": 1
    },
    {
      "publicKey": "EOS8YcshKyX4sG3GPRpaTdAsz5EmAFZuLLNJtbRXEHE6nrfAEpf7m",
      "controller": "99394650071860096581833102200703088599",
      "index": 2
    },
    {
      "publicKey": "EOS6pUhw1ueSAXdPaz3PrXQrGLCEtMgrvemmLSWJ5ZpiJNRq1mtRj",
      "controller": "99394650071860096581833102200703088599",
      "index": 3
    },
    {
      "publicKey": "EOS73cAB2C6xdPdn1b3361X44vdrifqBdHodVDCp476nDVP3M1KpM",
      "controller": "99394650071860096581833102200703088599",
      "index": 4
    }
  ],
  "authentication": [ { "uuid": "99394650071860096581833102200703088599", "index": 0 } ],
  "assertionMethod": [],
  "keyAgreement": [],
  "capabilityInvocation": [],
  "capabilityDelegation": []
}
```

</br>

### 2.1.2 deletedid

DID Document를 Ledgis DID체인에서 삭제(비활성화)하고자 할 경우, `deletedid` 액션을 사용한다.

```txt
contract : led.lit
action : deletedid
input : {
    "controller" :  <current controller uuid value in DID Document>,
    "uuid" : <lit did Identifier>
}
```

</br>

deletedid 파라미터 예시

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599"
}
```

</br>
</br>

### 2.2 controller

### 2.2.1 changectrl

 `controller` 을 수정할 경우,  `changectrl` 액션을 사용한다.

```txt
contract : led.lit
action : changectrl
input : {
    "from" :  <current controller did as uuid of the target DID Document>,
    "to" : <controller did as uuid to change>,
    "uuid" : <target did document's id as uuid>,
}
```

</br>

changectrl 파라미터 예시

```json
{
    "from": "317158017176121438146673224759223206864",
    "to": "102328121263104977887553834695733343061",
    "uuid": "99394650071860096581833102200703088599"
}
```

</br>
</br>

### 2.3 verification method

### 2.3.1 updatekeys

 `verificationMethod` 을 수정할 경우,  `updatekeys` 액션을 사용한다.

```txt
contract : led.lit
action : updatekeys
input : {
    "controller" :  <current controller did value as uuid of in DID Document>,
    "uuid" : <lit did Identifier>,
    "verificationMethod" : <verificaionMethod value in array>
}
```

</br>

updatekeys 파라미터 예시

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "verificationMethod": [
      {
        "index": 0,
        "publicKey": "PUB_K1_7VsJLbbTJtvTfjTAJ9WLa2wTn4P7fBk71UckBDtFHkerou1hDd",
        "controller": "317158017176121438146673224759223206864"
      },
      {
        "index": 1,
        "publicKey": "PUB_K1_7wkd9kjfdMbxRYCrvYUbJdCKWYn8hqQxBMchLjQCgTpdwc4PFr",
        "controller": "317158017176121438146673224759223206864"
      },
      {
        "index": 2,
        "publicKey": "PUB_K1_8EYpZU9EL1meLKErcV9RJzmS5gHN4Tzn9rtQtHuyqzvhFeLAXc",
        "controller": "317158017176121438146673224759223206864"
      },
      {
        "index": 3,
        "publicKey": "PUB_K1_5NuY4gFU7zmgVJMtjK2HBnhT2C296mPV8MrXk15ehCHGYgm1YS",
        "controller": "317158017176121438146673224759223206864"
      }
    ]
}
```

</br></br>

### 2.4 verification relationship

verification relationship에는 `authentication`, `assertionMethod`, `keyAgreement`, `capabilityDelegation`, `capabiltiyInvoctaion`이 있다. `capabilityInvocation`이외의 속성들은 실행하는 액션명만 다르고 입력한 파라미터는 동일하다. 아래 `authentication`에 대한 추가/삭제를 참고해 목적에 맞는 액션을 실행하면 된다. `authentication`, `assertionMethod`, `keyAgreement`, `capabilityDelegation`은 사용자의 controller권한을 이용해 트랜잭션을 실행한다.

- authentication - addauth, rmauth

- assertionMethod - addasserter, rmasserter

- keyAgreement - addkeyagrm, rmkeyagrm

- capablityDelegation - adddelegator, rmdelegator

</br>

### 2.4.1 authentication update

</br>

authentication, assertionMethod, keyAgreement, capabilityDelegation에 대한 추가/삭제는 사용자 계정의 controller권한을 이용해 트랜잭션을 실행한다.

`authentication` 항목을 추가할 경우, `addauth` 액션을 사용한다.

```txt
contract : led.lit
action : addauth
input : {
    "controller" :  <current controller uuid value in DID Document>,
    "uuid" : <lit did identifier as uuid>,
    "authenticator" : <value of new authentication data with uuid and index to add in DID Document>
}
```

</br>

addauth 파라미터 예시

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "authenticator": { "uuid": "99394650071860096581833102200703088599", "index": 0 }
}
```

</br>
</br>

 `authentication` 항목을 삭제할 경우, `rmauth` 액션을 사용한다.

```txt
contract : led.lit
action : rmauth
input : {
    "controller" :  <current controller uuid value in DID Document>,
    "uuid" : <lit did identifier as uuid>,
    "authenticator" : <value of authentication with uuid, index to remove from DID Document>
}
```

</br>

rmauth 파라미터 예시

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "authenticator": { "uuid": "99394650071860096581833102200703088599", "index": 0 }
}
```

</br></br>

### 2.4.2 capabilityInvocation udpate

capabilityInvocation에 대한 추가/삭제는 사용자 계정의 delegator권한을 이용해 트랜잭션을 실행한다.

`capabiltiyInvocation` 항목을 추가할 경우, `addinvocator` 액션을 사용한다.

```txt
contract : led.lit
action : addinvocator
input : {
    "uuid" : <lit did Identifier>,
    "delegator" : <current capabiltiyDelegation Key information in DID Document>,
    "signature" : <signature of delegator using key index in verificationMethod>,
    "capabilityInvocator" : <value of new capabiltiyInvocation with uuid, index to add in DID Document>
}
```

</br>

addinvocator 파라미터 예시

```json
{
    "delegator": { "uuid": "317158017176121438146673224759223206864", "index": 15 },
    "signature": "SIG_K1_K86rnAkBqcWFT2XoUNrhXdyoc3gdajLN6y4RmCb1mqSj3W4Q6TtRgQL5PWwvdBAdLjKha3ZK3DLzYLWDTVvuXQW87McvKT",
    "capabilityInvocator": { "uuid": "273181167325615934766063315144949048995", "index": 9 },
    "uuid": "99394650071860096581833102200703088599"
}
```

</br>

 `capabiltiyInvocation` 항목을 삭제할 경우, `rminvocator` 액션을 사용한다.

```txt
contract : led.lit
action : rminvocator
input : {
    "uuid" : <lit did Identifier>,
    "delegator" : <current capabiltiyDelegation key information in DID Document>,
    "signature" : <signature of delegator using key index in verificationMethod>,
    "capabilityInvocator" : <value of capabiltiyInvocation with uuid, index to remove from DID Document>
}
```

</br>

rminvocator 파라미터 예시

```json
{
    "delegator": { "uuid": "317158017176121438146673224759223206864", "index": 15 },
    "signature": "SIG_K1_K86rnAkBqcWFT2XoUNrhXdyoc3gdajLN6y4RmCb1mqSj3W4Q6TtRgQL5PWwvdBAdLjKha3ZK3DLzYLWDTVvuXQW87McvKT",
    "capabilityInvocator": { "uuid": "273181167325615934766063315144949048995", "index": 9 },
    "uuid": "99394650071860096581833102200703088599"
}
```

</br></br>

### 2.5 service

### 2.5.1 addservice

`service` 항목을 추가할 경우, `addservice` 액션을 사용한다.

```txt
contract : led.lit
action : addservice
input : {
    "controller" : <current controller uuid value in DID Document>,
    "uuid" : <lit did Identifier>,
    "service" : <data of service provider with id, type, endpoint>
}
```

</br>

addservice 파라미터 예시

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "service": {
        "id": "did:lit:CeZJ3DpfCVg51SYWDUsxc7",
        "type": "TrustedThirdPartyVerificationVersion1.0Service",
        "endpoint": "https://ttp.crosscert.com/blahblah"
    }
}
```

</br>

### 2.5.2 rmservice

 `service` 항목을 삭제할 경우, `rmservice` 액션을 사용한다.

```txt
contract : led.lit
action : rmservice
input : {
    "controller" : <controller uuid value in DID Document>,
    "uuid" : <lit did Identifier>,
    "serviceId" : <Service Id to remove>
}
```

</br>

rmservice 파라미터 예시

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "serviceId": "did:lit:CeZJ3DpfCVg51SYWDUsxc7"
}
```

</br>
</br>

## Read

DID Universal Resolver을 통해 `did:lit` 식별자를 조회할 수 있다.

아래의 결과에 따라 input값을 주어야한다.

```txt
endpoint: /universal resolver
input: {DID}
output: {DID Document}
```

</br>

예시:

```json
"input": "did:lit:AEZ87t1bi5bRxmVh3ksMUi"

"output" : 
{
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
    "controller": "did:lit:WTu1etB6oU5ggo7Bkrxhd1",
    "service": [],
    "authentication": [
        "did:lit:AEZ87t1bi5bRxmVh3ksMUi#0"
    ],
    "assertionMethod": [
        "did:lit:AEZ87t1bi5bRxmVh3ksMUi#1"
    ],
    "keyAgreement": [
        "did:lit:AEZ87t1bi5bRxmVh3ksMUi#2"
    ],
    "capabilityInvocation": [],
    "capabilityDelegation": [
        "did:lit:AEZ87t1bi5bRxmVh3ksMUi#3",
        "did:lit:AEZ87t1bi5bRxmVh3ksMUi#4"
    ],
    "verificationMethod": [
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#0",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "zbPJfARDmbshQ2iSZ3fg5WxAh9VEXAoiyi6QRBJBBj2z"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#1",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "24YpP4L2ydSffMn92KF1EvzgwcStdzixut1CDizuCpaqD"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#2",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "277hEJxdh596ptwNmyApNTa1TZLMjgpEeQgXbTbXGYns1"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#3",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "foWWHmUrwxXFu12aEoS4GK9MdqVNTKLbpGEF9ND7wEvH"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#4",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "qVFze1eaPJavKvmGqEsF4LPRdUDzsvFukqQH5KVhseE1"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#5",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "29NGo9CDpMcVWhTp1XKNse63DVzgHUHiQpWv1bQMXj7Wx"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#6",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "nnvBVyLX77f39KwNrsUhkdvjWCVXt4o71U6DBbZSbDZA"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#7",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "nESzTFNwQfdar2v4aHPKeYZA6fobDfdYsssFV8ZBzRTZ"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#8",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "sZzPChJYcibqcvr7nvHJHyVUtACKoNyRarsppdwMJvGN"
        },
        {
            "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi#9",
            "type": "EcdsaSecp256k1VerificationKey2019",
            "controller": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
            "publicKeyBase58": "z2SqWSUz92ULURxmr254RWbg3UdFLwRSLQctuwHHxbWy"
        }
    ],
    "createdAt": "2021-06-07T06:23:54+00:00",
    "updatedAt": "2021-07-08T02:25:35+00:00"
}
```

</br>
</br>
</br>

## 3. VC Management

`did:lit` 식별체계는 DID Method뿐 아니라 Verifiable Credential의 상태 정보를 관리하는 기능을 제공한다.

모든 Verifiable Credential에는 고유한 ID가 있다. 그리고 모든 Verifiable Credential에는 상태 정보가 있다. 이를 관리하기 위해 Ledgis DID체인에서는 Verifiable Credential의 상태 정보 관리 방안을 제공한다. Verifiable Credential의 상태 정보는 유효, 중지, 폐기 등이 있을 수 있다. 아래는 Verifiable Credential에 대한 예시다.

```json
    {
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "http://127.0.0.1:4000/Credentials.jsonld"
      ],
      "vcId": "a264fa35-aa35-46cc-9e84-68d7b5b70941",
      "type": [ "VerifiableCredential", "HealthCheckUp" ],
      "issuer": "did:lit:8UPz7JKwCvWHGtVBvayMBP",
      "issuanceDate": "2021-07-16T03:48:12.833Z",
      "credentialSubject": {
        "type": "HealthCheckUp",
        "subjectDid": "did:lit:W4fgrbXRaSURDcjEJ4APcS",
        "height": "200cm",
        "weight": "100kg",
        "colorVision": "정상",
        "ophthalmology": "정상",
        "internalMedicinenternal": "정상",
        "surgery": "정상",
        "vision": "not good",
        "bloodPressure": "129/76"
      },
      "proof": {
        "type": "EcdsaSecp256k1Signature2019",
        "created": "2021-07-16T03:48:12Z",
        "verificationMethod": "did:lit:8UPz7JKwCvWHGtVBvayMBP#10",
        "proofPurpose": "assertionMethod",
        "jws": "eyJhbGciOiJFUzI1NksiLCJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdfQ..MEUCIQDK_UfYiFBZFc_TOUQdYfq3NFblD63usFs1t8x00F23wAIgIoZX4EN4kdL3nIjeDR5jb0BviNHsKrfRzgm0PruPx_4"
      }
    }
```

</br>

### 3.1 Register VC-id Status

특정 Verifiable Credential의 상태정보를 등록하려면 `regvcs` 액션을 사용한다.

```txt
contract : led.lit
action : regvcs
input : {
    "issuer" : <user account who is registering VC status info>,
    "vcUuid" : <id value of Verifiable Credential to bigint>,
    "vcStatus" : <status Info of Verifiable Crednetial>,
    "expiredAt": <expireDate of Verifiable Credential>,
}
```

</br>

regvcs 파라미터 예시

```json
{
    "issuer": "test3",
    "vcUuid": "62677297661723981814102856366482868005",
    "vcStatus": "valid",
    "expiredAt": 1626407638
}
```

</br></br>

### 3.2 Update VC-id Status

특정 Verifiable Credential의 상태정보를 수정하려면 `updatevcs` 액션을 사용한다.

```txt
contract : led.lit
action : updatevcs
input : {
    "issuer" : <user account who is updating specific VC status info>,
    "vcUuid" : <id value of Verifiable Credential>,
    "vcStatus" : <status Info of Verifiable Crednetial>,
    "expiredAt": <expireDate of Verifiable Credential>,
}
```

</br>

updatevcs 파라미터 예시

```json
{
    "issuer": "test3",
    "vcUuid": "62677297661723981814102856366482868005",
    "vcStatus": "revoke",
    "expiredAt": 1626407943
}
```

</br></br>

### 3.3 Remove VC-id Status

특정 Verifiable Credential가 폐기되었다면 블록체인에 등록된 상태 정보를 삭제하기 위해 `rmvcs` 액션을 사용한다.

```txt
contract : led.lit
action : rmvcs
input : {
    "issuer" : <user account who is removing specific VC status info>,
    "vcUuid" : <id value of Verifiable Credential>
}
```

</br>

rmvcs 파라미터 예시

```json
{
    "issuer": "test3",
    "vcUuid": "62677297661723981814102856366482868005"
}
```

</br></br>

### 3.4 Clear VC-Status

동일한 사용자가 등록한 특정 Verifiable Credentials 정보를 지우려면 `clearvcs`액션을 사용해야한다.

```txt
contract : led.lit
action : clearvcs
input : {
    "issuer" : <user account who is clearing VCs status info>
}
```

</br>

rmvcs 파라미터 예시

```json
{
    "issuer": "test3"
}
```

</br></br>

## 4. Security Considerations

`did:lit` 식별체계는 완전한 SSI(Self Sovereign Identity)를 실현하기 위해 설계되었다. DID Document의 접근 통제를 위해 사용자 Ledgis DID체인 계정에 새로운 controller권한, delegator권한을 추가하였다. `did:lit` 식별체계에서 DID Document에 대한 CRUD작업은 DID Document controller값의 계정을 확인하고, 해당 계정에 controller권한이 있는지 확인한다. 해당 권한이 있는 사용자 계정만 DID Document를 수정할 수 있도록 설계하였다.

</br></br>

## 5. Privacy Consideration

Ledgis DID체인은 사용자 프라이버시를 고려하여 PII(Personally-Identifiable Information)없이, DID Document정보, Verifiable Credential의 상태 정보만 등록한다.

현재 Ledgis DID체인에는 아래 데이터를 저장한다.

- 개체를 식별하는데 사용되는 DID Document
- Verifiable Credential의 유효성을 관리할 수 있는 상태정보

</br></br>

## References

[1] IBCT, [Ledgis.io](https://www.ledgis.io/)

[2] Decentralized Identifiers (DIDs) v1.0, [W3C did-core](https://www.w3.org/TR/did-core/)