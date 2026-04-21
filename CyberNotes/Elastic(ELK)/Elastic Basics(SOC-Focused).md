
##  What is ELK?

ELK stands for:
- **Elasticsearch** → stores & searches data
- **Logstash** → processes/ingests data
- **Kibana** → visualizes & searches data
Together, they form a **SIEM platform** for analyzing logs.
## Key Components
### Elasticsearch
- Database for logs
- Fast search & indexing
- Stores structured/unstructured data
###  Logstash
- Collects & processes logs
- Transforms data before storage
###  Kibana
- Interface for analysts
- Used to:
    - Search logs
    - Build dashboards
    - Investigate incidents
### 🚚Beats (Important)
Lightweight agents used to ship data:
- Filebeat → log files
- Metricbeat → system metrics
- Winlogbeat → Windows logs
 Equivalent to **Splunk Forwarders** 
##  KQL (Kibana Query Language)
Used to search and filter logs in Kibana.
##  Types of Searches
### 1. Free Text Search

```
security
```

- Searches all fields
- Returns any log containing the term
### 2. Wildcards
```
United*
```
- Matches variations of a term
- Useful for pattern matching
### 3. Logical Operators
#### AND

```
"United States" AND "Virginia"
```

Both conditions must be true
#### OR

```
"United States" OR "England"
```

Either condition can be true
#### NOT
```
"United States" AND NOT "Florida"
```

Excludes specific results
### 4. Field-Based Search (MOST IMPORTANT)

```
Source_ip: 238.163.231.224 AND UserName: Suleman
```

 Format:

```
Field : Value
```

- More precise than free text
- Used in real investigations
## SOC Analyst Thinking (Using KQL)

Instead of:

> “Search random stuff”

Think:

> “What question am I trying to answer?”

###  Example Questions

- Who accessed a system?
- What IP is suspicious?
- What user performed an action?
- What logs match this pattern?
##  Investigation Workflow (Elastic)

1. Identify suspicious indicator (IP, user, file)
2. Search using KQL
3. Filter using fields (IP, username, etc.)
4. Correlate multiple conditions
5. Build a timeline/story

##  Important Notes
- KQL searches **exact terms** (unless wildcard used)
- Free text = broad search
- Field-based = precise search
- Logs alone ≠ malicious → need context
##  Key Insight

> ELK is not just a tool—it’s a way to ask questions about data.

## Comparison to Splunk

|Concept|Elastic (ELK)|Splunk|
|---|---|---|
|Data Shipper|Beats|Forwarders|
|Query Language|KQL|SPL|
|Interface|Kibana|Splunk UI|

##  Summary
- ELK is a flexible SIEM platform
- KQL allows powerful log searching
- Field-based searches are critical
- Investigation = asking the right questions