# 🖧 Client-Server-Architecture-with-MySQL
## 🌫 DevOps/Cloud Engineering ~ Client-Server Architecture with MySQL

#### **Understanding Client-Server Architecture**

- `Client-Server` refers to an architecture in which two or more computers are connected together over a network to send and receive requests between one another.

- **In their communication, each machine has its own role:**

> The machine sending requests is usually referred to as the "Client"

> The machine responding (serving) is called the "Server"

> Our Web Server has a role of a `Client` that connects and reads/writes to/from a Database (DB) Server (MySQL, MongoDB, Oracle, SQL Server or any other), and the communication between them happens over a Local Network (it can also be Internet connection, but it is a common practice to place Web Server and DB Server close to each other in local network).

---

#### 🎯**Step-by-step guide on how to implement MySQL Client-Server architecture on AWS EC2 Linux instances**

**1. Setup EC2 Instances**

- Create two EC2 instances running Ubuntu Linux.

- Name one `mysql-server` and the other `mysql-client`.

<img width="1070" height="150" alt="Screenshot From 2025-09-25 22-46-11" src="https://github.com/user-attachments/assets/38898181-4661-4154-b161-07b40e310909" />

🌍 **Allow inbound traffic on port 3306 in mysql-server security group**

- Go to AWS Console > EC2 > Security Groups.

- Select the security group attached to mysql-server.

- Add a new Inbound rule: Select Custom TCP > Port 3306 > Enter the private IP of `MySQL-Client` instance only


<img width="1330" height="483" alt="image" src="https://github.com/user-attachments/assets/953dbafc-4d90-4c40-8dc6-e3025547cb4e" />



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

3. **On mysql-client instance: Install MySQL Client**

- SSH into the Client instance.

```
ssh -i <Your-private-key.pem> ubuntu@<EC2-Public-IP-address>
```
- Update and Upgrade system packages:
```
sudo apt update && sudo apt upgrade
```
- install `MySQL Server`
```
sudo apt install mysql-client -y
```

<img width="1330" height="400" alt="image" src="https://github.com/user-attachments/assets/1dc4b6b3-32b3-4b2b-a82d-ab78136a94f0" />

4. **Configure MySQL server to accept remote connections**

```
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```
<img width="1317" height="712" alt="image" src="https://github.com/user-attachments/assets/85a9cbb0-a299-46a1-abb9-c93339fca576" />

- Restart MySQL Server to apply changes
```
sudo systemctl restart mysql
```
5. **Create MySQL user with remote access permissions on mysql-server**

- Login to MySQL Server
```
sudo mysql
```
- Create a user that can connect remotely
```
CREATE USER 'remoteuser'@'client_private_ip' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON *.* TO 'remoteuser'@'client_private_ip' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

<img width="1328" height="571" alt="image" src="https://github.com/user-attachments/assets/f9a5ac79-c663-41d6-a606-900d0406e128" />

- Check that you have successfully connected to a remote MySQL server and can perform SQL queries:
```
show databases;
```
<img width="1328" height="571" alt="Screenshot From 2025-09-26 00-55-36" src="https://github.com/user-attachments/assets/5d9c2d05-1732-41cf-a9f5-82c630f25a16" />
- Add some data:

```
CREATE DATABASE binary_db;
USE binary_db;
```

```
INSERT INTO employees (name, position, salary) VALUES 
('Oladapo', 'DevOps Engineer', 200000.00),
('Dolapo', 'IT Manager', 350000.00),
('Funmilayo', 'Intern', 75000.00);
```

<img width="1323" height="623" alt="image" src="https://github.com/user-attachments/assets/bd489ec0-d83a-4e6d-97a6-eeba9ebb451c" />
