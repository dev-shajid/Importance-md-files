# Some Django Admin


## show image in Django admin 
```python
> Model.py

from django.utils.html import format_html

class Post(models.Model):
    image = models.ImageField(upload_to="post/",blank=True,null=True)    
    
    def showimage(self):
        return format_html('<img width="70" height="50" src="/media/%s" />' % self.image)

> Admin.py


admin.AdminSite.site_header = "Welcome Rafiq"
admin.AdminSite.site_title = "rafiq"
admin.AdminSite.index_title = "Rafiq Blog"
    
class PostAdmin(admin.ModelAdmin):    
    list_display = ('id','title','date','showimage')
admin.site.register(Post,PostAdmin)
```
