## SQL problem：
### find all supervisors who has more than 4 employees under him 
** （include directly under and undirectly under） **
** hierarchy structure **
------my code----
```
with CTE(sup_id,emp_id) as
(
select distinct sup_id ,emp_id=sup_id from  [dbo].[EMPLOYEE] e 
where sup_id is not null
union all
select CTE.sup_id, t.emp_id
from [dbo].[EMPLOYEE] t join CTE
on t.sup_id=CTE.emp_id )
,CTE2(sup_id,emp_num) as
(
   select sup_id,emp_num=count(*)-1  from CTE 
   group by sup_id
   having count(*)-1>=4
)
select CTE2.sup_id,a.name,CTE2.emp_num
from CTE2 left join [dbo].[EMPLOYEE] a
on CTE2.sup_id=a.emp_id
```
