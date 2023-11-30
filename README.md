# DJANGO-USER-GUIDE
This repo contains the gudie to use the django features these are the commonly used features rest of the details can be seen on the django official documentation site.
# How to connect django with sql servre?
This works with the django version 4.1 and below so make sure you have the related versions<br>

	pip install django==4.1
	pip install django-mysql
	pip install mysqlclient

Then Do the following changes in the __settings.py__

	  DATABASES = {
		'default': {
			'ENGINE': 'django.db.backends.mysql',
			'NAME': 'allmagnus',
			'USER': 'root',
			'PASSWORD': '',
			'HOST' : 'localhost',
			'PORT' : '3306',
			'OPTIONS' : {
				'init_command':"SET sql_mode='STRICT_TRANS_TABLES'",
				}
	
			}
		}


# How To Create the Custom User Model in django?
Follow the steps<br>
__Creat a user model in models.py__ <br>
Here is the code

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

# How to use API in django?
First install the given dependencies

	pip install djangorestframework

Now create your models in your __models.py__ file

Now create __serializers.py__ file in your app. Then write the serializer classes as shown below
	
 	from rest_framework import serializers
	from .models import *
	
	class CourseSeralizer(serializers.ModelSerializer):
		class Meta:
			model = Courses
			fields = "__all__" 
   			#or fields = ["name","of","fields","to","include"]
And our serializer is ready to use



