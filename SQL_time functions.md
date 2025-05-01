# SQL Date and Time Functions

## Table of Contents
- [PostgreSQL](#postgresql)
  - [CURRENT_TIME](#current_time)
  - [CURRENT_DATE](#current_date)
  - [CURRENT_TIMESTAMP](#current_timestamp)
  - [NOW()](#now)
- [T-SQL (SQL Server)](#t-sql-sql-server)
  - [GETDATE()](#getdate)
  - [SYSDATETIME()](#sysdatetime)
  - [DATETIMEOFFSET()](#datetimeoffset)

---


## PostgreSQL

### CURRENT_TIME

Gives current time with time zone value.  
**Output format:** `HH:MI:SS.MS+TZ`

**Example:**
```sql
SELECT CURRENT_TIME;
-- Output:
15:47:25.123456+00
```

We can also modify the format using the following:
```sql
SELECT TO_CHAR(CURRENT_TIME, 'HH24:MI:SS') AS current_time_formatted;
-- Output:
current_time_formatted  
15:47:25
```

---

### CURRENT_DATE

Gives current date **without time and without time zone**.  
**Output format:** `YYYY-MM-DD`

**Example:**
```sql
SELECT CURRENT_DATE;
-- Output:
2025-04-30
```

You can also format it like this:
```sql
SELECT TO_CHAR(CURRENT_DATE, 'MM/DD/YYYY') AS formatted_date;
-- Output:
formatted_date  
04/30/2025
```

---

### CURRENT_TIMESTAMP

Gives date in format `YYYY-MM-DD HH:MI:SS.MS+TZ`.  
Includes **date**, **time (with microseconds)**, and **timezone offset**.

**Example:**
```sql
SELECT CURRENT_TIMESTAMP;
-- Output:
2025-04-30 15:49:37.123456+00
```

---

### NOW()

Returns the current date and time (timestamp) at the moment the query is run.  
It is shorthand for `CURRENT_TIMESTAMP`.

**Example:**
```sql
SELECT NOW();
-- Output:
2025-04-30 16:00:45.123456+00
```

---

## T-SQL (SQL Server)

### GETDATE()

Returns the date and time from the **server**.  
Includes **milliseconds**.

**Example:**
```sql
SELECT GETDATE() AS current_datetime;
-- Output:
current_datetime  
2025-04-30 16:22:45.340
```

To format it into ISO format:
```sql
SELECT FORMAT(GETDATE(), 'yyyy-MM-ddTHH:mm:ss') AS iso_format;
-- Output:
2025-04-30T16:22:45
```

---

### SYSDATETIME()

Includes **date**, **time**, and **fractional seconds** up to 7 digits.  
Does **not include time zone info**.

**Output format:** `2025-04-30 21:29:11.3020621`

---

### DATETIMEOFFSET()

Gives current timestamp with **time zone offset** and **high precision time**.

**Example:**
```sql
DECLARE @dtOffset datetimeoffset = SYSDATETIMEOFFSET();
SELECT @dtOffset AS current_datetime_with_timezone;
-- Output:
current_datetime_with_timezone  
2025-04-30 14:45:30.1234567 -04:00
```

- High-precision time (7 digits)
- Time zone offset (`-04:00` for Eastern Daylight Time)
```

Let me know if you want this as a `.py`, `.txt`, or `.md` file again!
