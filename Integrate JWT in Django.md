# How to integrate JWT security in Django

install the below-mentioned dependencies

    pip install djangorestframework_simplejwt


Add this code sniped to your __settings.py__

    REST_FRAMEWORK = { 
        'DEFAULT_AUTHENTICATION_CLASSES': [ 
            'rest_framework_simplejwt.authentication.JWTAuthentication', 
        ], 
    }


Add this in your project's __urls.py__

    from django.urls import path, include 
    from rest_framework_simplejwt import views as jwt_views 
      
    urlpatterns = [ 
        path('api/token/', 
             jwt_views.TokenObtainPairView.as_view(), 
             name ='token_obtain_pair'), 
        path('api/token/refresh/', 
             jwt_views.TokenRefreshView.as_view(), 
             name ='token_refresh'), 
        path('', include('app.urls')), 
    ] 

Now send a __POST__ request to this api https://yoursite.com/api/token/ (https://120.0.0.1:8000/api/token/ -- for local host)

You will get two token __refresh token__ and __access token__

Use this access token to have to the pages send this token as __Bearer Token__ in the header

    Bearer_token: "token_value";
