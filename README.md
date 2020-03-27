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
* myNav,mycontent for custom CSS

### Login and Logout Redirect url in settings.pyt
* Bottom of settings.py, login and logout redirect url
* Create test and thanks templates in the main templates folder
* Need to set them up in views.py and urls.py file

### Groups and Post Applications
* django-admin startapp posts
* django-admin startapp groups
* Create templates/posts/post_base.html directly under posts
* We will also create post_detail, post_confirm_delete, post_form, post_list, user_post_list.html and _post.html
* _post.html will be used to inject this in other posts.html files
* Create urls.py and forms.py in posts
* Similarly create templates/groups directly under groups
* Then in templates create group_base.html, group_detail.html, group_form.html and group_list.html
* Create urls.py 

#### Groups models.py
* import slugify
    * Convert spaces to hyphens. Remove characters that aren't alphanumerics, underscores, or hyphens. Convert to lowercase. Also strip leading and trailing whitespace.
* pip install misaka
    * Allows md in posts
* get_user_model returns the User model that is active in this project
* import template from django and get template.Library() in register
    * Use custom template tags in the future
* group attribute of GroupMember is a foreign key to Groups and its related name will be memberships
* String representation of model will be called when a model is used in a template
* GroupMember connects Group and Users

#### Posts models.py
* User from get_user_model()
* auto_new=True sets the DateTimeField automatically when someone posts
* Meta class ordering is descending(that's what the - indicates)
* unique_together so that every message is uniquely linked to the User

#### Connecting Groups models to views
* Import Mixins required for Login and Permission
* Import reverse and generic
* 3 Views namely CreateView, DetailView and ListView
* In group_base.html, 3 blocks
* Next group_detail.html, where group is a context dictionary that comes from CBV
    * count attribute for members of group model
    * Leave or Join button, where content class is custom class
    * include is just like extends but we are doing it in the middle of the file
    * _post.html means this html file is gonna be injected somewhere
* Create urls.py for groups
* Register models in admin.py of groups
    * TablularInLine allows to edit models on the same page as the Parent model

#### Posts views.py
* pip install django-braces
* select_related for posts with user and group
* Then in urls.py of posts add the paths
* Next is templates for Posts pages
* get_user_groups in post_list.html comes from the Groups GroupMember models template library which we imported from django(related_name user_groups from GroupMember)
* Have no idea on where get_other_groups is coming from, maybe it is the complement of get_user_groups
* Filling _post.html file, we don't have to extend since we are injecting in the middle
* aria-hidden: Ignore the element and not read it out loud
    * aria for screenreaders used by people having disablities
* Next fill post_confirm_delete,user_post_list and post_detail

#### Groups views.py
* Add JoinGroup and LeaveGroup in views.py of groups
* Redirect from View by inheriting RedirectView
* Get model using method like get_object_or_404
* Connect the above 2 CBV to urls.py

#### Migrations and Debugging
* Add groups and posts app in settings.py file's INSTALLED_APPS
* python manage.py migrate
* python manage.py makemigrations groups
* python manage.py makemigrations posts
* python manage.py migrate
* python manage.py runserver
* Ran into some error while logging in, need to check
    * That is because simplesocial's settings.py and urls.py were not updated
* Next error in HomePage views.py of simplesocial
    * Resolved after making is_authenticated() to is_authenticated
* Another problem of Groups not being listed
    * This problem was due to incorrect code in group_list.html
* Finally correct the DIR to DIRS in settings.py

### Django Toolbar
* pip install django-debug-toolbar
* Django docs for django-debug-toolbar
* In settings.py
    * After staticfiles in INSTALLED_APPS, add 'debug_toolbar' before our custom apps
    * Add 'debug_toolbar.middleware.DebugToolbarMiddleware' to MIDDLEWARE
    * Add INTERNAL_IPS to point to localhost
* In project level urls.py file, concatenate url_patterns with debug url