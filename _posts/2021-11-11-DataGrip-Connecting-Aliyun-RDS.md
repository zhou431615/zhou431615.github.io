---
layout:     post
title:      "DataGrip中数据库(云数据库)连接与管理"
subtitle:   "使用操作"
date:       2021-11-12 08:00:00
author:     "QianYe"

tags:
- MySQL
---


# DataGrip中数据库(云数据库)连接与管理

### Intro

购买阿里云的RDS实例，使用DataGrip客户端连接时出现的问题。具体原因，由于没有为云数据库设置白名单，导致在本地设备连接失败。解决办法：（前提，已申请开放云数据库的外网地址）将本机的IP的地址，添加到白名单即可成功访问。同理，使用ECS实例访问云数据库RDS也是如此。但是如果你的ECS实例和RDS实例在同一区域，例如同在杭州，并且网络类型相同。如果都是专有网络，专有网络ID也需要相同。在此前提条件下，ECS实例可以使用内网访问RDS实例。由此总一下，在不同场景条件下，使用客户端或者命令行连接数据库的情况。

### 场景

![image-20211129140940047](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111291409230.png)

### RDS的白名单设置

要使用百度（www.ip138.com/）查询本机公网IP的地址 （使用CMD 命令ipconfig /all 查询到是本地局域网IP地址，不要混淆。）

![image-20211129145612547](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111291456633.png)

一般来说，开放白名单，确保端口可以访问，驱动配置正确，账号和密码填写正确，就可以成功连接RDS云数据库。通常我们需要连接到别人的数据库、服务器或者云数据库前，先ping一下主机是否可以访问，telnet一下端口。成功后，使用客户端DataGrip连接。

![image-20211129150638583](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111291506659.png)

```
ping <IP>
```

```
telnet <IP> <port>
```

> 使用之前，确保telnet命令开启。 控制面板>>windows功能

![image-20211129151044582](https://mybolg-typora.oss-cn-beijing.aliyuncs.com/blogPic/202111291510663.png)

当您连接云数据库RDS，可以使用客户端管理数据库，或者阿里云的DMS管理数据库。

可以参考连接排查策略。

# 数据库连接排查策略

## Step 1:检查您的网络设置

数据库可以在本地、服务器上或云中工作。对于服务器和云数据库，您需要网络连接。要验证连接是否可用，请使用**ping**和**telnet**命令。

使用**ping**命令，您可以确保从源计算机可以访问目标计算机。打开命令行并键入以下命令：`ping -a <host_IP>`，其中`-a`是将地址解析为主机名的命令选项（如果可能）。如果在**ping**命令中使用主机名，主机名将被解析为 IP 地址。例如，`ping -a example.com`解析为`PING example.com (93.184.216.34)`。

```none
ping -a <host_IP>
```

已复制！

![用ping命令测试连接](http://127.0.0.1:63342/help/img/idea/2021.2/db_test_connection_with_ping.png)

使用**telnet**命令，您可以测试与远程计算机的连接并发出命令。如果将端口指定为`telnet`命令的参数，则可以测试到给定端口上的远程主机的连接性。如果连接成功，您会看到消息：`Connected to <host_IP>`。

```none
telnet <host_IP> <port_number>
```

已复制！

![使用 telnet 命令测试连接](http://127.0.0.1:63342/help/img/idea/2021.2/db_test_connection_with_telnet.png)

> 出于安全原因，DBMS 通常会丢弃所有 telnet 连接。telnet 命令允许您检查端口是否已打开以进行通信。

## Step 2. 检查您的连接属性﻿

每个数据库（MySQL、PostgreSQL、Oracle 或任何其他供应商）都有自己的连接设置。大多数数据库包括连接设置：

- **主机**：存储数据库的计算机或其他设备的主机名。它可以是 IP 地址**127.0.0.1**或域名**localhost**。

- **数据库**：要连接的数据库的名称。您可以在数据库服务器的设置中找到数据库名称，也可以询问您的数据库管理员。在某些情况下，可以在数据库命令行中运行查询以查看所有可用数据库的名称。例如，在 MySQL 中，您可以运行`SHOW DATABASES;`.

  ![SHOW DATABASES 查询](http://127.0.0.1:63342/help/img/idea/2021.2/db_troubleshooting_show_databases.png)

  

- **用户**：具有足够权限对数据库执行操作的用户的名称。在数据库命令行中运行查询以查看所有可用数据库的名称。例如，在 MySQL 中，您可以运行`SHOW GRANTS;`.

  ![SHOW GRANTS 查询](http://127.0.0.1:63342/help/img/idea/2021.2/db_troubleshooting_show_grants.png)

  

- **密码**：用户的密码。

- **端口**：标识主机之间连接点的数字。主机使用端口号来确定必须与哪个应用程序、服务或进程建立连接。不同的数据库供应商为其数据库使用不同的端口。以下列表是默认端口号列表。

  |              供应商               |                   默认端口                    |
  | :-------------------------------: | :-------------------------------------------: |
  |        **Amazon Redshift**        |                     5439                      |
  |         **Apache Derby**          |                     1527                      |
  |       **Apache Cassandra**        |                     9042                      |
  |          **Apache Hive**          | 10000 (Hive Server2) or 9083 (Hive Metastore) |
  |      **Azure SQL Database**       |                     1433                      |
  |          **ClickHouse**           |                     8123                      |
  | **Couchbase Query Query Service** |                     11210                     |
  |            **Exasol**             |                     8563                      |
  |           **Greenplum**           |                     5432                      |
  |              **H2**               |                     8082                      |
  |            **HSQLDB**             |                     9001                      |
  |          **IBM Db2 LUW**          |                     50000                     |
  |            **MariaDB**            |                     3306                      |
  |     **Microsoft SQL Server**      |   1433 (TCP), 1434 (UDP might be required)    |
  |             **MySQL**             |                     3306                      |
  |            **Oracle**             |                     1521                      |
  |          **PostgreSQL**           |                     5432                      |
  |           **Snowflake**           |                      443                      |
  |            **SQLite**             |                     None                      |
  |          **Sybase ASE**           |                     5000                      |
  |            **Vertica**            |                     5433                      |

  > 您系统上的实际端口号可能会有所不同。与数据库管理员确认您使用了正确的端口号。

验证所选数据库连接的连接设置是否正确。有关创建或更改数据库连接的更多信息，请参阅[数据库连接](http://127.0.0.1:63342/help/connecting-to-a-database.html)。

## Step 3. 检查驱动程序版本﻿

使用 JDBC 驱动程序，您可以与来自 DataGrip 的数据库管理系统 (DBMS) 进行交互。每个 DBMS 都需要自己的 JDBC 驱动程序。确保驱动程序版本和 DBMS 版本相互兼容。

您可以从 DataGrip 下载所有受支持供应商的驱动程序。您可以在**驱动程序**列表中查看受支持供应商的完整列表Ctrl+Alt+S。或者，您可以将自己的驱动程序添加到现有供应商，或为不在**驱动程序**列表中的供应商创建新的驱动程序条目。

### 下载驱动程序并选择驱动程序版本﻿

要从 JetBrains FTP 服务器下载驱动**程序**，请从**驱动程序**列表中选择一个供应商，然后单击**下载版本。****驱动程序文件**窗格中的**<version_number>**链接。

要更改驱动程序版本，请单击版本**。****驱动程序文件**窗格中的**<version_number>**链接，然后选择您需要的驱动程序版本。

![驱动程序列表和驱动程序设置](http://127.0.0.1:63342/help/img/idea/2021.2/db_download_driver_select_driver_version.png)



### 使用用户驱动程序文件﻿

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：

   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标

2. 在“**数据源和驱动程序”**对话框中，确保您位于“**驱动程序”**选项卡上。

3. 在“**数据源和驱动程序”**对话框中，单击“**添加”**图标 。

4. 在**名称**字段中，键入驱动程序的名称。

5. 在**Driver Files**窗格中，单击**Add**图标  并选择**Custom JARs**。

6. 导航到 JDBC 驱动程序的 JAR 文件，选择它，然后单击**OK**。

7. 在**类**字段中，指定要用于驱动程序的值。

8. 单击**应用**。

9. 要从驱动程序的对话框中**创建数据源**，请单击**创建数据源**。

   ![/help/img/idea/2021.2/db_create_user_driver_connection.png](http://127.0.0.1:63342/help/img/idea/2021.2/db_create_user_driver_connection.png)

   动图

### 从现有连接配置 JDBC 驱动程序﻿

您可以向现有驱动程序添加库或完全替换驱动程序。

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：

   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标

2. 在“**数据源和驱动程序”**对话框中，单击“**驱动程序”**选项卡，然后选择要更改驱动程序的数据源。

3. 单击数据源设置中的**驱动程序**链接。

4. 单击提供的驱动程序条目，然后单击**删除**。

   要恢复更改，请单击窗口右下角的**回滚更改**图标。

5. 在**Driver files**窗格中，单击**Add**图标 并选择**Custom JARs**。

6. 在文件浏览器中，导航到 JDBC 驱动程序的 JAR 文件，选择它，然后单击**OK**。

7. 在**Class**字段中，指定要用于驱动程序的值。

8. 单击**应用**。

   ![将用户驱动程序添加到现有连接](http://127.0.0.1:63342/help/img/idea/2021.2/db_add_user_driver_to_connection.png)

## Step 4. 检查是否需要SSH或SSL连接﻿

为了更安全地连接到数据库，某些服务需要使用 SSH 或 SSL。

### 安全证书﻿

以下过程描述了适用于大多数数据库的 SSL 配置。对于某些数据库，您需要使用另一种方法才能成功连接。请参阅*教程*部分，其中包括[Apache Cassandra](http://127.0.0.1:63342/help/how-to-connect-to-cassandra-with-ssl.html)、[Heroku Postgres](http://127.0.0.1:63342/help/how-to-connect-to-heroku-postgres.html)和[MySQL 5.1 的](http://127.0.0.1:63342/help/cannot-connect-to-mysql-5-1.html)配置示例。

### 使用 SSL 连接到数据库﻿

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：

   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标。

2. 在“**数据源”**选项卡上，选择要修改的数据源。

3. 单击**SSH/SSL**选项卡并选中**使用 SSL**复选框。

4. 在**CA 文件**字段中，导航到 CA 证书文件（例如，**mssql.pem**）。

5. 在**客户端证书文件**字段中，导航到客户端证书文件（例如，**client-cert.pem**）。

6. 在**客户端密钥文件**字段中，导航到客户端密钥文件（例如，**client-key.pem**）。

7. 从**模式**列表中，选择验证模式：

   - **要求**：验证服务器是否接受此 IP 地址的 SSL 连接并识别客户端证书。
   - **验证 CA**：通过检查证书链直到存储在客户端上的根证书来验证服务器。
   - **完全验证**：验证服务器主机以确保它与存储在服务器证书中的名称匹配。如果无法验证服务器证书，则 SSL 连接失败。

8. 为确保与数据源的连接成功，请单击**测试连接**。

   ![使用 SSL 连接到数据库](http://127.0.0.1:63342/help/img/idea/2021.2/db_connect_with_ssl.png)

> 建议使用 PEM 证书。

> 使用自签名证书以及在某些情况下使用受信任的根实体颁发的证书，您在使用最新的 JDBC 驱动程序版本时可能会遇到错误。如果您的 Java 密钥库不接受证书链，则 SSL 连接可能会失败。作为临时解决方案，尝试降级JDBC驱动程序（例如，对于MySQL连接器，您需要切换到5.1.40版本。）

### 禁用与数据库的 SSL 连接﻿

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：
   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标
2. 在“**数据源”**选项卡上，选择要修改的数据源。
3. 单击**SSH/SSL**选项卡并清除**使用 SSL**复选框。
4. 单击**应用**。

### 从其他数据源复制 SSL 设置﻿

如果为一个数据源配置了 SSL 设置，则可以为另一个数据源复制这些设置。

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：

   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标

2. 在“**数据源”**选项卡上，选择要修改的数据源。

3. 单击**SSH/SSL**选项卡并选中**使用 SSL**复选框。

4. 单击**从**链接**复制**并选择要复制的配置。

   ![复制 SSL 设置](http://127.0.0.1:63342/help/img/idea/2021.2/db_copy_ssl_settings.png)

### SSH﻿

> 配置 SSH 设置后，在**常规**选项卡上，使用主机地址和数据库端口，而不是`localhost`.

Secure Shell 或 SSH 是一种网络协议，用于加密客户端和服务器之间的连接。

所有创建的 SSH 连接都在项目中的所有数据源之间共享。如果您不想在项目之间共享连接，请在 SSH 连接设置中选中**仅对此项目可见**复选框。

![共享 SSH 连接设置](http://127.0.0.1:63342/help/img/idea/2021.2/db_ssh_connections_sharing.png)

### 使用 SSH 连接到数据库﻿

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：

   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标

2. 选择要更改连接设置的数据源配置文件。

3. 单击**SSH/SSL**选项卡并选中**使用 SSH 隧道**复选框。

4. 单击**添加 SSH 配置**按钮。

5. 在**SSH**对话框中，单击**添加**按钮。

6. 如果您不想在项目之间共享配置，请选中**仅对此项目可见**复选框。

7. 在**Host**、**User name**和**Port**字段中，指定您的连接详细信息。

8. 从**身份验证类型**列表中，您可以选择身份验证方法：

   - **密码**：使用**密码**访问主机。要在 DataGrip 中**保存密码**，请选中**保存密码**复选框。

   - **密钥对（OpenSSH 或 PuTTY）**：通过密钥对使用[SSH 身份验证](https://www.ssh.com/)。要应用此身份验证方法，您必须在客户端计算机上有一个私钥，在远程服务器上有一个公钥。DataGrip 支持使用[OpenSSH](https://www.openssh.com/)实用程序生成的私钥。

     指定存储*私钥*的文件的路径，并在相应字段中键入密码（如果有）。要让 DataGrip 记住密码，请选中**保存密码**复选框。

   - **OpenSSH 配置和身份验证代理**：使用由凭据帮助程序管理的 SSH 密钥（例如，Windows 上的[Pageant](https://the.earth.li/~sgtatham/putty/0.70/htmldoc/Chapter9.html#pageant)或macOS 和 Linux 上的[ssh-agent](https://en.wikipedia.org/wiki/Ssh-agent)）。

   ![数据源的 SSH 和 SSL 设置](http://127.0.0.1:63342/help/img/idea/2021.2/db_data_source_ssh_ssl_settings.png)

> 有关使用 SSH 密钥的详细信息，请参阅[生成新的 SSH 密钥并将其添加到 ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)教程。

### 禁用与数据库的 SSH 连接﻿

1. 打开数据源属性。您可以使用以下选项之一打开数据源属性：
   - 导航到**文件 | 数据源**。
   - 按Ctrl+Alt+Shift+S。
   - 在**数据库**工具窗口（**查看 | 工具窗口 | 数据库**）中，单击**数据源属性**图标。
2. 选择要更改连接设置的数据源配置文件。
3. 单击**SSH/SSL**选项卡并清除**使用 SSH 隧道**复选框。
4. 单击**应用**。

### 使用 PuTTY 创建 SSH 隧道 (Windows)﻿

1. 下载并运行最新版本的 PuTTY SSH 和 Telnet 客户端（从https://www.putty.org/下载客户端）。
2. 在**PuTTY 配置**对话框中，导航到**连接 | SSH | 验证**。
3. 在**用于身份验证的私钥文件**字段中，指定您的私钥文件的路径，然后单击**打开**。
4. 在命令行窗口中，指定用于 SSH 隧道的用户名，然后按Enter。不要关闭命令行窗口。
5. 在 DataGrip 中，导航到**文件 | 数据源** Ctrl+Alt+Shift+S。
6. 选择要更改连接设置的数据源配置文件。
7. 单击**SSH/SSL**选项卡并选中**使用 SSH 隧道**复选框。
8. 从**Auth type**列表中，选择**OpenSSH config and authentication agent**。
9. 在**Proxy host**、**Proxy user**和**Port**字段中，指定连接详细信息。
10. 为确保与数据源的连接成功，请单击**测试连接**。

![使用 PuTTY 创建 SSH 隧道 (Windows)](http://127.0.0.1:63342/help/img/idea/2021.2/db_putty_key_config.png)

### 使用 Pageant (Windows) 创建 SSH 隧道﻿

Pageant 是 PuTTY、PSCP、PSFTP 和 Plink 的 SSH 身份验证代理。Pageant 存储您的私钥，只要它在运行，它就会向 PuTTY 或其他工具（如 DataGrip）提供解锁的私钥。您可以在 Windows 任务栏中找到 Pageant 图标。

1. 下载最新版本的 Pageant（从https://www.putty.org/下载客户端）。
2. 在 Windows 任务栏中，右键单击 Pageant 图标并选择**Add Key**。
3. 在“**选择私钥文件”**对话框中，导航到私钥文件（PPK 文件）并单击“**打开”**。
4. （可选）输入私钥密码，然后按Enter。
5. 在 DataGrip 中，导航到**文件 | 数据源** Ctrl+Alt+Shift+S。
6. 选择要更改连接设置的数据源配置文件。
7. 单击**SSH/SSL**选项卡并选中**使用 SSH 隧道**复选框。
8. 从**Auth type**列表中，选择**OpenSSH config and authentication agent**。
9. 在**Proxy host**、**Proxy user**和**Port**字段中，指定连接详细信息。
10. 为确保与数据源的连接成功，请单击**测试连接**。

![使用 Pageant (Windows) 创建 SSH 隧道](http://127.0.0.1:63342/help/img/idea/2021.2/db_task_area_pageant.png)

### 使用 ssh-agent（macOS 和 Linux）创建 SSH 隧道﻿

在命令行中运行 ssh-agent 的所有命令。

1. 确保 ssh-agent 正在运行。

   ```none
   ssh-agent
   ```

   已复制！

2. 将您的密钥添加到代理（在以下示例中，密钥路径为**~/.ssh/id_rsa**）。

   ```none
   ssh-add ~/.ssh/id_rsa
   ```

   已复制！

3. （可选）在 macOS 上，您可以`-K`向`ssh-add`命令添加选项以将密码短语存储在您的钥匙串中。在 macOS Sierra 及更高版本上，您需要在**~/.ssh/ 中**使用以下文本创建**配置**文件：

   ```none
   Host *
   UseKeychain yes
   AddKeysToAgent yes
   IdentityFile ~/.ssh/id_rsa
   ```

   已复制！

   如果**.ssh**目录中有其他**私钥**，请`IdentityFile`为每个密钥添加一行。例如，如果第二个密钥的名称为**id_ed25519**，则为第二个私钥添加`IdentityFile ~/.ssh/id_ed25519`一行。

4. 列出所有添加的键。

   ```none
   ssh-add -L
   ```

   已复制！

5. 在 DataGrip 中，导航到**文件 | 数据源** Ctrl+Alt+Shift+S。

6. 选择要更改连接设置的数据源配置文件。

7. 单击**SSH/SSL**选项卡并选中**使用 SSH 隧道**复选框。

8. 从**Auth type**列表中，选择**OpenSSH config and authentication agent**。

9. 在**Proxy host**、**Proxy user**和**Port**字段中，指定连接详细信息。

10. 为确保与数据源的连接成功，请单击**测试连接**。

![使用 ssh-agent（macOS 和 Linux）创建 SSH 隧道](http://127.0.0.1:63342/help/img/idea/2021.2/db_ssh_agent_linux_macos.png)

# 参考

### 什么是SSL?

SSL(Secure Sockets Layer [安全套接字协议](https://baike.baidu.com/item/安全套接字协议)),及其继任者[传输层安全](https://baike.baidu.com/item/传输层安全)（Transport Layer Security，TLS）是为[网络通信](https://baike.baidu.com/item/网络通信/9636548)提供安全及[数据完整性](https://baike.baidu.com/item/数据完整性/110071)的一种安全协议。TLS与SSL在[传输层](https://baike.baidu.com/item/传输层/4329536)与[应用层](https://baike.baidu.com/item/应用层/16412033)之间对网络连接进行加密。

### SSL作用机制

当前版本为3.0。它已被广泛地用于[Web浏览器](https://baike.baidu.com/item/Web浏览器)与服务器之间的[身份认证](https://baike.baidu.com/item/身份认证)和加密数据传输。

SSL协议位于[TCP/IP协议](https://baike.baidu.com/item/TCP%2FIP协议)与各种[应用层协议](https://baike.baidu.com/item/应用层协议/3668945)之间，为[数据通讯](https://baike.baidu.com/item/数据通讯)提供安全支持。[SSL协议](https://baike.baidu.com/item/SSL协议/4602579)可分为两层： SSL记录协议（SSL Record Protocol）：它建立在可靠的[传输协议](https://baike.baidu.com/item/传输协议)（如TCP）之上，为高层协议提供[数据封装](https://baike.baidu.com/item/数据封装)、压缩、加密等基本功能的支持。 SSL[握手协议](https://baike.baidu.com/item/握手协议)（SSL Handshake Protocol）：它建立在SSL记录协议之上，用于在实际的数据传输开始前，通讯双方进行[身份认证](https://baike.baidu.com/item/身份认证)、协商[加密算法](https://baike.baidu.com/item/加密算法)、交换加密[密钥](https://baike.baidu.com/item/密钥)等。

其作用：

（1）认证用户和服务器，确保数据发送到正确的[客户机](https://baike.baidu.com/item/客户机)和[服务器](https://baike.baidu.com/item/服务器)；

（2）加密数据以防止数据中途被窃取；

（3）维护数据的完整性，确保数据在传输过程中不被改变。

### 什么是SSH?

SSH 为 [Secure Shell](https://baike.baidu.com/item/Secure Shell) 的缩写，由 IETF 的网络小组（Network Working Group）所制定；SSH 为建立在应用层基础上的安全协议。SSH 是较可靠，专为[远程登录](https://baike.baidu.com/item/远程登录/1071998)会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。SSH最初是UNIX系统上的一个程序，后来又迅速扩展到其他操作平台。SSH在正确使用时可弥补网络中的漏洞。[SSH客户端](https://baike.baidu.com/item/SSH客户端/7091372)适用于多种平台。几乎所有UNIX平台—包括[HP-UX](https://baike.baidu.com/item/HP-UX)、[Linux](https://baike.baidu.com/item/Linux)、[AIX](https://baike.baidu.com/item/AIX)、[Solaris](https://baike.baidu.com/item/Solaris/3517)、[Digital](https://baike.baidu.com/item/Digital) [UNIX](https://baike.baidu.com/item/UNIX)、[Irix](https://baike.baidu.com/item/Irix)，以及其他平台，都可运行SSH。

### SSH功能

传统的网络服务程序，如：[ftp](https://baike.baidu.com/item/ftp)、pop和[telnet](https://baike.baidu.com/item/telnet)在本质上都是不安全的，因为它们在网络上用[明文](https://baike.baidu.com/item/明文)传送口令和数据，别有用心的人非常容易就可以截获这些口令和数据。而且，这些服务程序的[安全验证](https://baike.baidu.com/item/安全验证)方式也是有其弱点的， 就是很容易受到“中间人”（man-in-the-middle）这种方式的攻击。所谓“中间人”的攻击方式， 就是“中间人”冒充真正的[服务器](https://baike.baidu.com/item/服务器)接收你传给服务器的数据，然后再冒充你把数据传给真正的服务器。服务器和你之间的数据传送被“中间人”一转手做了手脚之后，就会出现很严重的问题。通过使用SSH，你可以把所有传输的数据进行加密，这样"中间人"这种攻击方式就不可能实现了，而且也能够防止DNS欺骗和IP欺骗。使用SSH，还有一个额外的好处就是传输的数据是经过压缩的，所以可以加快传输的[速度](https://baike.baidu.com/item/速度/5456)。SSH有很多功能，它既可以代替[Telnet](https://baike.baidu.com/item/Telnet)，又可以为[FTP](https://baike.baidu.com/item/FTP)、[PoP](https://baike.baidu.com/item/PoP)、甚至为[PPP](https://baike.baidu.com/item/PPP)提供一个安全的"通道"。
