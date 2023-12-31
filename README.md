# DJANGO-USER-GUIDE
This repo contains the guide to use the django features, these are the commonly used features rest of the details can be seen on the django official documentation site. <a href="https://docs.djangoproject.com/en/4.2/">Django Docs<a/>



# How to connect django with SQL servre?
This works with the django version 4.1 and below so make sure you have the related versions.

	pip install django==4.1
	pip install django-mysql
	pip install mysqlclient

Then do the following changes in the __settings.py__

	  DATABASES = {
		'default': {
			'ENGINE': 'django.db.backends.mysql',
			'NAME': 'databaseName',
			'USER': 'root',
			'PASSWORD': '',
			'HOST' : 'localhost',
			'PORT' : '3306',
			'OPTIONS' : {
				'init_command':"SET sql_mode='STRICT_TRANS_TABLES'",
			}
	
		}
	}

Reference: <a href="https://docs.djangoproject.com/en/4.2/ref/databases/">Django Databases</a>


# How To Create the Custom User Model in django?

Write this in __models.py__ file

	class CustomUserManager(BaseUserManager):
	    
		def create_user(self, email, password=None, **extra_fields):
			if not email:
				raise ValueError('The Email field must be set')
			email = self.normalize_email(email)
			user = self.model(email=email, **extra_fields)
			user.set_password(password)
			user.save(using=self._db)
			return user
	
	    def create_superuser(self, email, password=None, **extra_fields):
	        extra_fields.setdefault('is_staff', True)
	        extra_fields.setdefault('is_superuser', True)
	
	        return self.create_user(email, password, **extra_fields)
	
	class CustomUser(AbstractUser):
	    username = None  # Remove the username field
	
	    email = models.EmailField(unique=True)
	    first_name = models.CharField(max_length=30)
	    last_name = models.CharField(max_length=30)
	
	    # Add your additional fields here
	    date_of_birth = models.DateField(null=True, blank=True)
	
	    USERNAME_FIELD = 'email'
	    REQUIRED_FIELDS = ['first_name', 'last_name']  # Add any other required fields
	
	    objects = CustomUserManager()
	
	    def __str__(self):
	        return self.email

Now add __"AUTH_USER_MODEL = 'appname.CustomUser'"__ to your __settings.py__

Run the following commands to migrate the created user table

	python manage.py makemigrations
	python manage.py migrate

For more details about user model refer : <a href="https://docs.djangoproject.com/en/4.2/topics/db/models/">Django Models</a>

 
# How to use API in django?
First install the given dependencies

	pip install djangorestframework

Now create your models in your __models.py__ file

Now create __serializers.py__ file in your app. Then write the serializer classes as shown below
	
 	from rest_framework import serializers
	from .models import *
	
	class SeralizerName(serializers.ModelSerializer):
		class Meta:
			model = modelName
			fields = "__all__" 
   			#or fields = ["name","of","fields","to","include"]


Import the __serializer.py__ in your __views.py__

	from . serializer import *
 	from rest_framemork.views import APIView
  	from rest_framework.response import Response

   	class MyView(APIView):
    
		def get(self,request):
			objs = MyModel.objects.all()
   			serializer_class = SerializerName(objs,many=True)
      			return Response({"data":serializer_class.data})
	 
		def post(self,request):
    			serializer_class = SerializerName(data=request.data)
       			if serializer_class.is_valid():
	  			serializer_class.save()
      				return Response({"data":serializer_class.data})
	  		return Response({"error":serializer_class.errors})

		def put(self,request,id):
       			obj = MyModel.objects.filter(id = id).first()
	  		serializer_class = SerializerName(instance=obj,data=request.data)
     			if serializer_class.is_valid():
				serializer_class.save()
    				return Response({"data":serializer_class.data})
			return Response({"error":serializer_class.errors})
   
		def delete(self,request,id):
     			obj = MyModel.objects.filter(id = id):
			try:
   				obj.delete()
				return Response({"data":"deleted"})
    			except Exception as e:
       				return Response({"error":f"couldn't delete! ({e})"})
      
And our serializer is ready to use

Here is the full documentation for django-rest-frmework : <a href="https://www.django-rest-framework.org/">Django Restframework</a>


To learn the web development using Django signup for <a href="https://www.webxter.in">Webxter</a> and enroll for Django Course

