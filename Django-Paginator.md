
>>> from django.core.paginator import Paginator
>>> posts = ['1','2','3','4','5','6','7']
>>> p = Paginator(posts, 2) 
>>> p
<django.core.paginator.Paginator object at 0x00000230EE5D7B20>
>>> p.num_pages
4   
>>> for page in p.page_range:
...     print(page) 
... 
1   
2   
3   
4   
>>> p1 = p.page(1) 
>>> 
>>> 
>>> p1
<Page 1 of 4>
>>> p1.number
1   
>>> p1.object_list
['1', '2']
>>> p1.has_previous()
False
>>>
