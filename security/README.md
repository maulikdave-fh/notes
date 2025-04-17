## Objective
Notes on my understanding of application security concepts & practices.

## Impact of Security Vulnerability
Security vulnerability impacts availability, integrity and confidentiality of data.

## Security Controls
### Preventive 
1. PCI-DSS Requirements - Secure data in transit and data at rest by securing networks, systems and apps. PCI-DSS has 6 Goals -> 12 Requirements -> 400+ controls.
2. Shift Security Left - Secure by design, secure coding practices - OWASP (Open Web Application Security Project), CI pipeline with static / dynamic code analysis, code reviews, penetration testing.  
   
### Detective 
1. Intrusion Detection & Alerts - comprehensive observability implementation.
   
### Corrective
1. Incident Response
2. Data Recovery
3. Post-incident Analysis

## Design & Development Practices
### Secure Coding
#### Input validation
Never trust user provided data or data coming from other apps / services. 
1. Input data validations on type, length, limits.
2. Rate Limiting / Throttling - In microservices architecture, API gateway can be leveraged for this
3. Schema based validations
4. White-listing over black-listing

#### Miscellaneous
1. SQL Injection (```%;UPDATE PRODUCT set price=0--```) - Use ```PreparedStatement``` with parameterized query. JPA's Hibernate implementation is safe.
2. Password - Hashing + Password specific salt	+ work factor (delay factor) using BCrypt , Scrypt, PBKDF2, Argon2. Avoid MD5, SHA
3. Encryption - Use AES with 128/256 bits key, secure mode for Symmetric Key Cryptography
4. File Upload - file name sanitization for path traversal - ensure that it is uploaded to intended directory, check file extension, check file content for allowed type, Minimal access rights on upload directory
5. Use Random Pseudo number generator for session ids, unique ids - sequential ids are more predictable and prone to enumerating attack
6. OWASP's Java encoder
7. XML Parsing - For XMLs coming from third party services. In XMLReader, use correct feature settings - disable doc types, disable external entities
8. YAML - Use SnakeYaml2.x with Spring.

#### Usage of Third-party Libs / Frameworks
1. Review for vulnerablities
2. Use right security alogrithms with correct configurations

### Secure By Design
1. Zero Trust - Validate every request, validate all data entering your system
2. Principle of Least Privillege - Clarity on roles and privilleges, allow access for minimal period needed
3. Defence in Depth - Multiple inter-related security measures to secure the system - no single point of failure. Multiple levels of security: Transport, Network, Infrastructure, OS, Application. For example, ID&V, MFA, Firewalls, Malware detection, ACL, Access Scanning, Cryptography for securing data, Backup & recovery, etc.
4. Fail safe - Murphy's law. If something fails, it should fail in a secured position. For example; if firewall fails, instead of allowing traffic, it should deny all traffic - valid & invalid both.
5. KISS - More complex the system, more difficult to secure. Openness of design - easier to identify and fix security flaws, follow security standards
6. SRP - Without SRP, one vulnerable service can make the entire system vulenrable.
7. Segmentation - Provides isolation. Helps reduce the blast radius. E.g.; In cloud, zones can have exclusive power, cooling and network services.
8. Minimize Attack Surface - Limit external interfaces, Limit Remote Access, Limit IPs, Limit No. of Components. Minimize entry points to the system - security filters
9. Secure By Default - Reduce attack surface, Change default passwords, Change default admin ids

### API Security
1. Minimize exposed APIs / services - helps reduce security exposure
2. Use https - prevents eavesdropping, man-in-middle attacks. Provides authentication, encryption and integrity.
3. OAuth2 + OIDC (OpenID Connect) - OAuth 2.0 and OpenID Connect (OIDC) are crucial for securing APIs by providing robust authentication and authorization mechanisms. While OAuth 2.0 focuses on delegated authorization, OIDC extends it to include user identity verification, enabling single sign-on and secure access to APIs
4. Leveled API keys + Key rotation - Read only, write key, admin key, etc. Helps reduce security vulnerability blast radius
5. Authorization - Role based access control
6. Rate limiting / Throttling - Protects against DOS attack. Provides security & helps improve performance & availability.
7. Allowed List (White-listing) - Can be on allowed IPs, User roles, User Ids, API keys. Everything else is Denied by Default
8. Check OWASP API security risks
9. Use API Gateway - Helps centralized implementation of security aspects - rate limiting, authentication, monitoring, logging
10. Error Handling - Descriptive error messages without any sensitive information. No stack-traces. Use appropriate HTTP status codes
11. Input validation - Validate request parameters, headers and payloads to prevent SQL injection, Cross-site Scripting attacks

## Tools & Frameworks
1. Snyk: Dependency vulnerability scanning
2. SonarQube: Static code analysis
3. Fortify: Static code analysis
4. Veracode: Comprehensive application security testing
5. Aqua Security: Container image scanning
6. Checkmarx: IaC (Infrastructure as Code) security scanning
7. Burp Suite: API security testing 
8. Maven Dependency Check plugin - https://mvnrepository.com/artifact/org.owasp/dependency-check-maven/7.1.0
9. ZAP (Zed Attack Proxy) - Open source tool to identify vulnerabilities during testing phase
10. Spring Security

## JWT (JSON Web Token)
1. Open, industry standard for representing claims securly between two parties. It can contains user details and authorizatins
2. Secure way of transmitting information between 2 parties in stateless manner - unlike session token where subsequent requests to server with a session token has to land on the same server that issued the session token. JWTs are ideal for distributed systems.
3. User is authenticated once, issued a JWT that contains information like user role. The JWT can be sent to APIs & APIs can authorize the user for granting access. Helps reduce a load on authentication server.
4. PKI is used - private key to sign the JWT and public key to verify the JWT
5. JWT has
- Return address - tells who sent the token
- Payload - contains claims (Registered claims & Custom claims) 
- JWT Wax seal - Signature of JWT to make the JWT temper-proof
6. Registered claims - has JWT issuer details, JWT subject details (id), Audience for the JWT (API endpoint), Expiry, Issue time
7. Custom claims - you can have entities like role or any other custom data that may help authenticate and authorize user
8. JWT is signed and encoded. No sensitive information should be part of JWT.

### JWT Format
<table>
   <tr><th>HEADER - ALGORITHMS & TOKEN TYPE</th></tr>
   <tr><td>Type: JWT<br/>Hashing Algo: HS512</td></tr>
<tr><th>PAYLOAD - DATA</th></tr>
   <tr><td><b>Standard Attributes:</b> <br/><li>iss: Token issuer</li><li>sub: Subject - whom this toke is about</li><li>aud - Intended Audience</li><li>exp: Expiry Date</li><li>iat: When was token issued</li><p></p><b>Custom Attributes:</b><br><li>yourattr1: Your custom attribute 1</li></td></tr>
   <tr><th>SIGNATURE - FOR VERIFICATION</th></tr>
   <tr><td>HMACSHA256(Base64(HEADER) + "." + Base64(PAYLOAD), your-256-bit-secret)<br/>Includes a secret</td></tr>   
</table>

### High Level JWT Flow
#### Create a JWT
1. Needs encoding - User credentials, user data (payload), RSA key pair

#### Send JWT 
JWT is sent as part of request header ```Authorization: Bearer ${JWT}```

#### Verify JWT
1. Needs decoding
2. RSA key pair (public key)

## OAuth2.0 Authorization Framework - For Delegated Access
1. OAuth 2.0 is a protocol that allows users to grant third-party applications access to their resources without sharing their credentials. It uses access tokens to authorize API requests, allowing clients to access protected resources. It focuses on granting access to resources, not verifying user identity.
2. Profiles of access tokens: Identifier-based (Holder of Key - like credit card - reference token) and Self-contained (Bearer - like cash - value token). Self-contained access tokens are easy to scale with distributed applications as they do not require the resource server to validate the token with the authorization server. On the other hand, an Identifier-based token is a hard-to-guess string, which the resource server needs to validate by making a call to the authorisation server's introspection endpoint, which adds latency and makes it difficult to scale with distributed applications. 
3. OAuth2.0 Flows - multiple flows - use based on system architecture

## OIDC (OpenID Connect) - Identity Layer
1. OIDC builds upon OAuth 2.0 by adding an identity layer, enabling clients to verify user identity. It uses ID tokens to authenticate users, allowing applications to determine who the user is without storing credentials. OIDC facilitates single sign-on (SSO), allowing users to log in once and access multiple applications.

## How they work together?
1. User Authentication: The user logs in with their credentials to an Identity Provider (IdP) that supports OIDC. The user can be a system / service, and credentials can be a device fingerprint.
2. ID Token Issuance: The IdP issues an ID token to the client, containing information about the user's identity.
3. Access Token Request: The client uses the ID token to request an access token from the authorization server, which is an OAuth 2.0 server.
4. Access Token Grant: The authorization server verifies the ID token and, if valid, issues an access token to the client, granting access to the protected API resources. Authorization server may also issue Refresh Token - Client can use it to request new access tokens.
5. API Access: The client uses the access token to make requests to the API, and the API server validates the token to ensure the user is authorized to access the requested resources

Access token is for API. Id token is for client. JWT can be used as tokens.

## Payment App Considerations
1. Better to use GUID based token (reference token) to pass around that contains a reference to the identity instead of value token (that contains identity and other details). I.e.; on authentication, identify provider generates GUID, stores it on server along side user record and shares this reference token as access token to the client.
2. In microservice architecture, API gateway sends the reference token to authorization server and receives back the value token. The value token is passed to individual microservice - that way, each microservice doesn't have to make a call to authorization server - micorservice can verify the token by verifying the signature of the token using authorization server public key.

## Encoding vs. Hashing vs. Encryption
<table>
   <tr><th>Process</th><th>Description</th><th>Is Reversible</th><th>Usecases</th><th>Examples</th></tr>
   <tr><th>Encoding</th><td>Transform data - one form to another.<br/>Doesn't use a key / password<br/>Not used to secure data</td><td>Yes</td><td>Compression, Streaming, Data Storage</td><td>Base64, MP3</td></tr>
   <tr><th>Hashing</th><td>Convert data into hash<br/>Doesn't use a key / password<br/>One way - not reversible</td><td>No</td><td>Validate integrity of data, Password storage</td><td>Bcrypt, Argon2</td></tr>
   <tr><th>Encryption</th><td>Encoding data using key/password.<br/>Need key to decrypt<td>Yes</td><td>Securing data</td><td>RSA</td></tr>
</table>

