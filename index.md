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
  
  
  
 
## Rendering  
- The views.py file of the django app will contain the visual content
of the project. Returning html content with a python fc inside of it:

from django.http import HttpResponse
def home(request):   
   #return render(request, "home.html", {})  
   return HttpResponse("<p> hello from django! </p>")   

or render on-the-spot code:

<img src="capture.png" alt="hi" class="inline"/>

def home(request): 
 html_var = '398'  
 html_ = f"""<!DOCTYPE html> 
 <html lang=en>  

 <head>
 </head> 
 <body> 
  <h1> Hello from django! {html_var} </h1>  
 </body>
 </html>   
 """
 return HttpResponse(html_)   

You can return much longer html content that will get rendered later on using
 """ instead of " and a local variable.


 
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  


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
