<meta http-equiv="content-type"
content="text/html;charset=utf-8" />





# Django 2.0.2  -- My notes

## Environment:  
 - Django 2.0.2  
 - Python 3.7.0   
 - Windows 10 - CMD   
    
  

## Initial Setup
 run the server to test it in the browser:   
   *python manage.py runserver*


 activate virtual enviroment (if windows):   
   *.\Scripts\activate  (run inside the parent folder of the project)*

 deactivate it with:   
   *.\Scripts\deactivate* 

 then start an app/feature in the src:  
   *python manage.py startapp nameOfApp*

The resulted folder will contain the views.py, that is used for visual content.
  
  

## rendering
- The views.py file of the django app will contain the visual content
of the project. Returning html content with a python fc inside of it:


*from django.http import HttpResponse*   
*def home(request):*   
   *return render(request, "home.html", {})*  
   *return HttpResponse("&lt;p&gt; hello from django! &lt;/p&gt;")*  

or render on-the-spot code:

*def home(request):*  
 *html_var = '398'*  
 *html_ = f""" < !DOCTYPE html >*  
 
 
 &lt;html lang=en&gt;   
 &lt;body&gt;    
 &lt;h1&gt; Hello from django! {html_var} &lt;/h1&gt;
 &lt;/body&gt;     
 &lt;/html&gt;       
 

 
 """
 *return HttpResponse(html_)*

- You can return much longer html content that will get rendered later on using
 """ instead of " and a local variable.



 
 
 ## urls
setting up urls in django 2: (!!!different 

*from nameOfApp.views import specificPageOfApp*   
*urlpatterns = [*   
   *path('', specificPageOfApp, name=specificPageOfApp)*  
*]*   



## templates
- create 'templates' folder in src  
- create new file 'home' as .html   
 "__ init__" should only import the settings file where the templates is mentioned    
(base.py)   
- in views.py use:  
    *def home(request):*    
     *return render(request, "base.html", {})*    





## contextVariable
- Work like procedures arguments. You transfer their value in the rendered html template  

- check python documentation    
- min 0:56:0   
  
- In views.py deal with the rendered content. The context variable works like a procedure parameter:   
*def home(request):*   
   *return render(request, "base.html", {"svar2": "context variable"})*

- In the html template use {{..}} :   
  text in html paragraph: *Base html: {{svar2}}*

- You can use a boolean variable inside the html template:  
 *{ % if svar2 != True% }*   
   *This is true*   
 *{ % endif % }*   
 
  
  

## templateInheritance
- Copy the rendering function, change the name   
- In urls.py include the procedures:    
   from restaurants.views import home, home2, home3    
- and add the paths:     
   *urlpatterns = [*  
    *path('admin/', admin.site.urls),*  
	*path('home',home, name='home'),*  
	*path('home2',home2, name='home2'),*  
	*path('home3',home3, name='home3'),*  
*]*
   
   
## blockContents  
- you can use snippets of code in several places in the project   
- embed the desired code inside:    
   *{% block content %}    //let's say the file is called index.html*    
      *your code to reuse*    
   *{% endblock content %}*   
   
- and fetch it with:    
   *{% extends "index.html" %}*  
   *{% block content %}*   
   *{% endblock content %}*   

  
  
  
  
## snippets  
- you can do the samething using another way:  
- include a html snippet file using 
                               *{% include 'path/to/file' %}*   


## Lecture #12  
### Documentation:   
### https://docs.djangoproject.com/en/2.0/ref/class-based-views/base/  



## ClassBasedViews  
 - in views.py:  
*import the view class from the django framework:*  
**from django.views import View*  
 - and write the rendering function:  
*class ContactView(View):  
 *def get(self, request, *args, **kwargs):*  
   *context = {}*  
   *return render(request, "contact.html", context)*  

- in urls.py: 
- Import the view in the urls:   
  **from restaurants.views import home, home2, home3, ContactView*  
- And mention it in the urls list:   
  **path('ContactView',ContactView.as_view, name='ContactView'), (in url patterns)*  
     
- For using an Id in the url:   
  Django 1.0.2:  url(r'^ContactView/(?P<id>\d+)$', ContactView.as_view())   
  Django 2.0.2:  path('ContactView/<int:id>/',ContactView.as_view(), name='ContactView')    
  



## Lecture #13

- TemplateView is a template like the previous View.   
- First import it into views.py:  
  from django.views.generic.base import TemplateView   
- And asociate it with a current page:   
   
  *class ContactTemplateView(TemplateView):*   
      *template_name = 'home.html'*   
   
- Do the same setup in urls like using a 'View', and instantiate the template with .as_view():   
* ... path('ContactTemplateView/',ContactTemplateView.as_view(), name='ContactTemplateView') ...* 

  

## Lecture #14   
- create a persistent structure, the model in models.py, inside the app's folder:   
  
*class Restauran(models.Model): *      
    * name = models.CharField(max_length=120) *  
  
- In base.py, mention the name of the django app.   
- then run these comands each time you add a new line in the above class:   
  python manage.py makemigrations  
  python manage.py migrate   
- add these in admin.py:  
  from .models import Restauran   
  admin.site.register.(Restauran)  

- You can access the dashboard at http://127.0.0.1:8000/admin/   

  
## Lecture 15    
  - timestamps:  
   *category      = models.CharField(max_length=120, null=True, blank=True)*    
   *time_stamp    = models.DateTimeField(auto_now=False, auto_now_add=False, null=True)*   
   *updated       = models.DateTimeField(auto_now=True)*   
   *my_date_field = models.DateField(auto_now=False, auto_now_add=False)*   


## Lecture 16   
- Import the module and retrieve the data using:    
   *queryset = RestaurantsLocation.objects.all()*   
   
- You can send the data packet throug the context in the following way:  
   
   *context = { "objects_list": queryset }*   
   *return render(request, template_name, context)*   






## Lecture 17   Understanding QuerySets   
- Playing with QuerySets  
   
Documentation at: https://docs.djangoproject.com/en/2.0/ref/models/querysets/
  
- Enter the python shell with:  
  * python manage.py shell*  
    
- Import the model inside the shell:   
 *from restaurants.models import RestaurantsLocation*     
   
- Retrieve data:   
   *qs = RestaurantsLocation.objects.all()*   
  
- Filter data:
   *italianDishes = qs.filter(category='italian')*  
                      or
   *italianDishes = qs.filter(category__iexact='italian')*   
   
Now italianDishes it's an array.

Here we pick an element:  
*instance = italianDishes[0]*     

Then we can use it as a normal DB object:   
*print(instance.name)*   
  
Edit:  
*qs.update(category='Mexican')*   

Create an object and save it:   
*obj = RestaurantLocation()*  
*obj.name = "blah blah"*  
.
.

And save it with:   
*obj.save()*  


- Or another method is by using the builtin function:   
  *obj = RestaurantsLocation.objects.create(name='McDonalds', category='Fast-Food', location='Everywhere')*   




## Lecture 17   Generic display views  
  
https://docs.djangoproject.com/en/2.0/ref/class-based-views/generic-display/   
  
- from django.views.generic.base import ListView
- set up in urls.py

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  


## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/AlexInntekt/DjangoNotes/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/AlexInntekt/DjangoNotes/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
