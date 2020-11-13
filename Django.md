# Django
1. Language.objects.exclude(id=3) = = find everything without id =3.
2. Programmer.objects.filter(age__gt=20) = = find everything greater than 20.
3. Programmer.objects.filter(age__gte=20) == find everything greater than or equal 20.
4. Programmer.objects.filter(age__lt=20) == find everything less than 20.
5. Programmer.objects.filter(age__lte=20) == find everything less than or equal 20.
6. Programmers.objects.filter(name__contains='Re')  == find the names who contains=Re(case sensitive)
7. Programmers.objects.filter(name__icontains='re')  == find the names who contains=Re(case in sensitive)
8. Programmers.objects.filter(name__in=['Rafiq','Remon']  ==  it LIKE 6
9. Programmers.objects.filter(name__startswith='Re') == startswith
10. Programmers.objects.filter(name__endswith='Re') == endswith
11. .count() ==  Counts the object numbers
12. Programmers.objects.all()[:3] = = Get only 3 result
13. .order_by() = = Order bay
14. ManyToMany--Relationship
python = Language.objects.get(name='python’)’’ 
>>> python
```
<Language: python>
>>> python.programmers_set.all()
<QuerySet [<Programmers: Rafiq>]>


```



15. Model.objects.all().order_by('-id')[:10]
16. obj=emp.objects.all()[:10]
17. Lecture.objects.filter(section__cource__id=3) == ul>li>a>span
18. Aggregation=https://docs.djangoproject.com/en/3.0/topics/db/aggregation/ =>>> from django.db.models import Avg, Max, Min
```
>>> Book.objects.aggregate(Avg('price'), Max('price'), Min('price'))
{'price__avg': 34.35, 'price__max': Decimal('81.20'), 'price__min': Decimal('12.99')}
1. Django Humanize==1 becomes one, 2 becomes two.
2. modelformset_factory== model Form
```