# django-user-guide
This repo contains the gudie to use the django features these are the commonly used features rest of the details can be seen on the django official documentation site.

# Using the APIs in django
To use the APIs in feature the best way to do is to use the rest_framework 
(python -m pip install djangorestframework)

# Now to use the API you have to first create the models and then the serializer classes which converts the data into json format
## To do so
from rest_framework import serializer
<br><br>
class serializerName(serializer.ModelSerializer)
<br>#here we are using the modelserializer there are other serializers also reffer to doganjoprojects.com
<br>
&nbsp;&nbsp;&nbsp;class Meta:
    <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;model = modelName
    <br>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fields = ["name","of","fields","to","include"] # or use fields = "\_\_all\_\_" to select all fields
<br><br>
And our serializer is ready to use

