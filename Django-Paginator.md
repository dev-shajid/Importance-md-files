# Django-Paginator

```
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
False
>>> p1.has_next()
True
>>> p1.next_page_number()
2
>>>
```
```
class HomeView(ListView):
    model = Post
    template_name='blog/home.html'
    context_object_name = 'posts'
    ordering=['-date_posted']
    paginate_by = 2
    
  http://127.0.0.1:8000/?page=2

___
  {% if is_paginated %}      

        {% if page_obj.has_previous %}
            <a class='btn btn-outline-info mb-4' href="?page=1">First</a>
            <a class='btn btn-outline-info mb-4' href="?page={{ page_obj.previous_page_number }}">Previous</a>
        {% endif %}   

      {% for num  in page_obj.paginator.page_range %}            
            {% if page_obj.number == num %}
            <a class='btn btn-info mb-4' href="?page={{ num }}">{{ num }}</a>
             {% elif num > page_obj.number|add:'-2' and num < page_obj.number|add:'2' %}   
            <a class='btn btn-outline-info mb-4' href="?page={{ num }}">{{ num }}</a>
            {% endif %}                
        {% endfor %} 
    


        {% if page_obj.has_next %}
            <a class='btn btn-outline-info mb-4' href="?page={{ page_obj.next_page_number }}">Next</a>
            <a class='btn btn-outline-info mb-4' href="?page={{ page_obj.paginator.num_pages }}">Last</a>
        {% endif %}  

    {% endif %}
  
  
```
