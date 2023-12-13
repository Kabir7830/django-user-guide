# How to integrate JWT security in Django

install the below-mentioned dependencies

    pip install djangorestframework_simplejwt


Add this code sniped to your __settings.py__

    REST_FRAMEWORK = { 
        'DEFAULT_AUTHENTICATION_CLASSES': [ 
            'rest_framework_simplejwt.authentication.JWTAuthentication', 
        ], 
    } 
