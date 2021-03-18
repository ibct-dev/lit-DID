# LIT DID Method Specification

</br>

## Introduction

LEDGIS is a blockchain established by IBCT, which is a combination of two words: LEDGER, which means "ledger" and AEGIS, which means "protection, shield."

LEDGIS aims to protect the trust and interests of user by protecting the integrity of the ledger.

Based on this, Ledgis DID Chain provides a transparent and cryptographically reliable `did:lit` identification system through a lit contract.


</br>

## Abstract

Ledgis DID Chain is a decentralized network system for self-sovereign identity and verifiable credentials.

Ledgis DID Chain is expected to improve the existing online identity problem by using the `did:lit` identification system proposed by IBCT.

The LIT DID Method spec contains information about the de-central identifier and credential status management operating in the Ledgis DID chain.

</br>

## Status Of this document

This is a draft document is based on W3C Standard and will be updated.

</br></br>

## 1. lit DID

LIT in the `did:lit` identification system stands for LEDGIS identity transformation.

Its a decentralized identification system developed to provide a method to uniquely identify a person, organization or device without a central authority.

The `did:lit` identification system follows the W3C standard for the DID Method. 

This document defines how to create, update, and cancel the `lit` identification DID and DID Document, and how to manage the status information of Verifiable Credential.

</br>

### 1.1 lit DID Method Name

The name string identifying the lit DID method is `lit`. 

Identifiers using the `did:lit` identification scheme must start with the `did:lit` prefix. 

The values after the prefix are described in the remaining sections below.

</br>

### 1.2 lit DID Format

The identifier of the `did:lit` identification system is composed of the following format.

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

### 1.2.1 lit-identifier

All `did:lit` identifiers are base58 encoded with 16 bytes of uuid alphabet. 

`did:lit` identifier use base58 to avoid readability issues for 0, O, I, l characters.

</br>

A convenient regex to match `did:lit` identifier is:

```
^[1-9A-HJ-NP-Za-km-z]{21,22}$
```


</br>

A convenient regex to match the entire `did:lit:IDENTIFIER` string is:


```
^(did:lit:(?:[1-9A-HJ-NP-Za-km-z]{21,22}))$
```

</br>


A valid did DID might be `did:lit:AEZ87t1bi5bRxmVh3ksMUi`.


</br></br>

## 2. DID Document

</br>

### 2.1 DID Document 예시

The `did:lit` DID Document contains the following property values:

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

example

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

The DID method specification introduces the data that can be CRUD (Create, Read, Update, Delete) through the lit contract, and explains the working process.

In the DID method specification, we would like to introduce actions that fits the purpose of managing DID Documents.

Below is an explanation of how to CRUD each property.

</br>

### 2.2.1 Add Permission

The `did:lit` identifier is managed by the lit contract of the Ledgis DID chain.

To acheive SSI(Self Sovereign Identity), the user's DID and DID document should be managed by the user.

DID document registration, modification, and deletion are all performed by the user.

For this purpose, the `did:lit` identification system utilized the account and permission concept of the Ledgis DID chain.

The Ledgis DID chain generates account-based transactions and, by default, owner, active permissions are mapped to the account when it is created.

</br>

An account is a human-readable name that is stored on the blockchain. An account is required to transfer or push any valid transaction to the blockchain. Every account has two default named permissions when created, owner and active.

The owner permission sits at the root of the permission hierarchy for every account. It is therefore the highest relative permission an account can have within its permission structure. 

The active permission is typically used for executing transactions, exepct changing the keys associated with the owner.

They have a parent-child relationship by default, but for more specific actions, custom permissions are typically created below the active permission and mapped to specific contracts or actions.

</br>

In the `did:lit` identification system, controller and delegator permissions are created as a child of active permission.

Theses custom permissions are created to manage DID documents registered in the Ledgis DID chain.

Updateauth and linkauth must be used to add new permission.

Create `controller` and `delegator` permission through updateauth action.

In addition, the lit contract action is linked to the permission through linkauth action, and the linked action can be executed with that permission.

And linkauth links lit contract actions to permissions to enable them to execute linked actions.

Below is a list of actions that should be mapped to controller permission.

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

Below is a list of actions that should be mapped to delegator permission.

```json
[
    "addinvocator"
    "rminvocator"
];
```

</br>

Account that has added controller and delegator permission is shown below.

```
user permissions: 
    owner        1:    1 <Owner permission public key value>
        active       1:    1 <Active permission public key value>
            controller   1:    1 <Controller permission public key value>
                delegator    1:    1 <User's controller permission >
```

</br>

example

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

To create a DID Document, use the regdid action of lit contract.

The result of executing the regdid action is the actual value stored in the Ledgis DID chain.

For compatibility, the result of DID Document read operation is converted and returned to the format of W3C.

Compare the result of create operation with the result of read operation.

</br>

Below is the parameters for regdid action.

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

example

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

A `did:lit` DID can be looked up through DID Universal Resolver.

Input value should be given to resolve the result below.

```
endpoint: /universal resolver
input: {DID}
output: {DID Document}
```

</br>

example

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

`did:lit` identification system, provides an update action for each attribute value of DID Document.

</br>

### controller 

To modify `controller` property, use the `changectrl` action.

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

To modify `verificationMethod` property, use the `updatekeys` action.

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

To add an specific `authentication`, use the `addauth` action.

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

To delete an specific `authentication`, use the `rmauth` action.

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

To add an specific `assertionMethod`, use the `addasserter` action.

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

To delete an specific `assertionMethod`, use the `rmasserter` action.


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

To add an specific `keyAgreement`, use the `addkeyagrm` action.

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

To delete an specific `keyAgreement`, use the `rmkeyagrm` action.

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

To add an specific `capabilityDelegation`, use the `adddelegator` action.

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

To delete an specific `capabilityDelegation`, use the `rmdelegator` action.


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

To add an specific `capabiltiyInvocation`, use the `addinvocator` action.

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

To delete an specific `capabiltiyInvocation`, use the `rminvocator` action.
 

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

To add an specific `service` property, use the `addservice` action.


```
contract : lit
action : addservice
input : {
    "controller" : <Current Controller Value of Account in DID Document>
    "uuid" : <lit did Identifier>
}
```

</br>

To delete an specific `service`, use the `rmservice` action.

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

To delete(or deactivate) a DID Document from the Ledgis DID chain, use the `deletedid` action.

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


Lit did method provides a function to manage status information of "Verifiable Credential" as well as "did method".

Every Verifiable Credential has its own id.

And every Verifiable Credential has an status information.

To manage this, we decided Ledgis DID Chain should provide a way to manage the status information.

Verifiable Credential's status information may be valid, suspended, or discarded.

Below is an example of Verifiable Credential.

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

To register the status information of a specific Verifiable Credential, use `regvcs` action.

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

To update the status information of a specific Verifiable Credential, use `updatevcs` action.

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

If a specific Verifiable Credential has been revoked, the `rmvcs` action is used to delete the state information registered in the blockchain.

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

If you want to clear specific Verifiable Credentials information registered by the same user, you need to use the `clearvcs` action.

```
contract : lit
action : clearvcs
input : {
    "issuer" : <User account who is clearing VCs status info>
}
```

</br></br>

## 4. Security Considerations

The `did:lit` identification system is designed to acheive full SSI(self sovereign identity).

In order to control DID Documents, new permissions(controller, delegator) have been added to the user's Ledgis DID chain account.

In the 'did:lit' identification system, CRUD operations on DID Document check the account of the DID Document controller value and verify that the account has controller permission.

It is designed so that only user accounts with the appropriate permision can modify DID Documents.

</br></br>

## 5. Privacy Consideration

Ledgis DID Chain only registers DID Document information and Verifiable Credential status information without PII (Personally-Identifiable Information) in consideration of user privacy.

Currently, only the following data is stored in the Ledgis DID chain.

- DID Docuemnt, for identifying an entity
- Verifiable Credential status info, for VC validity management


</br></br>


## References

[1] IBCT, [ibct.kr](http://ibct.kr)

[2] Decentralized Identifiers (DIDs) v1.0, https://www.w3.org/TR/did-core/







