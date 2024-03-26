Given the following relational scheme that describes patients associated with pathologies, and drugs associated with the same pathologies:

```
Patients (IdPz, NamePz , Surname, Sex, Date of Birth)
Pathologies Patients (IdPt *, IdPz *)
Pathologies(IdPt, NamePt, CategoryP)
Pathologies Drugs (IdPt *, IdD *)
Drugs (IdD, NameD, Principle, Dose, CategoryD, Price)
```

write the SQL queries that return the following information, without repetitions


a1) For all patients who are associated with some pathologies with CategoryP = ‘autoimmune’, return IdPz NamePz and Surname (61 rows)

```sql
select pz.IdPz, pz.NamePz, pz.Surname, pt.CategoryP
from PathologiesPatients pp join Patients pz on pp.IdPz=pz.IdPz
	join Pathologies pt on pt.IdPt=pp.IdPt
where CategoryP='autoimmune'
```
  ok

a2) For all patients who are only associated with pathologies with CategoryP = ‘autoimmune’, return IdPz NamePz and Surname (10 rows)

The quantification goes only between pp and pz.
Between pt and pp there is a unique id so it is not neede

WRONG
```sql
select pz.IdPz, pz.NamePz, pz.Surname, pt.CategoryP
from PathologiesPatients pp join Patients pz on pp.IdPz=pz.IdPz
	join Pathologies pt on pt.IdPt=pp.IdPt
where not exists(
	select *
	from PathologiesPatients pp join Patients pz on pp.IdPz=pz.IdPz
		join Pathologies pt on pt.IdPt=pp.IdPt
	where not (pt.CategoryP='autoimmune'))
```

CORRECT
```sql
select *
from Patients pz
where not exists(
	select *
	from PathologiesPatients pp
		join Pathologies pt on pp.IdPt=pt.IdPt
	where pz.IdPz=pp.IdPz and not (pt.CategoryP='autoimmune'))
```

b) For each CategoryD (drug category), return the number of all the pathologies that are associated with some drug of that category (3 rows)

```sql
select d.CategoryD, count (pt.IdPt)
from PathologiesDrugs pd
	join Drugs d on pd.IdD=d.IdD
	join Pathologies pt on pt.IdPt=pd.IdPt
group by d.CategoryD
```
ok
  

c) For each pair of pathologies that are different and have some drug in common, return the NamePt of the first and the NamePt of the second (362 or maybe 410 or 205)

WRONG
```sql
select pt1.NamePt, pt2.NamePt
from PathologiesDrugs pd
	join Pathologies pt1 on pt1.IdPt=pd.IdPt
	join Pathologies pt2 on pt2.IdPt=pd.IdPt
where pt1.IdD=pt2.IdD

```

```sql

```

d) For each pair of pathologies that are different and have some drug in common, return the NamePt of the first and the NamePt of the second, and the number of drugs in common (362 rows)

  
  

e) For each CategoryP (category of pathology), return the category and the number of patients associated with some pathology of that category (3 rows)

  
  

f1) Return the name of patients who are affected by some pathology for which some drug exists that costs strictly less than 50 (44 rows)

  

f2) (Diificult) Return the name of patients who are only affected by pathologies for which some drug exists that costs strictly less than 50 (29 rows)

  

g) (Diificult) Indicate in English or in Italian, without using IT terms but only by referring to pathologies and drugs, what the following questions return. Try to be clear and unambiguous in the answer.

  
  
  

```sql
SELECT pt.NamePt

FROM Pathologies pt

WHERE NOT EXISTS (SELECT *

    FROM PathologiesDrugs pd JOIN Drugs d USING (IdD)

    WHERE pd.IdPt = pt.IdPt and d.Dose> 10 and d.Price <100

)
```

Do not talk about joins and tables. Speak to the final user.
If it was without `and d.Dose> 10`,



  

```sql
SELECT pt.NamePt

FROM Pathologies pt JOIN PathologiesDrugs pd USING (IdPt)

WHERE NOT EXISTS (SELECT *

    FROM Drugs d

    WHERE pd.IdD = d.IdD AND d.Dose> 10 and d.Price <100

)
```

