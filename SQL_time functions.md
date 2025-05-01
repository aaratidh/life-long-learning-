
---

```markdown
# SQL Date and Time Functions

## Table of Contents

  - [CURRENT_TIME](#current_time)
  - [CURRENT_DATE](#current_date)
  - [CURRENT_TIMESTAMP](#current_timestamp)
  - [NOW()](#now)
  - [Date Formatting Functions](#date-formatting-functions)
  - [Date Arithmetic](#date-arithmetic)
  - [Date Truncate and Rounding](#date-truncate-and-rounding)
  - [Casting and Conversions](#casting-and-conversions)
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

### Date Formatting Functions

**TO_CHAR** – Converts date to string in desired format.

```sql
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD HH24:MI') AS formatted_datetime;
-- Output:
formatted_datetime  
2025-04-30 15:45
```

**EXTRACT** – Extract part of a date.

```sql
SELECT EXTRACT(YEAR FROM NOW()) AS current_year;
-- Output:
current_year  
2025
```

**T-SQL Equivalents:**
```sql
FORMAT(GETDATE(), 'yyyy-MM-dd HH:mm');
DATEPART(YEAR, GETDATE());
```

---

### Date Arithmetic

**PostgreSQL:**
```sql
SELECT NOW() + INTERVAL '5 days';
SELECT NOW() - INTERVAL '5 days';
SELECT AGE(NOW(), '2025-01-01');
```

**T-SQL:**
```sql
SELECT DATEADD(DAY, 5, GETDATE());
SELECT DATEADD(DAY, -7, GETDATE());
SELECT DATEDIFF(DAY, '2025-01-01', GETDATE());
```

---

### Date Truncate and Rounding

**PostgreSQL:**
```sql
SELECT DATE_TRUNC('month', NOW());
SELECT DATE_TRUNC('day', NOW());
-- Output: '2025-04-01 00:00:00'
```

**T-SQL:**
```sql
SELECT CAST(GETDATE() AS DATE);
SELECT FORMAT(GETDATE(), 'yyyy-MM-dd');
-- Output: '2025-04-01'
```

---

### Casting and Conversions

**PostgreSQL:**
```sql
SELECT TO_DATE('2025-04-30', 'YYYY-MM-DD');
SELECT TO_CHAR(NOW(), 'YYYY-MM-DD');
-- Output: '2025-04-30'
```

**T-SQL:**
```sql
SELECT CAST('2025-04-30' AS DATE);
SELECT FORMAT(GETDATE(), 'yyyy-MM-dd');
-- Output: '2025-04-30'
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
