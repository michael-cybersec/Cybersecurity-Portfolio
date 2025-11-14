# SQL Security Cheat Sheet

## 📋 Overview
Quick reference guide for SQL security concepts, injection prevention, and secure coding practices.

---

## 🔐 SQL Injection Prevention

### ❌ Vulnerable Code
```python
query = "SELECT * FROM users WHERE username='" + username + "' AND password='" + password + "'"
```

### ✅ Secure Code (Parameterized Queries)
```python
query = "SELECT * FROM users WHERE username=? AND password=?"
cursor.execute(query, (username, password))
```

---

## 💾 Common SQL Injection Attacks

### 1. Authentication Bypass
```sql
' OR '1'='1
admin' --
' OR 1=1 --
```

### 2. Data Extraction
```sql
' UNION SELECT null, username, password FROM users --
' UNION SELECT null, column_name FROM information_schema.columns --
```

### 3. Time-Based Blind SQLi
```sql
' AND SLEEP(5) --
' AND IF(1=1, SLEEP(5), 0) --
```

### 4. Boolean-Based Blind SQLi
```sql
' AND 1=1 --
' AND 1=2 --
```

---

## 🛡️ Secure Practices

### 1. Input Validation
```python
def validate_username(username):
    if len(username) > 50:
        raise ValueError("Username too long")
    if not username.isalnum():
        raise ValueError("Invalid characters")
    return username
```

### 2. Prepared Statements (Python/SQLAlchemy)
```python
from sqlalchemy import text

query = text("SELECT * FROM users WHERE id = :user_id")
result = db.execute(query, {"user_id": user_id})
```

### 3. Stored Procedures
```sql
CREATE PROCEDURE GetUser @UserID INT
AS
BEGIN
    SELECT * FROM users WHERE id = @UserID
END
```

### 4. Least Privilege
```sql
CREATE USER 'app_user'@'localhost' IDENTIFIED BY 'strong_password';
GRANT SELECT, INSERT ON database.* TO 'app_user'@'localhost';
REVOKE DELETE, DROP ON database.* FROM 'app_user'@'localhost';
```

---

## 📊 Useful SQL Security Queries

### 1. Find Admin Users
```sql
SELECT username, role FROM users WHERE role='admin' OR is_admin=1;
```

### 2. Find Weak Passwords
```sql
SELECT username, password FROM users 
WHERE LENGTH(password) < 8 
OR password REGEXP '^[0-9]+$';
```

### 3. Audit Permissions
```sql
SELECT grantee, privilege_type FROM information_schema.role_table_grants 
WHERE is_grantable='YES';
```

---

**Last Updated:** November 2025
