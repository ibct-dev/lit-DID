# LIT DID Method Specification

</br>

## Abstract

Ledgis DID체인은 자기주권신원 및 검증가능한 자격증명을 위한 분산형 네트워크 시스템입니다.

Ledgis DID체인은 IBCT에서 운영하며 제안하는 `lit` 식별체계를 이용해 기존의 온라인상에서의 아이덴티티 문제를 개선할 수 있을 것으로 예상됩니다.

LIT DID Method spec은 Ledgis DID체인에서 동작하는 탈중앙 식별자 및 자격증명 상태 정보 관리에 대한 내용을 담고있습니다.

</br>

## Status Of this document

이 문서는 W3C 표준을 기반으로 한 초안 문서이며 업데이트 될 예정입니다.

</br></br>

## 1. lit DID



`lit` 식별체계의 lit는 LEDGIS identity transformation의 약어로, 중앙기관 없이 사람, 조직 또는 장치를 고유하게 식별하는 방법을 제공하기 위해 개발된 탈중앙화된 식별체계입니다. 

`lit` DID Method는 W3C 표준을 따릅니다. 이 문서에서는 `lit` 식별 DID 및 DID Document의 생성, 업데이트, 취소 방법 및 Verifiable Credential의 상태 정보 관리에 방안 대해 정의합니다. 

</br>

### 1.1 lit DID Method Name

------

lit DID 메소드를 식별하는 이름 문자열은 `lit` 입니다. `lit` 식별체계를 이용하는 식별자는 `did:lit`접두사로 시작해야 합니다. 접두사 뒤의 값은 나머지 아래 절에서 설명합니다.

</br>

### 1.2 lit DID Format

------

`lit` 식별체계의 식별자는 아래의 형식으로 구성됩니다.

```json
lit-did = "did:lit" + lit-identifier
lit-identifier = 21 * 22 (base58char)
base58char = "1" / "2" / "3" / "4" / "5" / "6" / "7" / "8" / "9" / "A" / "B" / "C"
    / "D" / "E" / "F" / "G" / "H" / "J" / "K" / "L" / "M" / "N" / "P" / "Q"
    / "R" / "S" / "T" / "U" / "V" / "W" / "X" / "Y" / "Z" / "a" / "b" / "c"
    / "d" / "e" / "f" / "g" / "h" / "i" / "j" / "k" / "m" / "n" / "o" / "p"
    / "q" / "r" / "s" / "t" / "u" / "v" / "w" / "x" / "y" / "z"
```

</br>

### 1.2.1 lit-identifier 생성 방법

`did:lit` 식별자는 아래의 규칙에 따라 정의됩니다. 모든 `did:lit` 식별자는 16바이트의 uuid 알파벳을 base58로 인코딩하여 사용합니다. 0, O, I, l 문자에 대한 가독성 문제를 피하기 위해 base58을 사용합니다.

lit-identifier 정규 표현식은 아래와 같습니다.

```
[1-9A-HJ-NP-Za-km-z]{21,22}$
```


lit DID 식별자의 정규 표현식은 아래와 같습니다.

```
did:lit:1-9A-HJ-NP-Za-km-z]{21,22}$
```



유효한 `did:lit` 식별자 DID는 did:lit:X91iGEUwpjraFUoMArHqsZ 같을 수 있습니다.

</br></br>

## 2. DID Document

</br>

### 2.1 DID Document 예

------

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
    "@context": "https://w3id.org/did/v1",
    "did": "did:lit:X91iGEUwpjraFUoMArHqsZ",
    "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
    "authentication": [
        "did:lit:X91iGEUwpjraFUoMArHqsZ#10",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#11",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#12",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#13",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#14",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#15",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#16",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#17",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#18",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#19"
    ],
    "assertionMethod": ["did:lit:X91iGEUwpjraFUoMArHqsZ#10"],
    "capabilityInvocation": [],
    "capabilityDelegation": [],
    "keyAgreement": [],
    "verificationMethod": [
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#10",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "269JzKmDo3DpaoVbnrd5PPthffo82NhvLNSwCRr5kxSkv"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#11",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "2AqvxwvNdw8JUn8Waa9vnNVDX5wgPQrQi7Yk6fR51b4XP"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#12",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "dmm4b6QniiJmv4LyNtyNXXeJymUCUTMNqtSF4uYSYg4n"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#13",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "sLvfD1zvyHm6FX4gqdgMCneVqJ3dSy59HvJzPZoZryZK"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#14",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "25cRC6XkQGLMcW5aVzeJR2EqNte72cwDFmxkaDYgwmekB"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#15",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "vp6yrPD7mpy7EoZuoNRVDcgikt1T7DvmDVH6Cehn4e1f"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#16",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "2BC6g8v56FcApM7cTRAgnYScyhEhPe1kGuEwnSCAmXCrU"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#17",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "sVzieURLMagvrwghtAKyaLDqgm2SYyoCbqFYx99fAxXJ"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#18",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "ykj4PaAhqYCZMwUvKD3F8v1Z8WTMrvGB5NeMp5v2FmK2"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#19",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "zpTJ3agmRef23zVinpRDHTYu5PhacCpUB9aXmLEYrn4q"
        }
    ],
    "service": []
}

```

</br>

## 2.2 CRUD Operation

DID method 명세에는 lit 컨트랙트를 통해 CRUD(Create, Read, Update, Delete)할 수 있는 데이터에 대해 소개하고 작업 과정에 대해 설명합니다.

DID method 명세에는 DID Document 관리를 위해 목적에 맞는 액션에 대해 소개하고자 합니다.

아래에 각 정보의 CRUD방법에 대한 설명입니다.

</br>

### 2.1 Add Permission

------

`did:lit` 식별자는 Ledgis DID체인의 lit 컨트랙트에 의해 관리됩니다. 

SSI를 실현하기 위해 사용자의 DID, DID Document는 사용자가 직접 관리하며 DID Document등록, 수정, 삭제 모두 사용자에 의해 수행됩니다.

이는 사용자 계정에 새로운 `controller`권한과 `delegator`권한을 추가해야 가능합니다.

사용자의 계정에 새로운 권한을 추가하기 위해서는 updateauth, linkauth를 이용해야합니다.

updateauth를 통해 `controller`, `delegator`권한을 생성합니다. 그리고 linkauth를 통해 각 권한에 lit 컨트랙트의 액션을 매핑합니다.

아래는 매핑해야할 lit 컨트랙트의 액션 목록입니다.

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

아래는 controller, delegator권한을 추가한 계정은 아래와 같이 보여집니다.

```
user permissions: 
    owner        1:    1 <Owner permission public key value>
    active       1:    1 <Active permission public key value>
    controller   1:    1 <Controller permission public key value>
    delegator    1:    1 <User's controller permission >
```

</br>

예시:

didtesttestc's user permission

```
didtesttestc permissions: 
    owner           1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    active          1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    controller      1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    delegator       1:    1 didtesttestc@controller
```

</br>

### 2.2 Create(Register)

------

DID Document를 생성하기 위해서는 lit 컨트랙트의 regdid액션을 사용합니다.

`did:lit` 식별체계는 Ledgis DID체인의 자원 문제와 사용자의 SSI를 고려하여 설계하였으며 그에 맞게 최적화하였습니다.

regdid액션 실행 결과는 Ledgis DID체인의 테이블 구조에 저장되는 실제 값입니다.

상호 호환성을 위해 DID Document read작업의 결과는 W3C의 포맷에 맞게 변환하여 반환합니다.

create작업의 결과와 read작업의 결과를 비교해보세요.



lit는 사용자의 SSI(Self-Sovereign Identity)를 실현하기 위해 아래의 속성값을 테이블에 에 등록합니다.

- controller: DID Document 수정 권한이 있는 사용자의 Ledgis DID체인 계정명
- verificatoinMethod.controller : 사용자의 `did:lit` 식별자값의 BigInt() 형 변환, 즉 verificationMethod를 제어하는 did값
- verificationRelationship.uuid : 사용자의 lit identifier 값의 BigInt() 형변환, 즉 verificationRelationship를 제어하는 did값

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

### 2.3 Read

------

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
input: did:lit:X91iGEUwpjraFUoMArHqsZ#15
output : 
{
    "@context": "https://w3id.org/did/v1",
    "id": "did:lit:X91iGEUwpjraFUoMArHqsZ",
    "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
    "authentication": [
        "did:lit:X91iGEUwpjraFUoMArHqsZ#10",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#11",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#12",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#13",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#14",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#15",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#16",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#17",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#18",
        "did:lit:X91iGEUwpjraFUoMArHqsZ#19"
    ],
    "assertionMethod": ["did:lit:X91iGEUwpjraFUoMArHqsZ#10"],
    "capabilityInvocation": [],
    "capabilityDelegation": [],
    "keyAgreement": [],
    "verificationMethod": [
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#10",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "269JzKmDo3DpaoVbnrd5PPthffo82NhvLNSwCRr5kxSkv"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#11",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "2AqvxwvNdw8JUn8Waa9vnNVDX5wgPQrQi7Yk6fR51b4XP"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#12",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "dmm4b6QniiJmv4LyNtyNXXeJymUCUTMNqtSF4uYSYg4n"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#13",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "sLvfD1zvyHm6FX4gqdgMCneVqJ3dSy59HvJzPZoZryZK"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#14",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "25cRC6XkQGLMcW5aVzeJR2EqNte72cwDFmxkaDYgwmekB"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#15",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "vp6yrPD7mpy7EoZuoNRVDcgikt1T7DvmDVH6Cehn4e1f"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#16",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "2BC6g8v56FcApM7cTRAgnYScyhEhPe1kGuEwnSCAmXCrU"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#17",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "sVzieURLMagvrwghtAKyaLDqgm2SYyoCbqFYx99fAxXJ"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#18",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "ykj4PaAhqYCZMwUvKD3F8v1Z8WTMrvGB5NeMp5v2FmK2"
        },
        {
            "id": "did:lit:X91iGEUwpjraFUoMArHqsZ#19",
            "type": "Secp256k1VerificationKey2018",
            "controller": "did:lit:X91iGEUwpjraFUoMArHqsZ",
            "publicKeyBase58": "zpTJ3agmRef23zVinpRDHTYu5PhacCpUB9aXmLEYrn4q"
        }
    ]
}
```



</br>

### 2.4 Update

------

`did:lit` 식별체계에서 update는 DID Document의 속성값 각각에 대한 update액션을 제공합니다.

</br>

### controller 

 `controller` 을 업데이트할 경우,  `changectrl` 액션을 사용합니다.

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

 `verificationMethod` 을 업데이트할 경우,  `updatekeys` 액션을 사용합니다.

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

 `authentication` 을 업데이트할 경우,  `addauth` 액션을 사용합니다.

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

 `assertionMethod` 을 업데이트할 경우,  `addasserter` 액션을 사용합니다.

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

 `keyAgreement` 을 업데이트할 경우,  `addkeyagrm` 액션을 사용합니다.

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

`capabilityDelegation` 을 업데이트할 경우,  `adddelegator` 액션을 사용합니다.

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

`capabiltiyInvocation` 을 업데이트할 경우,  `addinvocator` 액션을 사용합니다.

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

`service` 을 업데이트할 경우,  `addservice` 액션을 사용합니다.

```
contract : lit
action : addservice
input : {
    "controller" : <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
}
```

</br>

 `service` 항목을 삭제할 경우,  `rmservice` 액션을 사용합니다.

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

### 2.5 Deactivate

------

DID Document를 테이블에서 삭제(비활성화)하고자 할 경우,  `deletedid` 액션을 사용합니다.

```
contract : lit
action : rminvocator
input : {
    "controller" :  <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
}
```

</br></br>

## 3. VC Management

`lit` 식별체계는 DID Method뿐 아니라 Verifiable Credential의 상태 정보를 관리하는 기능을 제공합니다.

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

------

특정 Verifiable Credential의 상태정보를 업데이트하려면 `updatevcs` 액션을 사용합니다.

```
contract : lit
action : updatevcs
input : {
    "issuer" : <User account who is registering specific VC status info>
    "vcUuid" : <Id value of Verifiable Credential>
    "vcStatus" : <Status Info of Verifiable Crednetial>
    "expiredAt": <ExpireDate of Verifiable Credential>
}
```

</br>

### 3.3 Remove VC-id Status

------

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

------

To clear specific Verifiable Credentials info which is registerd by same user, you shoud use `clearvcs` action.

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

`lit` 식별체계는 완전한 SSI를 실현하기 위해 설계되었습니다.

Ledgis체인에 등록되는 DID Document는 사용자 키 정보, lit identifier값, 사용자의 Ledgis DID체인 계정을 이용해서 생성됩니다.

DID Document의 접근 통제를 위해 사용자 Ledgis DID체인 계정에 새로운 controller권한, delegator권한을 추가하였습니다. 

Ledgis DID체인에 등록된 DID Document controller값의 계정을 확인하고, 해당 계정에 controller권한이 있는지 확인합니다.

해당 권한이 있는 사용자 계정만 DID Document를 수정할 수 있도록 설계하였습니다.

</br></br>

## 5. Privacy Consideration

Ledgis DID체인은 사용자 프라이버시를 고려하여 PII(Personally-Identifiable Information)없이, DID Document정보, Verifiable Credential의 상태 정보만 등록합니다.

현재 Ledgis DID체인에는 다음 데이터만 저장합니다.

- 개체를 식별하는데 사용되는 DID Document
- Verifiable Credential의 유효성을 관리할 수 있는 상태정보


</br></br>


## References

[1]. IBCT, [ibct.kr](http://ibct.kr)

[2] Decentralized Identifiers (DIDs) v1.0, https://www.w3.org/TR/did-core/







