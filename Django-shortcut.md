# Django-shortcut
 ```
rafiq@rrrr-PC:/mnt/c/users/rrrr/Desktop$
nano ~/.bashrc
source ~/.bashrc
```
```
mkvirtualenv --python=python3.8 myproject
```
```
Model.objects.all().order_by('-id')[:10]
obj=emp.objects.all()[:10]
```




```
python3 -m venv venv

python -m venv venv
```
```
source venv/bin/activate
source venv/Scripts/activate
pip freeze > requirements.txt
pip install -r requirements.txt
```
```
data.instance.user=self.request.user
```
```
winpty python manage.py createsuperuser
```

> {% static ' ' %}


virtualenv venv


pip install -r requirements.txt


touch filename.formate


rm <drname> -rf




prototype.gameOver = function() {console.log("TechSpartan")}




django to sql
sudo apt-get install python3-dev
pip install mysqlclient
sudo service mysql start


# Root
```
os.path.join(BASE_DIR,'templates')
```
```
STATIC_URL = '/static/'
STATICFILES_DIRS = (os.path.join(BASE_DIR,'staticfiles/', 'static'),)
STATIC_ROOT= os.path.join(BASE_DIR,'staticfiles/','staticroot/')
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR,'staticfiles/','media')
```
```
staticfiles/static

from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```





# Auto create profile after created User
```
from django.db.models.signals import post_save
from django.contrib.auth.models import User
from django.dispatch import receiver
from .models import Profile

@receiver(post_save, sender=User)
def create_user_profile(sender, instance, created, **kwargs):
    if created:
        Profile.objects.create(user=instance)

@receiver(post_save, sender=User)
def save_user_profile(sender, instance, **kwargs):
    instance.profile.save()
```
```
> if not work
> __init__.py
> default_app_config = 'user.apps.AccountsConfig'
```

```
> > Goto apps.py file

    def ready(self):
        import users.signals
```


# Redirects
```
LOGIN_REDIRECT_URL = 'client:user_profile request.user.id'
LOGIN_URL = '/path_to_the_page'
LOGOUT_REDIRECT_URL = 'login/'
```
# Outher 
```
pipenv shell ======for active vipenv virtualenv
pip freeze
```
