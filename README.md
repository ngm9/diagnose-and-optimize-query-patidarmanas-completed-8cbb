# Task Overview

InsightsNow is a multi-tenant analytics SaaS product where customers upload large datasets for interactive dashboards and live reporting. Recently, support tickets have spiked due to performance degradations: users report delays in saving new events or updating dashboards, especially during periods of heavy analytics workloads (e.g., monthly report runs). Support staff noticed that analytical queries frequently block OLTP traffic in production, causing business outages and slowdowns for critical endpoints.

# Objectives
- Identify blocking relationships and sources of contention between OLTP/OLAP workloads using system views.
- Add or tune appropriate indexes, foreign keys, and constraints on high-volume tables.
- Optimize analytical queries and introduce materialized views or partitioning where needed.
- Implement query-level timeouts to prevent OLAP tasks from blocking crucial OLTP endpoints.
- Ensure new structure maintains transactional and data integrity for concurrent workloads.

# Database Access
- **Host**: <DROPLET_IP>
- **Port**: 5432
- **Database**: insightsnowdb
- **Username**: insightsuser
- **Password**: insightspass

You may use any PostgreSQL client (psql, DBeaver, pgAdmin, DataGrip) for connection, schema analysis, and performance diagnostics. System is preloaded with realistic event data and typical reporting/analytic workloads.
### How to Verify
- Use database inspection tools to observe that the most common transactional operations proceed with fewer delays after your adjustments.
- Compare behavior of representative reporting queries to see whether results appear more promptly or place less strain on active OLTP paths.
- Generate typical workloads and confirm that audit and event information remains consistent and complete even when activity increases.
- Review system views again to verify reduced blocking patterns and more stable performance under concurrent operations.
- Document the key refinements made and reflect on how each change affected overall workload balance.

### Helpful Tips
- Use PostgreSQL’s monitoring views to understand where blocking typically originates between transactional and reporting workloads. Focus on identifying patterns, not mapping every detail.
- Inspect the structure of the highest-traffic tables to spot areas where indexing or relational design may not fully support the operations hitting them most often.
- Evaluate the SQL used for real-time event operations and heavier reporting processes to see which queries could benefit from refinements or restructuring.
- Consider whether simple range or list partitioning may help reduce scan sizes or minimize contention on very active tables.
- For resource-intensive reporting, think about how materialized views could offload repeated calculations and how refresh strategies might fit into ongoing activity.
