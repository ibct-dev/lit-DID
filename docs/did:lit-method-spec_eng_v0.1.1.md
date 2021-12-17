# LIT DID Method Specification v0.1.1

This is version 0.1.1 of the lit DID Method Specification.

</br>

## Introduction

LEDGIS is a blockchain established by IBCT, which is a combination of two words: LEDGER, which means "ledger" and AEGIS, which means "protection, shield." LEDGIS aims to protect the trust and interests of user by protecting the integrity of the ledger. Based on this, Ledgis DID Chain provides a transparent and cryptographically reliable `did:lit` identification system through a lit contract.

</br>

## Abstract

Ledgis DID Chain is a decentralized network system for self-sovereign identity and verifiable credentials. Ledgis DID Chain is expected to improve the existing online identity problem by using the `did:lit` identification system proposed by IBCT. The LIT DID Method spec contains information about the decentral identifier and credential status management operating in the Ledgis DID chain.

</br>

## Status Of this document

This is a draft document is based on W3C Standard and will be updated.

</br></br>

## 1. lit DID

LIT in the `did:lit` identification system stands for LEDGIS identity transformation. Its a decentralized identification system developed to provide a method to uniquely identify a person, organization or device without a central authority. The `did:lit` identification system follows the W3C standard for the DID Method. This document defines how to create, update, and cancel the `lit` identification DID and DID Document, and how to manage the status information of Verifiable Credential.

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

Example

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

The name string identifying the lit DID method is `lit`. Identifiers using the `did:lit` identification scheme must start with the `did:lit` prefix. The values after the prefix are described in the remaining sections below.

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

All `did:lit` identifiers are base58 encoded with 16 bytes of uuid alphabet. `did:lit` identifier use base58 to avoid readability issues for 0, O, I, l characters.

</br>

A convenient regex to match `did:lit` identifier is:

```txt
^[1-9A-HJ-NP-Za-km-z]{21,22}$
```

</br>

A convenient regex to match the entire `did:lit:IDENTIFIER` string is:

```txt
^(did:lit:(?:[1-9A-HJ-NP-Za-km-z]{21,22}))$
```

</br>

A valid did might be `did:lit:AEZ87t1bi5bRxmVh3ksMUi`.

</br>

### 1.3 did system contract

</br>

Ledgis DID chain is based on account and authority. When a user creates an account, the owner, active authority is created by default. Owner authority is located at the root of the permission hierarchy for all accounts. This is the highest privilege mapped to an account. Active authority are used to execute transactions, except for key changes related to owner authority. The Ledgis DID chain can create additional authorities that meet the purpose of active submissions. Using these accounts, authority, are used to acheive the user's self-sovereign identity (SSI). To this end, all control functions related to `did:lit` were implemented as `led.lit`, which is a system contract of Ledgis DID chain.

</br>

Through led.lit system contract first, create and map controller and delegator authority second, create controller did document third, did document CRUD is available.

</br>

### 1.3.1 account with customized permission

User creates an account and automatically gets controller/delegator authority an controller did document. controller/delegator authority is added using updateauth action. The 'led.lit' contract can be set to run the action linked to the controller and delegate permission using linkauth action. This is useful for querying permissions required to validate action execution permissions. The roles of each authority are as follows.

- controller permission

    CRUD-enabled permissions on did document, which must be verified by the Ledgis DID chain when executing CRUD transactions on did document

- delegator permission

    CRUD-enabled permissions to capabilityInvocation in did document, which must be acknowledged when adding/deleting did to the capability invocation property

</br>

The account with the controller and delegator permissions is shown below.

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

When an account is created in the Ledgis DID chain, the controller did document is created. We wanted to associate the permission to modify did document with the user's account and the controller attribute value of did document. According to the W3C standard, the controller attribute value must meet the did regular expression. However, the account of Ledgis DID chain does not satisfy the 'did:lit' regular formula. Therefore, we created a controller did document to link the user account with the controller attribute value. The table that maps the controller did to the user account is specified in the controller table.

The controller DID document has only id, controller separate key set(verificationMethod). Map the id value of the controller did document to the user account and record it in the Ledgis DID chain. If the user wants to modify his or her DID Document, the node looks up the controller value in the DID Document in the controller table. CRUD of DID Document is performed through controller permissions or deregator permissions checks of mapped accounts.

</br>

controller DID document example

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
See section2


</br></br>

## 2. DID Document CRUD Operation

</br>

The actions of the 'led.lit' contract that performs CRUD on DID Document are as follows.

</br>

DID document CRUD action

```json
[
    "deletedid",
    "regdid",
]
```

</br>

verification method CRUD action

```json
[
    "updatekeys",   
]
```

</br>

controller CRUD action

```json
[
    "changectrl",
]
```

</br>

verification relationship CRUD action

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

service CRUD action

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

To create a DID Document, use the regdid action of the lit contract. The result of regdid action is the actual did document data stored in the Ledgis DID chain. For interoperability, the results of the DID Document read operation are converted and returned to the format of W3C. It can be confirmed that the result of the create operation and the result of the read operation are different.

</br>

Below is a description of the parameters required for `regdid` action.

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

regdid param example

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

Use the `deletedid` action to delete (disable) DID Document from the Ledgis DID chain.

```txt
contract : led.lit
action : deletedid
input : {
    "controller" :  <current controller uuid value in DID Document>,
    "uuid" : <lit did Identifier>
}
```

</br>

deletedid param exapmle

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

When modifying 'controller', use the `changectrl` action.

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

changectrl param example

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

When modifying 'verificationMethod', use the `updatekeys` action.

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

updatekeys param example

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

verification relationship has `authentication`, `assertionMethod`, `keyAgreement`, `capabilityDelegation`, `capabiltiyInvoctaion` attributes. To CRUD other attributes you should use different action but the parameters entered are the same, except for `capability Invocation`. Add/removing of verificaion relationship attributes can be performed as below. The following example is adding and removing `authentication` attribute. Remind verification relationship attributes(except for `capabiltiyInvocation`) use controller permission for executing transactions.

- authentication - addauth, rmauth

- assertionMethod - addasserter, rmasserter

- keyAgreement - addkeyagrm, rmkeyagrm

- capablityDelegation - adddelegator, rmdelegator

</br>

### 2.4.1 authentication update

</br>

When adding authentication, use the `addauth` action

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

addauth param example

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "authenticator": { "uuid": "99394650071860096581833102200703088599", "index": 0 }
}
```

</br>
</br>

When removing authentication, use the `rmauth` action

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

rmauth param example

```json
{
    "controller": "317158017176121438146673224759223206864",
    "uuid": "99394650071860096581833102200703088599",
    "authenticator": { "uuid": "99394650071860096581833102200703088599", "index": 0 }
}
```

</br></br>

### 2.4.2 capabilityInvocation udpate

Add/delete capability Invocation uses the user account's delegate permission to execute transactions. When adding capabiltiyInvocation, use the `addinvocator` action.

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

addinvocator param example

```json
{
    "delegator": { "uuid": "317158017176121438146673224759223206864", "index": 15 },
    "signature": "SIG_K1_K86rnAkBqcWFT2XoUNrhXdyoc3gdajLN6y4RmCb1mqSj3W4Q6TtRgQL5PWwvdBAdLjKha3ZK3DLzYLWDTVvuXQW87McvKT",
    "capabilityInvocator": { "uuid": "273181167325615934766063315144949048995", "index": 9 },
    "uuid": "99394650071860096581833102200703088599"
}
```

</br>

When adding capabiltiyInvocation, use the `rminvocator` action.

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

rminvocator param example

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

When adding service, use the `addservice` action.

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

addservice param exapmle

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

  When removing service, use the `rmservice` action.

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

rmservice param example

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

You can resolve `did:lit` identifier through DID Universal Resolver

```txt
endpoint: /universal resolver
input: {DID}
output: {DID Document}
```

</br>

example:

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

Lit did method provides a function to manage status information of "Verifiable Credential" as well as "did method". Every Verifiable Credential has its own id. And every Verifiable Credential has an status information. To manage this, we decided Ledgis DID Chain should provide a way to manage status information. Verifiable Credential's status information could be valid, suspended, or discarded. Below is an example of Verifiable Credential.

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

Use the `regvcs` action to register status information for a particular Verifiable Credential.

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

regvcs param example

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

updatevcs param example

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

Use the `rmvcs` action to remove status information for a discarded Verifiable Credential.

```txt
contract : led.lit
action : rmvcs
input : {
    "issuer" : <user account who is removing specific VC status info>,
    "vcUuid" : <id value of Verifiable Credential>
}
```

</br>

rmvcs param exapmle

```json
{
    "issuer": "test3",
    "vcUuid": "62677297661723981814102856366482868005"
}
```

</br></br>

### 3.4 Clear VC-Status

The `clearvcs` action should be used to clear certain Verifiable Credentials information registered by the same user.

```txt
contract : led.lit
action : clearvcs
input : {
    "issuer" : <user account who is clearing VCs status info>
}
```

</br>

rmvcs param example

```json
{
    "issuer": "test3"
}
```

</br></br>

## 4. Security Considerations

The `did:lit` identification system is designed to acheive full SSI(Self Sovereign Identity). In order to control DID Documents, new permissions(controller, delegator) have been added to the user's Ledgis DID chain account. In the 'did:lit' identification system, CRUD operations on DID Document check the account of the DID Document controller value and verify that the account has controller permission. It is designed so that only user accounts with the appropriate permision can modify DID Documents.

</br></br>

## 5. Privacy Consideration

Ledgis DID Chain only registers DID Document information and Verifiable Credential status information without PII (Personally-Identifiable Information) in consideration of user privacy.

Currently, only the following data is stored in the Ledgis DID chain.

- DID Docuemnt, for identifying an entity
- Verifiable Credential status info, for VC validity management

</br></br>

## References

[1] IBCT, [Ledgis.io](https://www.ledgis.io/)

[2] Decentralized Identifiers (DIDs) v1.0, [W3C did-core](https://www.w3.org/TR/did-core/)