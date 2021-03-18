# LIT DID Method Specification

</br>

## Introduction

LEDGIS는 IBCT에서 구축한 블록체인으로 "원장"을 의미하는 LEDGER와 "수호, 방패"를 의미하는 AEGIS 두 단어의 합성어입니다.

LEDGIS는 원장의 무결성을 수호하여 참여자의 신뢰와 이익을 지켜내는 것을 목표로 합니다.

Ledgis DID체인은 이를 기반으로 lit 컨트랙트를 통해 개체를 투명하고 암호학적으로 신뢰성이 보장된 `did:lit`식별체계를 제공합니다.


</br>

## Abstract

Ledgis DID체인은 자기주권신원 및 검증가능한 자격증명을 위한 분산형 네트워크 시스템입니다.

Ledgis DID체인은 `did:lit` 식별체계를 이용해 기존의 온라인상에서의 아이덴티티 문제를 개선할 수 있을 것으로 예상됩니다.

LIT DID Method spec은 Ledgis DID체인에서 동작하는 탈중앙 식별자 및 자격증명 상태 정보 관리에 대한 내용을 담고있습니다.

</br>

## Status Of this document

이 문서는 W3C 표준을 기반으로 한 초안 문서이며 업데이트 될 예정입니다.

</br></br>

## 1. lit DID

`did:lit` 식별체계의 lit는 LEDGIS identity transformation의 약어로, 중앙기관 없이 사람, 조직 또는 장치를 고유하게 식별하는 방법을 제공하기 위해 개발된 탈중앙화된 식별체계입니다. 

`did:lit` 식별체계는 DID Method는 W3C 표준을 따릅니다. 이 문서에서는 `lit` 식별 DID 및 DID Document의 생성, 업데이트, 취소 방법 및 Verifiable Credential의 상태 정보 관리에 방안 대해 정의합니다. 

</br>

### 1.1 lit DID Method Name

lit DID 메소드를 식별하는 이름 문자열은 `lit` 입니다. `did:lit` 식별체계를 이용하는 식별자는 `did:lit`접두사로 시작해야 합니다. 접두사 뒤의 값은 나머지 아래 절에서 설명합니다.

</br>

### 1.2 lit DID Format

`did:lit` 식별체계의 식별자는 아래의 형식으로 구성됩니다.

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

`did:lit` 식별자는 아래의 규칙에 따라 정의됩니다. 모든 `did:lit` 식별자는 16바이트의 uuid 알파벳을 base58로 인코딩하여 사용합니다. 0, O, I, l 문자에 대한 가독성 문제를 피하기 위해 base58을 사용합니다.

</br>

lit 식별자값 정규 표현식은 아래와 같습니다 
```
^[1-9A-HJ-NP-Za-km-z]{21,22}$
```


</br>

did를 포함한 lit DID 식별자의 정규 표현식은 아래와 같습니다.

```
^(did:lit:(?:[1-9A-HJ-NP-Za-km-z]{21,22}))$
```

</br>


유효한 `did:lit` 식별자 DID는 did:lit:AEZ87t1bi5bRxmVh3ksMUi 같을 수 있습니다.

</br></br>

## 2. DID Document

</br>

### 2.1 DID Document 예시

`lit` DID Document에는 아래와 같은 속성값이 포함됩니다.

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
  "controller": "didtesttest1",
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
  "createdAt": "2021-03-17T07:05:14+00:00",
  "updatedAt": "2021-03-17T07:05:14+00:00"
}

```

</br>

## 2.2 CRUD Operation

DID method 명세에는 lit 컨트랙트를 통해 CRUD(Create, Read, Update, Delete)할 수 있는 데이터에 대해 소개하고 작업 과정에 대해 설명합니다.

DID method 명세에는 DID Document 관리를 위해 목적에 맞는 액션에 대해 소개합니다.

아래에 각 정보의 CRUD방법에 대한 설명입니다.

</br>

### 2.2.1 Add Permission

`did:lit` 식별자는 Ledgis DID체인의 lit 컨트랙트에 의해 관리됩니다.

SSI(Self Sovereign Identity)를 실현하기 위해 사용자의 DID, DID Document는 사용자가 직접 관리하며 DID Document등록, 수정, 삭제 모두 사용자에 의해 직접 수행됩니다.

이를 위해 `did:lit` 식별체계에서는 Ledgis DID체인의 계정, 권한 기능을 활용하였습니다.

Ledgis DID체인은 계정 기반으로 트랜잭션이 발생되며 계정 생성시, 기본적으로 owner, active권한이 계정에 매핑되어 있습니다.

</br>

owner권한은 모든 계정에 대한 권한 계층의 루트에 위치합니다. 따라서 계정에서 권한 구조 내에서 가질 수 있는 가장 높은 상대 권한입니다.

active권한은 owner권한과 관련된 키 변경을 제외하고 트랜잭션을 실행하는데 사용됩니다.

owner, active권한은 계층적인 구조를 가지고 있지만, 구체적인 작업이 필요한 경우 active권한 하위에 커스텀 권한을 생성하여 특정 컨트랙트의 액션과 매핑할 수 있습니다.

</br>

`did:lit` 식별체계에서는 active권한의 자식 권한으로 controller권한, delegator권한을 생성하여 Ledgis DID체인에 등록되는 DID Document를 관리합니다.

새로운 권한을 추가하기 위해서는 updateauth, linkauth를 이용해야합니다.

updateauth를 통해 `controller`, `delegator`권한을 생성합니다.

그리고 linkauth를 통해 lit 컨트랙트 액션을 권한에 링크하여 해당 권한으로 링크된 액션을 실행할 수 있게 설정합니다.

아래는 controller권한에 매핑해야할 lit 컨트랙트의 액션 목록입니다.

```json
[
    "addasserter",
    "addauth",
    "adddelegator",
    "addinvocator",
    "addkeyagrm",
    "addservice",
    "changectrl",
    "clearvcs",
    "deletedid",
    "regdid",
    "regvcs",  
    "rmasserter",
    "rmauth",
    "rmdelegator",
    "rminvocator",
    "rmkeyagrm",
    "rmservice",
    "rmvcs", 
    "updatekeys",
    "updatevcs", 
];
```

</br>

아래는 delegator권한에 매핑해야할 lit 컨트랙트의 액션 목록입니다.

```json
[
    "addinvocator"
    "rminvocator"
];
```

</br>

controller, delegator권한을 추가한 계정은 아래와 같이 보여집니다.

```
user permissions: 
    owner        1:    1 <Owner permission public key value>
        active       1:    1 <Active permission public key value>
            controller   1:    1 <Controller permission public key value>
                delegator    1:    1 <User's controller permission >
```

</br>

예시:

didtesttest1 user permission

```
created: 2021-03-16T08:08:30.000
permissions:
     owner          3:    1 
     EOS6E5Wcw8WJqGu13igZzd4YCGKpuCN7QxjAGPrAdDn7ZbsX23cP7, 1 EOS6JbyJ2fVSKt8F3QWYtczU3mJbni4EC6KTjYezmsZRvJeKX18QJ, 1 EOS7TQHjDHea56GyLYfRy7SfBypm27K5wrC9tLrNvTpFK8U4GH5hc, 1 EOS7c4p2jkWbmkG415RrhukK26PyJhXfhozLwAdSYgzvQwbkUsEY8, 1 EOS8Zwn1my4KusbBLwZue2g4rtm1HcSz7rm8jiSxoW8XFwv7kwMzZ
        active      2:    1 
        EOS5KGrXBQyhSKmxqiZhpgJdZvScAapVNuDf1GHqL3AkVWSvyEf2g, 1 EOS72jo9wE3DKMXy16CNEkRQtfAmqknJUp6JkiKSuwWheFUxjGpNw, 1 EOS7efW6w6b1WKftgZMdsTwwsD9TUuxn6WaVWrQHY5oFKpza5r1k9
           controller       1:    1 
           EOS6ZtXCkzDAf73t6qtq881hFZUUiwhBdP8pbbzhpNyMVBxrftDm7, 1 EOS75W5Gm4aK4LzBjn2uBxM4k56YEC9deboxKyB1g3xvjG7UL1KUP
              delegator     1:    1 didtesttest1@controller
```

</br>

### 2.2.2 Create(Register)

DID Document를 생성하기 위해서는 lit 컨트랙트의 regdid액션을 사용합니다.

regdid액션 실행 결과는 Ledgis DID체인에 저장되는 실제 값입니다.

상호 호환성을 위해 DID Document read작업의 결과는 W3C의 포맷에 맞게 변환하여 반환합니다.

create작업의 결과와 read작업의 결과를 비교해보세요.

</br>

아래는 regdid액션에 입력할 파라미터에 대한 설명입니다.

```
{
    controller: <User Account>,
    uuid : <lit did Identifier>,
    service : [{Service info DID subject is using}]
    verificationMethod: [{List of VerificationMethod}],
    authentication: [{PublicKey Value and Public Key Controller}],
    assertionMethod: [{PublicKey Value and Public Key Controller},
    keyAgreement: [{PublicKey Value and Public Key Controller}],
    capabilityInvocation: [{PublicKey Value and Public KeyController},
    capabilityDelegation: [{PublicKey Value and Public KeyController}]
}
```

</br>

예시

```
{
      controller: 'didtesttestc',
      uuid: '312846759731486237926840657526976805015',
      service: [],
      verificationMethod: [
        ...
        {
          publicKey: 'PUB_K1_7bhWFK2tqeNY2PNbKUE7nSjzeYerNuvLyPMr3Qo1bHKWx2az3a',
          controller: '312846759731486237926840657526976805015'
        },
        ...
      ],
      authentication: [ { uuid: '312846759731486237926840657526976805015', index: 0 } ],
      assertionMethod: [ { uuid: '312846759731486237926840657526976805015', index: 1 } ],
      keyAgreement: [ { uuid: '312846759731486237926840657526976805015', index: 2 } ],
      capabilityInvocation: [],
      capabilityDelegation: [ { uuid: '312846759731486237926840657526976805015', index: 3 } ],
      service: [{
          "id": "did:lit:W4fgrbXRaSURDcjEJ4APcS#ttp",
          "type": "TrustedThirdPartyVerificationVersion1.0Service",
          "endpoint": "https://ttp.crosscheck.com/blahblah"
        }
      ],
      createdAt: 1615462292,
      updatedAt: 1615520431
      
    }
```

</br>

### 2.2.3 Read

누구나 DID Universal Resolver을 통해 `did:lit` 식별자를 조회할 수 있습니다.

아래의 결과에 따라 input값을 주어야합니다. 

```
endpoint: /universal resolver
input: {DID}
output: {DID Document}
```

</br>

예시:

```json
input: did:lit:AEZ87t1bi5bRxmVh3ksMUi
output : 
{
  "@context": "https://www.w3.org/ns/did/v1",
  "id": "did:lit:AEZ87t1bi5bRxmVh3ksMUi",
  "controller": "didtesttest1",
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
  "createdAt": "2021-03-17T07:05:14+00:00",
  "updatedAt": "2021-03-17T07:05:14+00:00"
}
```



</br>

### 2.2.4 Update

`did:lit` 식별체계에서 update는 DID Document의 속성값 각각에 대한 update액션을 제공합니다.

</br>

### controller 

 `controller` 을 수정할 경우,  `changectrl` 액션을 사용합니다.

```
contract : lit
action : changectrl
input : {
    "from" :  <Current Account Value of Controller in DID Document>
    "to" : <Account Value to be updated>
    "uuid" : <lit did Identifier>,
}
```

</br></br>

### verificationMethod

 `verificationMethod` 을 수정할 경우,  `updatekeys` 액션을 사용합니다.

```
contract : lit
action : updatekeys
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "verificationMethod" : <VerificaionMethod Value in array>
}
```

</br></br>

### authentication

 `authentication` 항목을 추가할 경우, `addauth` 액션을 사용합니다.

```
contract : lit
action : addauth
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "authenticator" : <Value of new authentication to add in DID Document>
}
```

</br>

 `authentication` 항목을 삭제할 경우,  `rmauth` 액션을 사용합니다.

```
contract : lit
action : rmauth
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "authenticator" : <Value of authentication to remove from DID Document>
}
```

</br></br>

### assertionMethod

 `assertionMethod` 항목을 추가할 경우,  `addasserter` 액션을 사용합니다.

```
contract : lit
action : addasserter
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "asserter" : <Value of new assertionMethod to add in DID Document>
}
```

</br>

 `assertionMethod` 항목을 삭제할 경우,  `rmasserter` 액션을 사용합니다.

```
contract : lit
action : rmasserter
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "asserter" : <Value of assertionMethod to remove from DID Document>
}
```

</br></br>

### keyagreement

 `keyAgreement` 항목을 추가할 경우,  `addkeyagrm` 액션을 사용합니다.

```
contract : lit
action : addkeyagrm
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "keyAgreement" : <Value of new keyAgreement to add in DID Document>
}
```

</br>

 `keyAgreement` 항목을 삭제할 경우,  `rmkeyagrm` 액션을 사용합니다.

```
contract : lit
action : rmkeyagrm
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "keyAgreement" : <Value of keyAgreement to remove from DID Document>
}
```

</br></br>

#### capabilityDelegation

`capabilityDelegation` 항목을 추가할 경우,  `adddelegator` 액션을 사용합니다.

```
contract : lit
action : adddelegator
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "capabilityDelegator" : <Value of new capabilityDelegation to add in DID Document>
}
```

</br>

 `capabilityDelegation` 항목을 삭제할 경우,  `rmdelegator` 액션을 사용합니다.

```
contract : lit
action : rmdelegator
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "capabilityDelegator" : <Value of capabilityDelegation to remove from DID Document>
}
```

</br></br>

#### capabiltiyInvocation

`capabiltiyInvocation` 항목을 추가할 경우, `addinvocator` 액션을 사용합니다.

```
contract : lit
action : addinvocator
input : {
    "uuid" : <lit did Identifier>
    "delegator" : <Current capabiltiyDelegation Key information in DID Document>
    "signature" : <Signature of delegator using key index in verificationMethod>
    "capabilityInvocator" : <Value of new capabiltiyInvocation to add in DID Document>
}
```

</br>

 `capabiltiyInvocation` 항목을 삭제할 경우,  `rminvocator` 액션을 사용합니다.

```
contract : lit
action : rminvocator
input : {
    "uuid" : <lit did Identifier>
    "delegator" : <Current capabiltiyDelegation Key information in DID Document>
    "signature" : <Signature of delegator using key index in verificationMethod>
    "capabilityInvocator" : <Value of capabiltiyInvocation to remove from DID Document>
}
```

</br></br>

#### service

`service` 항목을 추가할 경우, `addservice` 액션을 사용합니다.

```
contract : lit
action : addservice
input : {
    "controller" : <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
}
```

</br>

 `service` 항목을 삭제할 경우, `rmservice` 액션을 사용합니다.

```
contract : lit
action : rmservice
input : {
    "controller" : <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
    "serviceId" : <Service Id to remove>
}
```

</br>

### 2.2.5 Deactivate

DID Document를 Ledgis DID체인에서 삭제(비활성화)하고자 할 경우, `deletedid` 액션을 사용합니다.

```
contract : lit
action : deletedid
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
}
```

</br></br>

## 3. VC Management

`did:lit` 식별체계는 DID Method뿐 아니라 Verifiable Credential의 상태 정보를 관리하는 기능을 제공합니다.

모든 Verifiable Credential에는 고유한 ID가 있습니다. 그리고 모든 Verifiable Credential에는 상태 정보가 있습니다. 이를 관리하기 위해 Ledgis DID체인에서는 Verifiable Credential의 상태 정보 관리 방안을 제공하기로 했습니다. Verifiable Credential의 상태 정보는 유효, 중지, 폐기 등이 있을 수 있습니다. 아래는 Verifiable Credential에 대한 예시입니다.


```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "http://127.0.0.1:3000/Credentials.jsonld#FamilyRelationCredential"
    ],
    "id": "19f92489-ba85-454f-bbb1-7c60c274c9b9",
    "type": ["VerifiableCredential", "FamilyRelationCredential"],
    "issuer": "did:lit:6GZ1RkqMTSxfFuohNTaZfh",
    "issuanceDate": "2020-12-22T11:18:51.483Z",
    "expirationDate": "2020-12-29T11:18:51.483Z",
    "credentialSubject": {
        "@context": [
            "https://www.w3.org/2018/credentials/v1",
            "http://127.0.0.1:3000/Credentials.jsonld#FamilyRelationCredential"
        ],
        "id": "19f92489-ba85-454f-bbb1-7c60c274c9b9",
        "type": ["VerifiableCredential", "FamilyRelationCredential"],
        "issuer": "did:lit:6GZ1RkqMTSxfFuohNTaZfh",
        "issuanceDate": "2020-12-22T11:18:51.483Z",
        "expirationDate": "2020-12-29T11:18:51.483Z",
        "credentialSubject": {
		        "type": "FamilyRelationCredential",	
	          "registerPlace": "서울시 서초구 서초대로 1길 2",
            "subject": {
                "name": "picard",
                "birthDate": "2001-01-10",
                "residentNum": "010110-123",
                "gender": "F"
            },
            "familyRelation": {
                "father": {
                    "name": "DAD",
                    "birthDate": "1900-09-09",
                    "residentNum": "1234-5678",
                    "gender": "M"
                }
            }
        },
        "credentialStatus": {
            "id": "http://127.0.0.1:4000/credentialStatus.json",
            "type": "ibctStatusList2020"
        },
        "credentialSchema": {
            "id": "http://127.0.0.1:3000/credentialSchema.json",
            "type": "JsonSchemaValidator2018"
        }
    },
    "proof": {
        "type": "EcdsaSecp256k1Signature2019",
        "created": "2020-12-22T11:18:52Z",
        "jws": "eyJhbGciOiJFUzI1NksiLCJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdfQ..MEQCIHgBrdBfzY0Jrm2p4NKBWdCjrGL589HXb2BWyVrQujJIAiBEmyd6fqfLfunxnVm_-2QLVY_03hNVDoIKPCGzQ8X45Q",
        "proofPurpose": "assertionMethod",
        "verificationMethod": "did:lit:6GZ1RkqMTSxfFuohNTaZfh#0"
    }
}
```

</br>

### 3.1 Register VC-id Status


특정 Verifiable Credential의 상태정보를 등록하려면 `regvcs` 액션을 사용합니다.

```
contract : lit
action : regvcs
input : {
    "issuer" : <User account who is registering VC status info>
    "vcUuid" : <Id value of Verifiable Credential>
    "vcStatus" : <Status Info of Verifiable Crednetial>
    "expiredAt": <ExpireDate of Verifiable Credential>
}
```

</br>

### 3.2 Update VC-id Status

특정 Verifiable Credential의 상태정보를 수정하려면 `updatevcs` 액션을 사용합니다.

```
contract : lit
action : updatevcs
input : {
    "issuer" : <User account who is updating specific VC status info>
    "vcUuid" : <Id value of Verifiable Credential>
    "vcStatus" : <Status Info of Verifiable Crednetial>
    "expiredAt": <ExpireDate of Verifiable Credential>
}
```

</br>

### 3.3 Remove VC-id Status

특정 Verifiable Credential가 폐기되었다면 블록체인에 등록된 상태 정보를 삭제하기 위해 `rmvcs` 액션을 사용합니다.

```
contract : lit
action : rmvcs
input : {
    "issuer" : <User account who is removing specific VC status info>
    "vcUuid" : <Id value of Verifiable Credential>
}
```

</br>

### 3.4 Clear VC-Status


동일한 사용자가 등록한 특정 Verifiable Credentials 정보를 지우려면 `clearvcs`액션을 사용해야합니다.

```
contract : lit
action : clearvcs
input : {
    "issuer" : <User account who is clearing VCs status info>
}
```

</br></br>

## 4. Security Considerations

`did:lit` 식별체계는 완전한 SSI(Self Sovereign Identity)를 실현하기 위해 설계되었습니다.

DID Document의 접근 통제를 위해 사용자 Ledgis DID체인 계정에 새로운 controller권한, delegator권한을 추가하였습니다.

`did:lit` 식별체계에서 DID Document에 대한 CRUD작업은 DID Document controller값의 계정을 확인하고, 해당 계정에 controller권한이 있는지 확인합니다.

해당 권한이 있는 사용자 계정만 DID Document를 수정할 수 있도록 설계하였습니다.

</br></br>

## 5. Privacy Consideration

Ledgis DID체인은 사용자 프라이버시를 고려하여 PII(Personally-Identifiable Information)없이, DID Document정보, Verifiable Credential의 상태 정보만 등록합니다.

현재 Ledgis DID체인에는 아래 데이터만 저장합니다.

- 개체를 식별하는데 사용되는 DID Document
- Verifiable Credential의 유효성을 관리할 수 있는 상태정보


</br></br>


## References

[1] IBCT, [ibct.kr](http://ibct.kr)

[2] Decentralized Identifiers (DIDs) v1.0, https://www.w3.org/TR/did-core/







