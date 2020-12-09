# Django Rest API Some Note


## Override Serializer

```python
    class ItemSerializer(serializers.ModelSerializer):
        category = serializers.SerializerMethodField()
        label = serializers.SerializerMethodField()
        class Meta:
            model = Item
            fields = "__all__"
        def get_category(self,obj):
            return obj.get_category_display()
        def get_label(self,obj):
            return obj.get_label_display()
```


## Override Viewsets

```python
    def list(self, request):
        company = Medicine.objects.all()
        serializer = MedicineSerializers(company, many=True, context={"request": request})

        medicine_data = serializer.data
        newmedicinelist=[]
        # Adding Extra Key for Medicine Details in Medicine
        for medicine in medicine_data:
            # Accessing All the Medicine Details of Current Medicine ID
            medicine_details = MedicalDetails.objects.filter(medicine_id=medicine['id'])
            medicine_details_serializer = MedicalDetailserializersSimple(medicine_details,many=True)
            medicine["medicine_details"] = medicine_details_serializer.data
            newmedicinelist.append(medicine)

        response_dict = {"error": False, "message": "All Company CompanyBank Data", "data": newmedicinelist}
        return Response(response_dict)
```

## Token Auth

```python
    from django.contrib import admin
    from django.urls import path, include, re_path
    from django.views.generic import TemplateView
    from rest_framework.authtoken.views import obtain_auth_token
    from django.conf import settings
    from django.conf.urls.static import static



    urlpatterns = [
        path('admin/', admin.site.urls),
        path('api/login/',obtain_auth_token),
    ]

    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
        urlpatterns += [
            re_path(r'^.*', TemplateView.as_view(template_name='index.html')),
        ]

    if not settings.DEBUG:
        urlpatterns +=[
            re_path(r'^.*', TemplateView.as_view(template_name='index.html')),
        ]
```
## Auto input User in Serializer

```python

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model  = Post
        fields = "__all__"
        read_only_fields = ['author']
        
    def validate(self,obj):
        obj['author'] = self.context['request'].user
        return obj
```
## Some Importent Inports
```python
from rest_framework.status import HTTP_200_OK, HTTP_400_BAD_REQUEST

from  django.shortcuts import get_object_or_404

from rest_framework.status import HTTP_200_OK

from rest_framework.response import Response

from rest_framework import viewsets

from rest_framework.views import APIView

order_item, created = OrderItem.objects.get_or_create()
```
## Token Auth serializer
```python
from rest_framework import serializers, fields
from django.contrib.auth import get_user_model
from .models import Post, Profile
from rest_framework.authtoken.models import Token


User = get_user_model()
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ('id', 'username', 'password','first_name','last_name','email')
        extra_kwargs = {'password': {'write_only': True, 'required': True}}

    def create(self, validated_data):
        user = User.objects.create_user(**validated_data)
        Token.objects.create(user=user)
        Profile.objects.create(user=user)
        return user
```
## Token Auth Viewset
```python


class UserViewset(APIView):
    qureryset = User.objects.all()
    permission_classes = (AllowAny, )
    def post(self,request):
        serializers = UserSerializer(data=request.data)
        if serializers.is_valid():
            serializers.save()
            return Response({"error":False,"message":"Update Success full","data":serializers.data})
        return Response({"error":True,"message":"A user with that username already exists! Try Anather Username"})

```

