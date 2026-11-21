# vsftpd 2.3.4
The vsftpd 2.3.4 FTP server (commonly seen on port 21) shipped with a malicious backdoor introduced into the source distribution. Connecting with a username ending in ":)" opens a command shell on TCP port 6200, granting remote command execution as root. Tracked as CVE-2011-2523. Severity: critical. Remediation: upgrade to a clean, vendor-verified vsftpd build and verify package checksums; never run software from unverified mirrors.

# OpenSSH 7.2p2
OpenSSH versions before 7.7 (including the 7.2 series often seen on port 22) are affected by a username enumeration weakness, CVE-2018-15473. By measuring response timing differences to malformed authentication requests, an attacker can determine which usernames exist on the system, aiding password-guessing and spear-phishing. Severity: medium. Remediation: upgrade OpenSSH to 7.7 or later, enforce key-based authentication, and rate-limit authentication attempts with fail2ban.

# Apache httpd 2.4.49
Apache HTTP Server 2.4.49 (port 80/443) contains a path-traversal flaw, CVE-2021-41773. A crafted URL using encoded "../" sequences can read files outside the document root, and when mod_cgi is enabled it escalates to remote code execution. Severity: critical. Remediation: upgrade to Apache 2.4.51 or later, disable directory aliasing you do not need, and ensure "require all denied" is set on the filesystem root.

# Apache Log4j 2.14
Applications using Apache Log4j 2 versions 2.0-beta9 through 2.14.1 are vulnerable to Log4Shell, CVE-2021-44228. If attacker-controlled text is logged, a JNDI lookup string such as "${jndi:ldap://...}" causes the server to fetch and execute remote code. This often surfaces through web services on ports 80/443/8080. Severity: critical. Remediation: upgrade Log4j to 2.17.1 or later, set log4j2.formatMsgNoLookups=true as a stopgap, and block outbound LDAP/RMI from servers.

# Samba 3.5.0
Samba file-sharing services (ports 139/445) from 3.5.0 up to 4.6.4 are vulnerable to CVE-2017-7494, nicknamed SambaCry. An authenticated client that can write to a share can upload and trigger a shared library, achieving remote code execution on the server. Severity: critical. Remediation: patch Samba to a fixed release, add "nt pipe support = no" to smb.conf as mitigation, and restrict share write access.

# Microsoft SMBv1
Windows hosts exposing SMBv1 (port 445) are vulnerable to EternalBlue, CVE-2017-0144, addressed by bulletin MS17-010. A malformed SMBv1 packet causes a buffer overflow leading to remote code execution; this was the propagation vector for the WannaCry and NotPetya worms. Severity: critical. Remediation: apply MS17-010, disable SMBv1 entirely, and block port 445 at the network perimeter.

# ProFTPD 1.3.5
ProFTPD 1.3.5 (port 21) with the mod_copy module enabled is vulnerable to CVE-2015-3306. The SITE CPFR and SITE CPTO commands can be used without authentication to copy files anywhere the daemon can write, enabling attackers to plant a web shell or read sensitive files. Severity: high. Remediation: upgrade ProFTPD, disable mod_copy unless required, and run the FTP daemon under a restricted account.

# OpenSSL 1.0.1
Services using OpenSSL 1.0.1 through 1.0.1f for TLS (ports 443, 993, 995, and others) are vulnerable to Heartbleed, CVE-2014-0160. A malformed TLS heartbeat request makes the server return up to 64 KB of process memory per request, which can leak private keys, session cookies, and credentials. Severity: critical. Remediation: upgrade OpenSSL to 1.0.1g or later, revoke and reissue affected certificates and keys, and force user password resets.

# MySQL 5.5
MySQL and MariaDB database servers (port 3306) in several 5.5/5.6 builds are affected by CVE-2012-2122, an authentication-bypass flaw. On vulnerable systems a timing issue lets a repeated login with an incorrect password occasionally succeed, granting access without valid credentials. Severity: high. Remediation: patch the database, never expose 3306 to untrusted networks, and require TLS plus strong, unique account passwords.

# Redis 4.0
Redis instances (port 6379) left without authentication and reachable over the network can be abused for remote code execution. An attacker writes a malicious module or crafted RDB/SSH key file via unauthenticated commands and loads it. There is no single CVE; this is a configuration weakness widely exploited in the wild. Severity: critical. Remediation: require a strong "requirepass", bind Redis to localhost or a private interface, enable protected-mode, and disable the MODULE and CONFIG commands.

# PHP-CGI
Web servers running php-cgi (ports 80/443) are vulnerable to CVE-2012-1823, an argument-injection flaw. Query strings beginning with "?-" are passed to the PHP binary as command-line switches, allowing source disclosure or remote code execution. Severity: critical. Remediation: upgrade PHP, use PHP-FPM instead of php-cgi, and add a web-server rule that rejects request strings starting with a dash.

# Telnet service
A telnet service (port 23) transmits all data, including usernames and passwords, in cleartext with no encryption. Anyone able to observe the traffic can capture credentials, and telnet is frequently left enabled with default credentials on routers, switches, and IoT devices. Severity: high. Remediation: disable telnet entirely and replace it with SSH; if a serial-console fallback is required, isolate it on a dedicated management network.

# nginx 1.18.0
nginx versions 0.6.18 through 1.20.0 (including 1.18.0), commonly serving HTTP on port 80 and HTTPS on port 443, are vulnerable to CVE-2021-23017, a one-byte memory overwrite in the DNS resolver. When the resolver directive is configured, an attacker capable of forging UDP packets from the DNS server (typically port 53) can send a specially crafted DNS response, potentially crashing an nginx worker process or allowing arbitrary code execution. Severity: high (CVSS 7.7). Remediation: upgrade to nginx 1.20.1 or later and restrict DNS communication to trusted resolvers.

# PostgreSQL 9.6.24
PostgreSQL database servers (typically TCP port 5432) in versions 9.6 through 9.6.23 are vulnerable to CVE-2021-23214, a man-in-the-middle vulnerability involving the processing of unencrypted data during SSL or GSS connection establishment. When the server uses trust authentication with a clientcert requirement or cert authentication, an attacker capable of intercepting and injecting TCP traffic can insert arbitrary SQL commands into the initial database connection despite encryption and certificate verification. Severity: high (CVSS 8.1). Remediation: upgrade to PostgreSQL 9.6.24 or later, use secure authentication configurations, and restrict database access to trusted networks.

# Apache httpd 2.2.8
Apache HTTP Server 2.2.8 is affected by CVE-2017-9798, commonly called OptionsBleed. The vulnerability is associated with the Apache HTTP service, commonly exposed on TCP port 80 (HTTP) or TCP port 443 (HTTPS). When an unrecognized HTTP method is specified in a `<Limit>` directive in an `.htaccess` file, processing the affected configuration can corrupt the server's global methods table, resulting in erratic behavior and potential information disclosure. The vulnerability affects Apache HTTP Server 2.2 releases including 2.2.8. Severity: low. Remediation: migrate to a supported Apache HTTP Server release, preferably the current supported 2.4 release, and review `.htaccess` files for unsafe `<Limit>` directives.

# Apache Tomcat 9.0.30
Apache Tomcat 9.0.30 is affected by CVE-2020-1938, commonly called Ghostcat. The vulnerability involves the Apache JServ Protocol (AJP) connector, commonly exposed on TCP port 8009. If the AJP connector is enabled and accessible, an attacker may be able to read files from a web application and potentially process application files as JSP. Remote code execution may be possible when an attacker can also upload files into the web application. The vulnerable range includes Tomcat 9.0.0.M1 through 9.0.0.30. Severity: critical (CVSS 9.8). Remediation: upgrade to Tomcat 9.0.31 or later, disable the AJP connector if it is not needed, and restrict access to AJP connections.

# Jetty 9.4.40
Eclipse Jetty 9.4.40 is affected by CVE-2021-28169. The vulnerability affects the ConcatServlet and is typically reachable through the Jetty HTTP service, commonly exposed on TCP port 8080 (HTTP) or TCP port 8443 (HTTPS). A double-encoded URL path sent to the ConcatServlet can bypass protections around the WEB-INF directory and expose protected application resources, including web.xml. This can disclose sensitive information about the web application. The vulnerability affects Jetty versions through 9.4.40. Severity: medium (CVSS 5.3). Remediation: upgrade to Jetty 9.4.41 or later and review application access controls and use of the ConcatServlet.