# Verified Public Keys

Public keys that I've verified out-of-band for popular Java software.

## Why

Gradle has dependency verification. 
It can check checksums of artifacts so that you can tell they haven't been tampered with.
You might care about that to make sure that dependencies don't change between subsequent builds -- like if you build on your dev machine by pulling from Maven Central, but your CI/CD system pulls from a cache. 
You'd probably like to fail that build if the checksums don't match. 
Maybe someone poisoned the cache!
Checksums are great for this. 

Gradle can _also_ verify signatures. 
You can make sure that the artifact you downloaded was signed by the authors of the software. 
If you do that, you don't have to trust Maven Central or your cache. 
You raise the bar for an attacker, so that they have to get access to the private signing key, not just upload access to (e.g.) Maven Central. 

Gradle will automatically pull public keys from well-known public key servers. 
I trust those servers.
I trust that they didn't alter a key that was uploaded, delete a key that shouldn't have been deleted, etc.
But I don't trust -- I _can't_ trust -- that the public key I pulled from their server wasn't uploaded by the attacker.
In this threat scenario, it's the same attacker who got access to upload artifacts to Maven Central. 
They upload their malicious artifact, sign it with a brand new key, naming it something that looks official, and now if I only trust the keys that Gradle downloaded then I'm in a bind.
It's signed but by who? 

The way out of this problem is to verify the keys out-of-band. 
While I'm setting things up, and Gradle pulled down all the signing keys, I need to cross check every single one of them with a public source that is controlled by the authors and isn't the same place I downloaded the artifact from. 
There are some customary places to keep these keys, like a file named `KEYS` in the root of the source code repository, but others are not so easy to find. 

Since it's a pain in the ass to find, I don't want to repeat this work every. 
So I'm writing it down for all. 
Don't copy-paste the public keys from this page. 
I have them here so you could maybe get this page if you Google the fingerprint that Gradle gave you and use that to find the public link. 

## Keys

| Organization        | Fingerprint                              | Public URL |
| ------------------- | ---------------------------------------- | ---------- |
| Apache Commmons     | &lt;many&gt;                             | https://downloads.apache.org/commons/KEYS |
| Apache log4j 2      | &lt;many&gt;                             | https://downloads.apache.org/logging/KEYS | 
| Groovy              | &lt;many&gt;                             | https://downloads.apache.org/groovy/KEYS | 
| Jackson (FasterXML) | 28118C070CB22A0175A2E8D43D12CA2AC19F3181 | https://github.com/FasterXML/jackson/blob/master/KEYS | 
| Jetty               | &lt;many&gt;                             | https://github.com/jetty/jetty.project/blob/jetty-12.0.x/KEYS.txt
| JUnit               | FF6E2C001948C5F2F38B0CC385911F425EC61B51 | https://github.com/junit-team/junit5/blob/main/KEYS | 
| Kotlin (JetBrains?) | 2FBA29D08D2E25EE84C132C30729A0AFF8999A87 | https://kotlinlang.org/docs/security.html |
| Logback             | 60200AC4AE761F1614D6C46766D68DAA073BE985 | https://github.com/qos-ch/logback/blob/master/SECURITY.md | 
| SLF4J               | 60200AC4AE761F1614D6C46766D68DAA073BE985 | https://github.com/qos-ch/slf4j/blob/master/SECURITY.md | 
| Spring              | 48B086A7D843CFA258E83286928FBF39003C0425 | https://spring.io/GPG-KEY-spring.txt |
| Square              | dbd744ace7ade6aa50dd591f66b50994442d2d40 | https://square.github.io/okhttp/security/security/#verifying-artifacts |


## Special Cases

### Byte Buddy

There is a link on both https://bytebuddy.net/ and https://github.com/raphw/byte-buddy/blob/master/README.md which points to https://keys.openpgp.org/search?q=rafael.wth@gmail.com 
Now, unfortunately that is a search by e-mail so I'm not sure if someone else could upload their own with the same email.
But as of today, 2024-03-25, there is only one key at that location: this one https://keys.openpgp.org/vks/v1/by-fingerprint/B4AC8CDC141AF0AE468D16921DA784CCB5C46DD5 
That key also matches the one the author originally posted here on the GitHub Issue https://github.com/raphw/byte-buddy/issues/721#issuecomment-551317008 

This is enough where I would trust that today. But it isn't a simple trustable link I could put above. 

### Gson

Gson is a little special.
With so long between releases, you could do just fine auditing the jar itself and making sure the checksums match. 
I did not find the public key portion of their signing key(s).

## Didn't find

- AssertJ
- Google anything
  - Checked guava, gson, guice. Closest I got was this issue https://github.com/google/guice/issues/1644 but no response. 
- Hamcrest 
- Hibernate
- http4k
- Jacoco
  - Found a GitHub issue but looks like the author just never did it https://github.com/jacoco/jacoco/issues/937 
- jOOQ
- Lombok
- Micrometer
- Micronaut
- Mockito 
  - No confirmation from author, but they're open to it https://github.com/mockito/mockito/issues/2851 
    It's probably 147b691a19097624902f4ea9689cbe64f4bc997f, but again, no confirmation.
- OpenTelemetry


