# INF226 Support Material

[Mandatory 1](mandatory1.md)

## Mandatory 2 :inChat

**NOTE:** (From the [README](https://git.app.uib.no/Hakon.Gylterud/inf226-2020-inchat/)):

```
A note about HTTPS: We assume that inChat will be running
behind a reverse proxy which takes care of HTTPS, so you
can ignore issues related HTTPS.
```

### Setting up and building

```sh
> mvn compile
> mvn test
> mvn exec:java
```

Be sure to have updated Java Development Kit (JDK) and Maven installed

[Oracle Java JDK](https://www.oracle.com/java/technologies/javase-downloads.html#javasejdk)

[Apache Maven](https://maven.apache.org/install.html)

#### Common problems

[Invalid target release](https://dzone.com/articles/how-to-fix-invalid-target-release-17-18-19-or-110)

[No compiler is prodived](http://roufid.com/no-compiler-is-provided-in-this-environment/)

### Authentication

[Key Derivation Functions](https://cryptobook.nakov.com/mac-and-key-derivation/kdf-deriving-key-from-password)

[scrypt](https://cryptobook.nakov.com/mac-and-key-derivation/scrypt)
Note: scrypt is already installed in the project.

[Aregon2](https://cryptobook.nakov.com/mac-and-key-derivation/argon2)

Note: needs to be installed in the project: [argon2 install](https://github.com/phxql/argon2-jvm)

### SQL injection

### Cross-site scripting (XSS)

[OWASP XSS Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

[OWASP Encoder](https://owasp.org/www-project-java-encoder/)

Examples of use, se the `How to`

### Cross-Site Request Forgery (CSRF)

[CWE 352](https://cwe.mitre.org/data/definitions/352.html)

### Access control

### Misc / Articles

[Using HTTP Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)