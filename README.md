# MagnaTech SLA Performance Analysis

## Business Overview
MagnaTech is a fictional technology services company that manages a centralized support desk responsible for handling customer and internal service tickets across multiple channels. The support team operates under defined Service Level Agreements (SLAs) that require tickets to receive timely responses and resolution.

Maintaining high SLA compliance is vital to ensure operational reliability, maintain customer trust, and manage internal service efficiency.

This analysis evaluates ticket performance using 2,312 support ticket processes during the analysis period. The dataset was cleaned and aggregated using SQL, and visualised in Tableau to simulate how operational teams assess SLA performance and service quality.

#### The Problem:
As ticket volume grows, MagnaTech must ensure that operational performance remains consistent across agents, ticket priorities, and time periods. The Head of Operations requires a structured analysis to identify emerging performance risks or opportunities for process improvement.

#### Key Metrics:
- Is SLA performance consistent across agents?
- Are certain ticket priorities more prone to compliance?
- Does workload volume influence SLA compliance?
- Are operational metrics aligned with customer satisfaction?

## Analysis Performed
Exploratory analysis was conducted and analytical views created using MySQL. Key queries answered the following:
- Overall SLA compliance levels
- Ticket volume distribution
- Agent performance metrics
- SLA compliance by ticket priority
- Monthly service performance trends

[*Check out sql queries*](sql/magnatech_sla_analysis.md)

## Insights Discovered

#### Key Insights:
- Total Tickets Analyzed: 2,312
- Average SLA Compliance: 96.5%
- Average Customer Satisfaction: 3.5 out of 5

*Dashboard image to be uploaded*

| Metrics | Insight |
| ------- | ------- |
| Compliance by Priority | Insight shows high-priority tickets at 96.7% compliance, followed by low-priority at 96.6%, and medium-priority at 95.8%. This shows that high-priority tickets are handled most effectively, while medium-priority tickets show slightly weaker compliance than the others. | 
| Compliance by Agent | Insight shows compliance falls within a narrow range of 95.5% - 97.2%, indicating generally consistent operational performance across the support team. Sheela achieved the highest compliance (97.2%) while handling one of the largest ticket volumes, suggesting strong efficiency under workload pressure. Nicola (95.6%) and Heather (95.5%) recorded the lowest compliance rates, with a relatively small difference between the two. |
| Monthly Compliance vs Workload | The insight shows an early-year volatility. SLA compliance dipped below 95% during the early months (February, April, May) of the year, having 94.9%, 94.7%, 94.1% compliance, respectively. The line chart shows performance stabilizing significantly in the second half of the year, reaching 98.2% in December. May recorded the lowest compliance (94.1%) with a high ticket volume (219 tickets). This suggests that spikes in workload may place pressure on response times. |
| Compliance vs Customer Satisfaction | Despite a strong compliance average of 96.5%, customer satisfaction averages 3.5 out of 5. This indicates that meeting response-time SLAs alone may not fully determine/improve customer experience outcomes. |

## Business Implication
First, MagnaTech's support operations demonstrate strong SLA discipline, and the narrow performance range among agents indicates that operational procedures and processes are generally standardized and effective. However, workload fluctuation can introduce short-term volatility, especially during higher ticket volume periods. Most importantly, the gap between compliance and customer satisfaction suggests that service quality beyond response speed may influence customer perception.

## Recommendations
- Monitor agent workload distribution to maintain consistent SLA performance during high-volume periods.
- Review triage processes and workflow prioritisation to ensure balanced performance across ticket types.
- Incorporate additional performance indicators to better understand satisfaction outcomes.
- Implement multi-year performance tracking to determine whether early-year volatility observed reflects a seasonal pattern or operational transitions.

## Tools
- MySQL: Data cleaning, aggregations, and exploratory data analysis (EDA).
- Tableau: Dashboard development and visualisation.

*Checkout Analytical Skills Demonstrated(LINK)* 

