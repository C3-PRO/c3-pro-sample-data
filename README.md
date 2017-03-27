C3-PRO Sample Resources
=======================

This repository contains 🔥FHIR sample resources, as used by the _C3-PRO_ libraries.

Since FHIR is still evolving there are different versions of the resources:

- the `master` branch contains **STU-3** (v`3.0.0`) resources
- the `develop` branch may contain resources of a newer FHIR version


Questionnaire
-------------

The `Questionnaire` subfolder contains simple questionnaires that demonstrate usage of certain data types with questionnaires.


QuestionnaireResponse
---------------------

Example `QuestionnaireResponse` files with responses to the respective questionnaires.
Usually, those are **encrypted** when going over the wire, see below.


Encryption
----------

C3-PRO uses RSA and AES encryption with _OAEP_ (optimal asymmetric encryption padding), which was standardized in PKCS#1 v2 and uses SHA-1/MGF1 by default.
We use our own simple JSON format to transmit both the RSA-encrypted random AES key as well as the AES-encrypted FHIR resource:

```json
{
    "message": "{{ AES-encrypted fhir resource, base64 encoded }}",
    "symmetric_key": "{{ RSA-encrypted AES key used to encrypt `message`, base64 encoded }}",
    "key_id": "{{ RSA key id used to encrypt `symmetric_key` }}",
    "version": "{{ FHIR version, `dstu2-1.0.2` or `stu3-3.0.0` }}"
}
```

Use of [JWE](http://openid.net/specs/draft-jones-json-web-encryption-02.html) is being discussed.

The `enc` directory contains encryption-related files that can be used for unit testing:

- `private.pem`: private RSA 2048 key
- `public.crt`: the corresponding public RSA key as X509 certificate

### AES

AES encryption uses a 32 bit key by default.
To achieve correct padding these settings can be used on the mobile platforms:

- iOS: `kSecPaddingOAEP`
- Java: `RSA/ECB/OAEPWithSHA1AndMGF1Padding`

### RSA

To follow.

### JWE

To follow.

