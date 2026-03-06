## Initial Data Exploration
```sql
SELECT *
FROM response_time_sla_processed;
```

```sql
DESCRIBE
response_time_sla_processed;
```

```sql
SELECT ticket_id, COUNT(*)
FROM response_time_sla_processed
GROUP BY ticket_id
HAVING COUNT(*)>1;
```

```sql
ALTER TABLE response_time_sla_processed
ADD COLUMN created_datetime DATETIME;

UPDATE response_time_sla_processed
SET created_datetime=str_to_date(created_time,'%Y-%m-%d %H:%i:%s');
```

```sql
SELECT survey_results,
length(TRIM(survey_results)) as len 
FROM response_time_sla_processed
WHERE survey_results IS NOT NULL
AND (survey_results='' OR survey_results REGEXP '[^0-9.-]');

UPDATE response_time_sla_processed
SET survey_score = CASE
	WHEN survey_results REGEXP '^[0-9]+\\.?[0-9]*$'
		AND survey_results NOT LIKE ''
	THEN CAST(survey_results AS DECIMAL (5,2))
	ELSE NULL
END;
```

```sql
ALTER TABLE response_time_sla_processed
ADD COLUMN sla_compliant_flag INT;

UPDATE response_time_sla_processed
SET sla_compliant_flag = CASE
WHEN SLA_status ='Compliant' THEN 1
ELSE 0
END;
```

## Analytical Views
```sql
-- SLA by Priority
CREATE OR REPLACE VIEW sla_by_priority AS 
SELECT priority,
COUNT(*) AS ticket_count,
ROUND(avg(response_hours),2) AS avg_response_hours,
ROUND(avg(sla_compliant_flag)*100,2) AS sla_compliance_pct
FROM response_time_sla_processed
group by priority;
```

```sql
-- Agent Performance
CREATE OR REPLACE VIEW agent_performance AS
SELECT agent_name,
COUNT(*) AS ticket_volume,
ROUND(avg(response_hours),2) AS avg_response_hours,
ROUND(avg(sla_compliant_flag)*100,2) AS sla_compliant_pct,
ROUND(avg(survey_score),2) AS avg_satisfaction
FROM response_time_sla_processed
GROUP BY agent_name;
```

```sql
-- Monthly Trend
CREATE OR REPLACE VIEW monthly_sla_trend AS
SELECT MONTHNAME(created_datetime) AS ticket_month,
COUNT(*) AS monthly_volume,
ROUND(avg(response_hours),2) AS avg_response_hours,
ROUND(avg(sla_compliant_flag)*100,2) AS sla_compliant_pct
FROM response_time_sla_processed
GROUP BY MONTHNAME(created_datetime);
```

```sql
-- SLA Summary 
CREATE OR REPLACE VIEW sla_summary AS
SELECT 
COUNT(*) AS total_tickets,
ROUND(avg(response_hours),2) AS avg_response_hours,
ROUND(avg(sla_compliant_flag)*100,2) AS sla_compliant_pct,
ROUND(avg(survey_score),2) AS avg_satisfaction
FROM response_time_sla_processed;
```
