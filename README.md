# Social media project

### Project and App setup
* source activate myEnv
* django-admin startproject simplesocial
* django-admin startapp accounts
* Create templates and static within the main project directory
* Under static, you can have master css and application specific static files
* In settings.py file, 
    * Add the TEMPLATE_DIR
    * Register accounts under # simplesocial
    * TEMPLATE_DIR under TEMPLATES
    * Add STATICFILES_DIR at the end
* python manage.py migrate
* python manage.py makemigrations accounts
* python manage.py migrate
* python manage.py runserver to check 

### Home Page Initial Implementation
* Under templates, create base.html and index.html
* views.py under simplesocial project for index.html
* In urls.py, import views and include in the path

### Model of User in accounts app
* Import auth
* Inherit Django's builtin User and Permission model
* __str__() for string representation of the object 
    * username is coming from User model
* Connect to a view in accounts' views.py 
    * import reverse_lazy, CreateView and forms
* Create forms.py 
    * get_user_model: Return the User model that is active in this project
    * UserCreationForm to inherit from
    * Check out docs of Django to know more about it
    * labels is just setting up labels in HTML
* Come back to views.py of accounts and set the forms up
    * Normal reverse redirects without letting them signup
    * But reverse_lazy only when submitted
* Create templates under accounts app
* Under accounts dir of templates, create login and signup

#### Install Bootstrap 3
* pip install django-bootstrap3
* Then in settings.py file, in Installed Apps list add bootstrap3

#### Signup and Login of Accounts app
* Extend base.html and load bootstrap3

#### url.py of Accounts
* Import path, auth_views and App views
* auth_views is imported to use LoginView and LogoutView
* Setup paths for login, logout and signup
* Connect this urls.py to settings urls
    * include('django.contrib.auth.urls') for Django Auth

### base.html of main template
* Link bootstrap 3