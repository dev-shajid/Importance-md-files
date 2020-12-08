# Django Rest API Some Note


> Override <b>Serializer</b>

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


> Override <b>Viewsets</b>

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

> Token Auth

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
