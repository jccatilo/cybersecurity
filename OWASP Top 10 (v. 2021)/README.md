# About OWASP

The Open Web Application Security Project (OWASP) is an open community dedicated to enabling organizations to develop, purchase, and maintain applications and APIs that can be trusted.

Learn more at: [https://www.owasp.org](https://www.owasp.org).

## OWASP V.2017 vs OWASP V.2021

![OWASP V.2017 vs OWASP V.2021](img/1_2017vs2021.png)

Learn more at: [https://owasp.org/Top10/A00_2021_Introduction/](https://owasp.org/Top10/A00_2021_Introduction/)

## OWASP Top 10 V.2021 (my summary)

**1. Broken Access Control**

- This is when a user can see things he shouldn't on an app or a website.
- Commonly done via URL modification
- Also known as Privilege escalation.
- Example
  - An attacker simply changes a known URL of a website by adding "admin"
    > <https://fac3book.com/app/group/member_details/>
    > <https://fac3book.com/app/group/admin/member_details>
    >
    > - if an unauthenticaed user can access both pages, priviledge escalation will happen.
    > - id a non admin can access the admin page, it is a problem.

- How to prevent
  - check back-end configs
  - Minimize CORS(cross-origin resource sharing) usage.
  - Apply some record ownership mechanisms rather than a user can create, read, update, or delete any record.
  - Log access control failures and alert admins when repeated failures occur
  - impliment a specified rate access to your APIs to minimize automated attacks via tools
  - study cookies, sessions, tokens, and folow OAuth standards.

**2. Cryptographic Failure / Sensitive Data Exposure**

- protection of data at rest and in transit is needed
- happens when...
  - data is sent, transmitted, and received in plain text
  - cryptographic algorithms are old or aren't updated
  - use of default cryptographic algorithms and protocols
- how to prevent
  - classify which data are sensitive so that you won't have to encrypt everything
  - Discard quickly sensitive data
  - encrypt all sensitive data at rest
  - ensure up to data algorithms, protocols and keys
  - don't use legacy protocols like FTP and SMTP to transport sensitive data.
  - consider authenticated encryption instead of encryption only.
  - avoid depreciated cryptographic functions like MD5, SHA1, PKCS number 1 v1.5
- Example:
    > An application encrypts credit card numbers in a database using automatic database encryption. However, this data is automatically decrypted when retrieved, allowing a SQL injection flaw to retrieve credit card numbers in clear text.

**3. Injection**

- happens when...
  - User-supplied data is not validated, filtered, or sanitized by the application.
  - Dynamic queries or non-parameterized calls without context-aware escaping are used directly in the interpreter.
  - Hostile data is used within object-relational mapping (ORM) search parameters to extract additional, sensitive records.
  - Hostile data is directly used or concatenated. The SQL or command contains the structure and malicious data in dynamic queries, commands, or stored procedures.
- can be prevented by...
  - use a safe API
  - user positive server-side input validation
  - Use LIMIT and other SQL Controls within queries to prevent mass disclosure of records in case of SQL injection.

**4. Insecure Design**

- how to prevent...
  - Establish and use a secure development lifecycle with AppSec professionals to help evaluate and design security and privacy-related controls

  - Establish and use a library of secure design patterns or paved road ready to use components

  - Use threat modeling for critical authentication, access control, business logic, and key flows

  - Integrate security language and controls into user stories

  - Integrate plausibility checks at each tier of your application (from frontend to backend)

  - Write unit and integration tests to validate that all critical flows are resistant to the threat model. Compile use-cases and misuse-cases for each tier of your application.

  - Segregate tier layers on the system and network layers depending on the exposure and protection needs

  - Segregate tenants robustly by design throughout all tiers

  - Limit resource consumption by user or service
- Example
    > A retail chain’s e-commerce website does not have protection against bots run by scalpers buying high-end video cards to resell auction websites. This creates terrible publicity for the video card makers and retail chain owners and enduring bad blood with enthusiasts who cannot obtain these cards at any price. Careful anti-bot design and domain logic rules, such as purchases made within a few seconds of availability, might identify inauthentic purchases and rejected such transactions.

**5. Security Misconfiguration**

- happens when there is...
  - Missing appropriate security hardening across any part of the application stack or improperly configured permissions on cloud services.

  - Unnecessary features are enabled or installed (e.g., unnecessary ports, services, pages, accounts, or privileges).

  - Default accounts and their passwords are still enabled and unchanged.

  - Error handling reveals stack traces or other overly informative error messages to users.

  - For upgraded systems, the latest security features are disabled or not configured securely.

  - The security settings in the application servers, application frameworks (e.g., Struts, Spring, ASP.NET), libraries, databases, etc., are not set to secure values.

  - The server does not send security headers or directives, or they are not set to secure values.

  - The software is out of date or vulnerable (see A06:2021-Vulnerable and Outdated Components).

- can be prevented by...
  - A repeatable hardening process makes it fast and easy to deploy another environment that is appropriately locked down. Development, QA, and production environments should all be configured identically, with different credentials used in each environment. This process should be automated to minimize the effort required to set up a new secure environment.

  - A minimal platform without any unnecessary features, components, documentation, and samples. Remove or do not install unused features and frameworks.

  - A task to review and update the configurations appropriate to all security notes, updates, and patches as part of the patch management process (see A06:2021-Vulnerable and Outdated Components). Review cloud storage permissions (e.g., S3 bucket permissions).

  - A segmented application architecture provides effective and secure separation between components or tenants, with segmentation, containerization, or cloud security groups (ACLs).

  - Sending security directives to clients, e.g., Security Headers.

  - An automated process to verify the effectiveness of the configurations and settings in all environments.
- Example...
    >
    > 1. Directory listing is not disabled on the server. An attacker discovers they can simply list directories. The attacker finds and downloads the compiled Java classes, which they decompile and reverse engineer to view the code. The attacker then finds a severe access control flaw in the application.
    > 2. The application server's configuration allows detailed error messages, e.g., stack traces, to be returned to users. This potentially exposes sensitive information or underlying flaws such as component versions that are known to be vulnerable.
    > 3. The application server comes with sample applications not removed from the production server. These sample applications have known security flaws attackers use to compromise the server. Suppose one of these applications is the admin console, and default accounts weren't changed. In that case, the attacker logs in with default passwords and takes over.

**6. Vulnerable and outdated components**

- can happen when...
  - If you do not know the versions of all components you use (both client-side and server-side). This includes components you directly use as well as nested dependencies.

  - If the software is vulnerable, unsupported, or out of date. This includes the OS, web/application server, database management system (DBMS), applications, APIs and all components, runtime environments, and libraries.

  - If you do not scan for vulnerabilities regularly and subscribe to security bulletins related to the components you use.

  - If you do not fix or upgrade the underlying platform, frameworks, and dependencies in a risk-based, timely fashion. This commonly happens in environments when patching is a monthly or quarterly task under change control, leaving organizations open to days or months of unnecessary exposure to fixed vulnerabilities.

  - If software developers do not test the compatibility of updated, upgraded, or patched libraries.

- can be prevent by...
  - Remove unused dependencies, unnecessary features, components, files, and documentation.

  - Continuously inventory the versions of both client-side and server-side components (e.g., frameworks, libraries) and their dependencies using tools like versions, OWASP Dependency Check, retire.js, etc. Continuously monitor sources like Common Vulnerability and Exposures (CVE) and National Vulnerability Database (NVD) for vulnerabilities in the components. Use software composition analysis tools to automate the process. Subscribe to email alerts for security vulnerabilities related to components you use.

  - Only obtain components from official sources over secure links. Prefer signed packages to reduce the chance of including a modified, malicious component (See A08:2021-Software and Data Integrity Failures).

  - Monitor for libraries and components that are unmaintained or do not create security patches for older versions. If patching is not possible, consider deploying a virtual patch to monitor, detect, or protect against the discovered issue.

- Example...
    > Components typically run with the same privileges as the application itself, so flaws in any component can result in serious impact. Such flaws can be accidental (e.g., coding error) or intentional (e.g., a backdoor in a component). Some example exploitable component vulnerabilities discovered are:
    >
    > - CVE-2017-5638, a Struts 2 remote code execution vulnerability that enables the execution of arbitrary code on the server, has been blamed for significant breaches.
    > - While the internet of things (IoT) is frequently difficult or impossible to patch, the importance of patching them can be great (e.g., biomedical devices).

**7. Identification and authentication failures**

- Confirmation of the user's identity, authentication, and session management is critical to protect against authentication-related attacks.
- Might happen when...
  - Permits automated attacks such as credential stuffing, where the attacker has a list of valid usernames and passwords.

  - Permits brute force or other automated attacks.

  - Permits default, weak, or well-known passwords, such as "Password1" or "admin/admin".

  - Uses weak or ineffective credential recovery and forgot-password processes, such as "knowledge-based answers," which cannot be made safe.

  - Uses plain text, encrypted, or weakly hashed passwords data stores (see A02:2021-Cryptographic Failures).

  - Has missing or ineffective multi-factor authentication.

  - Exposes session identifier in the URL.

  - Reuse session identifier after successful login.

  - Does not correctly invalidate Session IDs. User sessions or authentication tokens (mainly single sign-on (SSO) tokens) aren't properly invalidated during logout or a period of inactivity.

- Can be prevented by...
  - Where possible, implement multi-factor authentication to prevent automated credential stuffing, brute force, and stolen credential reuse attacks.

  - Do not ship or deploy with any default credentials, particularly for admin users.

  - Implement weak password checks, such as testing new or changed passwords against the top 10,000 worst passwords list.

  - Align password length, complexity, and rotation policies with National Institute of Standards and Technology (NIST) 800-63b's guidelines in section 5.1.1 for Memorized Secrets or other modern, evidence-based password policies.

  - Ensure registration, credential recovery, and API pathways are hardened against account enumeration attacks by using the same messages for all outcomes.

  - Limit or increasingly delay failed login attempts, but be careful not to create a denial of service scenario. Log all failures and alert administrators when credential stuffing, brute force, or other attacks are detected.

  - Use a server-side, secure, built-in session manager that generates a new random session ID with high entropy after login. Session identifier should not be in the URL, be securely stored, and invalidated after logout, idle, and absolute timeouts.

- Scenarios...
    > Scenario #1: Credential stuffing, the use of lists of known passwords, is a common attack. Suppose an application does not implement automated threat or credential stuffing protection. In that case, the application can be used as a password oracle to determine if the credentials are valid.
    > Scenario #2: Most authentication attacks occur due to the continued use of passwords as a sole factor. Once considered best practices, password rotation and complexity requirements encourage users to use and reuse weak passwords. Organizations are recommended to stop these practices per NIST 800-63 and use multi-factor authentication.
    > Scenario #3: Application session timeouts aren't set correctly. A user uses a public computer to access an application. Instead of selecting "logout," the user simply closes the browser tab and walks away. An attacker uses the same browser an hour later, and the user is still authenticated.

**8. Software and data integrity failures**

- These failures relate to code and infrastructure that does not protect against integrity violations. An example of this is where an application relies upon plugins, libraries, or modules from untrusted sources, repositories, and content delivery networks (CDNs). An insecure CI/CD pipeline can introduce the potential for unauthorized access, malicious code, or system compromise. Lastly, many applications now include auto-update functionality, where updates are downloaded without sufficient integrity verification and applied to the previously trusted application. Attackers could potentially upload their own updates to be distributed and run on all installations. Another example is where objects or data are encoded or serialized into a structure that an attacker can see and modify is vulnerable to insecure deserialization.
- Can by prevented by...
  - Use digital signatures or similar mechanisms to verify the software or data is from the expected source and has not been altered.

  - Ensure libraries and dependencies, such as npm or Maven, are consuming trusted repositories. If you have a higher risk profile, consider hosting an internal known-good repository that's vetted.

  - Ensure that a software supply chain security tool, such as OWASP Dependency Check or OWASP CycloneDX, is used to verify that components do not contain known vulnerabilities

  - Ensure that there is a review process for code and configuration changes to minimize the chance that malicious code or configuration could be introduced into your software pipeline.

  - Ensure that your CI/CD pipeline has proper segregation, configuration, and access control to ensure the integrity of the code flowing through the build and deploy processes.

  - Ensure that unsigned or unencrypted serialized data is not sent to untrusted clients without some form of integrity check or digital signature to detect tampering or replay of the serialized data
- Scenarios
    > Scenario #1 Update without signing: Many home routers, set-top boxes, device firmware, and others do not verify updates via signed firmware. Unsigned firmware is a growing target for attackers and is expected to only get worse. This is a major concern as many times there is no mechanism to remediate other than to fix in a future version and wait for previous versions to age out.
    > Scenario #2 SolarWinds malicious update: Nation-states have been known to attack update mechanisms, with a recent notable attack being the SolarWinds Orion attack. The company that develops the software had secure build and update integrity processes. Still, these were able to be subverted, and for several months, the firm distributed a highly targeted malicious update to more than 18,000 organizations, of which around 100 or so were affected. This is one of the most far-reaching and most significant breaches of this nature in history.
    > Scenario #3 Insecure Deserialization: A React application calls a set of Spring Boot microservices. Being functional programmers, they tried to ensure that their code is immutable. The solution they came up with is serializing the user state and passing it back and forth with each request. An attacker notices the "rO0" Java object signature (in base64) and uses the Java Serial Killer tool to gain remote code execution on the application server.

**9. Security logging and monitoring failures**

- this category is to help detect, escalate, and respond to active breaches. Without logging and monitoring, breaches cannot be detected.
- Occurs when...
  - Auditable events, such as logins, failed logins, and high-value transactions, are not logged.

  - Warnings and errors generate no, inadequate, or unclear log messages.

  - Logs of applications and APIs are not monitored for suspicious activity.

  - Logs are only stored locally.

  - Appropriate alerting thresholds and response escalation processes are not in place or effective.

  - Penetration testing and scans by dynamic application security testing (DAST) tools (such as OWASP ZAP) do not trigger alerts.

  - The application cannot detect, escalate, or alert for active attacks in real-time or near real-time.
- can be prevented by implementing the ff...
  - Ensure all login, access control, and server-side input validation failures can be logged with sufficient user context to identify suspicious or malicious accounts and held for enough time to allow delayed forensic analysis.

  - Ensure that logs are generated in a format that log management solutions can easily consume.

  - Ensure log data is encoded correctly to prevent injections or attacks on the logging or monitoring systems.

  - Ensure high-value transactions have an audit trail with integrity controls to prevent tampering or deletion, such as append-only database tables or similar.

  - DevSecOps teams should establish effective monitoring and alerting such that suspicious activities are detected and responded to quickly.

  - Establish or adopt an incident response and recovery plan, such as National Institute of Standards and Technology (NIST) 800-61r2 or later.

> There are commercial and open-source application protection frameworks such as the OWASP ModSecurity Core Rule Set, and open-source log correlation software, such as the Elasticsearch, Logstash, Kibana (ELK) stack, that feature custom dashboards and alerting.

- Example Attack Scenarios
    > Scenario #1: A children's health plan provider's website operator couldn't detect a breach due to a lack of monitoring and logging. An external party informed the health plan provider that an attacker had accessed and modified thousands of sensitive health records of more than 3.5 million children. A post-incident review found that the website developers had not addressed significant vulnerabilities. As there was no logging or monitoring of the system, the data breach could have been in progress since 2013, a period of more than seven years.

    > Scenario #2: A major Indian airline had a data breach involving more than ten years' worth of personal data of millions of passengers, including passport and credit card data. The data breach occurred at a third-party cloud hosting provider, who notified the airline of the breach after some time.

    > Scenario #3: A major European airline suffered a GDPR reportable breach. The breach was reportedly caused by payment application security vulnerabilities exploited by attackers, who harvested more than 400,000 customer payment records. The airline was fined 20 million pounds as a result by the privacy regulator.

**10. Server-side Request Forgery (SSRF)**

- SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).
- As modern web applications provide end-users with convenient features, fetching a URL becomes a common scenario. As a result, the incidence of SSRF is increasing. Also, the severity of SSRF is becoming higher due to cloud services and the complexity of architectures.

- How to Prevent
  - From Network layer
    - Segment remote resource access functionality in separate networks to reduce the impact of SSRF

    - Enforce “deny by default” firewall policies or network access control rules to block all but essential intranet traffic.
    - Hints:
      - Establish an ownership and a lifecycle for firewall rules based on applications.
      - Log all accepted and blocked network flows on firewalls (see A09:2021-Security Logging and Monitoring Failures).

  - From Application layer:
    - Sanitize and validate all client-supplied input data

    - Enforce the URL schema, port, and destination with a positive allow list

    - Do not send raw responses to clients

    - Disable HTTP redirections

    - Be aware of the URL consistency to avoid attacks such as DNS rebinding and “time of check, time of use” (TOCTOU) race conditions

        > Note: Do not mitigate SSRF via the use of a deny list or regular expression. Attackers have payload lists, tools, and skills to bypass deny lists.

  - Additional Measures to consider:
    - Don't deploy other security relevant services on front systems (e.g. OpenID). Control local traffic on these systems (e.g. localhost)

    - For frontends with dedicated and manageable user groups use network encryption (e.g. VPNs) on independent systems to consider very high protection needs

- Example Attack Scenarios
Attackers can use SSRF to attack systems protected behind web application firewalls, firewalls, or network ACLs, using scenarios such as:

    > Scenario #1: Port scan internal servers – If the network architecture is unsegmented, attackers can map out internal networks and determine if ports are open or closed on internal servers from connection results or elapsed time to connect or reject SSRF payload connections.

    > Scenario #2: Sensitive data exposure – Attackers can access local files or internal services to gain sensitive information such as file:///etc/passwd</span> and <http://localhost:28017/>.

    > Scenario #3: Access metadata storage of cloud services – Most cloud providers have metadata storage such as <http://169.254.169.254/>. An attacker can read the metadata to gain sensitive information.

    > Scenario #4: Compromise internal services – The attacker can abuse internal services to conduct further attacks such as Remote Code Execution (RCE) or Denial of Service (DoS).
