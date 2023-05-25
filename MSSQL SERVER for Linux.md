# See:
- [Microsoft SQL Server - Ubuntu based images](https://hub.docker.com/_/microsoft-mssql-server)
- [Install the SQL Server command-line tools sqlcmd and bcp on Linux](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-setup-tools?view=sql-server-ver16)
- [Quickstart: Run SQL Server Linux container images with Docker](https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver16&pivots=cs1-bash)
- [Bulk copy data with bcp to SQL Server on Linux](https://learn.microsoft.com/en-us/sql/linux/sql-server-linux-migrate-bcp?view=sql-server-ver16)
- [sqlcmd - Use the utility](https://learn.microsoft.com/en-us/sql/ssms/scripting/sqlcmd-use-the-utility?source=recommendations&view=sql-server-ver16)
- [sqlcmd Utility](https://learn.microsoft.com/en-us/sql/tools/sqlcmd-utility?source=recommendations&view=sql-server-ver16)

# See:
- [Download SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16)
- [What is SQL Server Management Studio (SSMS)?](https://learn.microsoft.com/en-us/sql/ssms/sql-server-management-studio-ssms?view=sql-server-ver16)

# See:
- [What is Azure Data Studio?](https://learn.microsoft.com/en-us/sql/azure-data-studio/what-is-azure-data-studio?view=sql-server-ver16)
- [Download and install Azure Data Studio](https://learn.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio?view=sql-server-ver16)

# 运行 SQL SERVER 2022
- [Microsoft SQL Server - Ubuntu based images](https://hub.docker.com/_/microsoft-mssql-server)
- [Quickstart: Run SQL Server Linux container images with Docker](https://learn.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-ver16&pivots=cs1-bash)
```
docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=yourStrong(!)Password" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2022-latest
```

# With Docker-commpose 
- configure file  "docker-compose.yml":
```
version: '3.9'
services:
  db:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: sql2022
    hostname: sql2022
    restart: always
    environment:
      SA_PASSWORD: "YourStrong!Passw0rd"
      ACCEPT_EULA: "Y"
    ports:
      - "1433:1433"
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /etc/timezone:/etc/timezone:ro

```

```
docker-compose up -d
docker-compose down
docker-compose ps
docker-compose logs
docker-compose images
docker-compose      ## For Help
```

## 查看日志 是服务器否准备好

```
docker exec -t sql2022 cat /var/opt/mssql/log/errorlog | grep connection
docker-compose logs | grep connection
```

## 更改 SA 密码
### 查看不安全的密码：
```
 ps -eax
 ps -eax | grep SA
```

### 下面的命令可以更改SA密码
```
sudo docker exec -it sql2022 /opt/mssql-tools/bin/sqlcmd \
-S localhost -U SA \
 -P "$(read -sp "Enter current SA password: "; echo "${REPLY}")" \
 -Q "ALTER LOGIN SA WITH PASSWORD=\"$(read -sp "Enter new SA password: "; echo "${REPLY}")\""
```
# 连接 SQL SERVER 2022 
- 登陆容器 container
```
sudo docker exec -it sql2022 "bash"
```
- 在容器内部使用完整路径通过 sqlcmd 进行本地连接
```
/opt/mssql-tools/bin/sqlcmd -S localhost -U SA -P "<YourNewStrong@Passw0rd>"
/opt/mssql-tools/bin/sqlcmd -S localhost -U SA
```
- 如果成功，应会显示 sqlcmd 命令提示符：1>

# 建立数据库 TestDB

```
create database TestDB
go

select name from sys.databases
go

```

# 插入数据
```
use TestDB
CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT);
INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
GO
```

# 选择数据

```
SELECT * FROM Inventory WHERE quantity > 152;
go
```

# 退出sqlcmd 命令提示符
```
quit
```



