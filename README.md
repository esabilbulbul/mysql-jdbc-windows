# mysql-jdbc-windows

MySQL8 Connection Problem on Windows 8

Author: Software Engineer @ www.shipshuk.com

If you are like me installed new Mysql version 8 on Windows 10, you will highly like to bump into the same problems. 
There are a few problems you might be facing when connecting 

Environment: Windows 10, Netbeans, MySQL10

1. SHA Security Algorith
MYSQL new version brought SHA security algorithm as oppose to the legacy connection in previous version. If you are using HeidiSQL for IDE 
you may need to disable this feature until HeidiSQL comes with support. If you are using Workbench you are fine. For HeidiSQL, the script is 

alter user root@'localhost' identified with mysql_native_password by '<your password>';

2. JDBC problem
The older than version 8 comes with mysql-connector-java-5.x.x-bin.jar package when the installation done. As of Aug 2018, the MSI installer for 
jdbc also comes with the same jar package. Therefore you need to download the new jar package to netbeans/IDE folder. The version as of the date 
I am using is mysql-connector-java-8.0.11.jar. You should copy this file into your IDE folder. I found the jar here on this link if you need
https://jar-download.com/download-handling.php

For Netbeans users, the driver location folder is C:\<Netbeans Root Path>\ide\modules\ext

3. JDBC Driver Problem (optional) (This wasn't the problem in my case)
Another problem you might run into will be the driver class. In previous version of MySQL the driver used is com.mysql.jdbc.Driver. Some texts on
mysql website says the driver class also change. However, I have managed to use with the older class. 
So in case you have problem, try to set up your jdbc connection with the new driver class. The old class name is com.mysql.jdbc.Driver. 
You might need to use the new driver class which is com.mysql.cj.jdbc.MysqlDataSource.

4. Timezone problem
When you are setting your jdbc URL you might be running into this problem like I did. Somehow, with mysql8 version, timezone is creating a problem
at connection. You need to specify your timezone in your jdbc URL. 

For Example;
jdbc:mysql://localhost:3306/mysql?serverTimezone=UTC

you will need to add "serverTimezone=UTC" piece into your url connection.

For Netbeans users, to define new driver to connect through Netbeans go to (See attachments NewDriver_step1.png and NewDriver_step2.png)
- Window (menu) -> Services 
- Right click on databases
- New Connection
- Choose MySQL (Connector / J Driver) on Driver options
- Update the jar file mentioned above
- Save

After completed the steps, go to (NewConnection.png)
- Window (menu) -> Services 
- Right click on databases
- New Connection
- Choose MySQL (Connector / J Driver)
- Next
- User Name & Pwd
- Add your jdbc URL (for example; jdbc:mysql://localhost:3306/mysql?serverTimezone=UTC)
- Next
- Next
- Finish

Hope this helps,


