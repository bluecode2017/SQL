### SQL query scenario： find all supervisors who has more than 4 employees directly under him from source table [dbo].[EMPLOYEE]
** directly under **
-- my code -----
```
with CTE as
(
select supervisor_employee_id,Total_employees_count=count(distinct employee_id)
from  [dbo].[EMPLOYEE]
group by supervisor_employee_id
having count(distinct employee_id)>=4
)
select CTE.supervisor_employee_id,a.name,CTE.Total_employees_count
from CTE 
left join 
[dbo].[EMPLOYEE] a
on CTE.supervisor_employee_id=a.employee_id
```
