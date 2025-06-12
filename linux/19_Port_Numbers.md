# 📦 Common Protocols and Default Port Numbers

| **Protocol**           | **Default Port** | **Description**                                 |
|------------------------|------------------|------------------------------------------------|
| **SSH (Secure Shell)** | `22`             | Secure remote login to machines                 |
| **HTTP**               | `80`             | Standard web traffic (unsecured)                |
| **HTTPS**              | `443`            | Secure web traffic (SSL/TLS encrypted)          |
| **FTP (File Transfer Protocol)** | `21`  | Transfer files (unsecured)                      |
| **FTPS (FTP Secure)**  | `990`            | FTP over SSL/TLS                                |
| **SFTP (SSH File Transfer Protocol)** | `22` | Uses SSH for secure file transfer               |
| **Telnet**             | `23`             | Remote login (unsecured)                        |
| **SMTP (Send Mail Transfer Protocol)** | `25`  | Email sending (unsecured or with STARTTLS)      |
| **SMTPS (SMTP Secure)**| `465`            | SMTP over SSL (deprecated, but still used)      |
| **Submission (SMTP over STARTTLS)** | `587`  | Email sending (Recommended secure port)         |
| **POP3 (Post Office Protocol)** | `110`  | Receiving emails                                |
| **POP3S (Secure POP3)** | `995`          | POP3 over SSL/TLS                               |
| **IMAP (Internet Message Access Protocol)** | `143` | Reading emails                                 |
| **IMAPS (Secure IMAP)** | `993`           | IMAP over SSL/TLS                               |
| **DNS (Domain Name System)** | `53`     | Resolves domain names to IPs                    |
| **MySQL**              | `3306`           | Database connections to MySQL                   |
| **PostgreSQL**         | `5432`           | Database connections to PostgreSQL              |
| **MongoDB**            | `27017`          | Database connections to MongoDB                 |
| **Redis**              | `6379`           | Default Redis database port                     |
| **RDP (Remote Desktop Protocol)** | `3389` | Windows remote desktop connection              |
| **LDAP (Lightweight Directory Access Protocol)** | `389` | Directory services                            |
| **LDAPS (Secure LDAP)** | `636`           | LDAP over SSL/TLS                               |
| **NTP (Network Time Protocol)** | `123`  | Time synchronization                            |
| **SNMP (Simple Network Management Protocol)** | `161` | Network monitoring                             |
| **Kerberos**           | `88`             | Authentication protocol                         |
| **SMB (Windows File Sharing)** | `445`   | Windows network file sharing                    |
| **ElasticSearch (HTTP API)** | `9200`   | Search and analytics engine                     |
| **Prometheus**         | `9090`           | Monitoring system                               |
| **Grafana**            | `3000`           | Analytics & visualization                       |
| **Kubernetes API Server** | `6443`       | Secure Kubernetes API access                    |

---

## ✅ Example for SSH, HTTP, HTTPS:

- **SSH** → Port `22`
- **HTTP** → Port `80`
- **HTTPS** → Port `443`

---

If you want **this entire list in a downloadable `.md` file**, let me know. Happy to generate that for you!
