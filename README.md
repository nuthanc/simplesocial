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

### Templates
* Under templates, create base.html and index.html
* views.py under simplesocial project for index.html