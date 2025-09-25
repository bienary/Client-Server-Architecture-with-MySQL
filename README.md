# 🖧 Client-Server-Architecture-with-MySQL
## 🌫 DevOps/Cloud Engineering ~ Client-Server Architecture with MySQL

#### **Understanding Client-Server Architecture**

- `Client-Server` refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

- **In their communication, each machine has its own role:**

> The machine sending requests is usually referred to as the "Client"

> The machine responding (serving) is called the "Server"

> Our Web Server has a role of a `Client` that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network).

---

#### **Step-by-step guide on how to implement MySQL Client-Server architecture on AWS EC2 Linux instances**

**1. Setup EC2 Instances**

- Create two EC2 instances running Ubuntu Linux.

- Name one `mysql-server` and the other `mysql-client`.

<img width="1070" height="150" alt="Screenshot From 2025-09-25 22-46-11" src="https://github.com/user-attachments/assets/38898181-4661-4154-b161-07b40e310909" />

**2. On mysql-server instance: Install MySQL Server**

- SSH into the Server instance.

```
ssh -i <Your-private-key.pem> ubuntu@<EC2-Public-IP-address>
```
- Update and Upgrade system packages:
```
sudo apt update && sudo apt upgrade
```
- install `MySQL Server`
```
sudo apt install mysql-server -y
```

<img width="1318" height="508" alt="Screenshot From 2025-09-25 23-16-07" src="https://github.com/user-attachments/assets/fc8122cc-e305-4f9f-b9f4-8def398eede4" />

- Check MySQL service status
```
sudo systemctl status mysql
```

<img width="1306" height="418" alt="Screenshot From 2025-09-25 23-18-28" src="https://github.com/user-attachments/assets/cdabd26a-5be2-429c-944a-637e386be94c" />
