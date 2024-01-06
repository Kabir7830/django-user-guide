# Getting Started with Django

1) Install the latest verison of Python and add it to the environmental variable
2) Create a directory in you PC where you want to build the project
3) Open windows powershell in the same directory
4) create a virtual environment using the command
	
 		python -m venv vitrualenv

5) Now activate the virtualenv using the following command

   		/virtualenv/scripts/activate

7) If you encountered any error then set the execution policy to remote signed using this command

   		set-ExecutionPolicy RemoteSigned
   	Then press "A"

8) After the virtiual env has been successfully activated. We are going to install the dependencies for our project
   Here are the required dependencies
   
   i) django==4.1<br>

	Install them using pip

		pip install django==4.1

 9) After successful installation of the dependencies, we are going to create our first project. To create the project write the following command
 	
  		django-admin startproject project_name
 
 10) A folder will be created to your directory with the name of the project given.
 11) Now move to this directory
	
			cd project_name
 
 12) Here you can see a folder with your project name and a manage.py file.
 13) Now we need to start the server to see your website. For that type the following Command

			python manage.py runserver
 
 15) This will start a server to your local network with a default IP 127.0.0.1:8000. Open this IP in your browser and boom your project is successfully made.

