# DJANGO-LABS-IFEANYI
By Ifeanyi Omeata

## DJANGO

### [Django Course 1](https://www.udemy.com/course/python-django-the-practical-guide/)

<details>
  <summary>Django Basics</summary>

  ### Create and activate Virtual Env

  ```
  python -m venv venv
  source venv/bin/activate
  ```

  ### Dectivate Virtual Env

  ```
  deactivate
  ```

  ### Check Installed Packages

  ```
  pip list
  ```

  ### Install Django

  ```
  python -m pip install Django
  django-admin
  ```

  ### Check Django Version

  ```
  python -m django --version
  ```

  ### Create New Django Project

  ```
  django-admin startproject my_project .
  ```

  ### Create New App

  ```
  python manage.py startapp first_app
  ```

  ### Run Django Project in dev Mode

  ```
  python manage.py runserver
  ```

  <img width="1406" alt="image" src="https://github.com/user-attachments/assets/fff512c5-2c50-4087-95ca-429f591d5570" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/e6eb4d82-19d7-4614-91c2-f6a0002035de" />

</details>

<details>
  <summary>Django Challenges Project - Create Monthly Challenges Project </summary>

  ### Create and activate Virtual Env

  ```
  python -m venv venv
  source venv/bin/activate
  ```

  ### Install Django

  ```
  python -m pip install Django
  ```

  ### Create project

  ```
  django-admin startproject monthly_challenges_project .
  ```

  ### Create app

  ```
  python manage.py startapp challenges
  ```

  <img width="1450" alt="image" src="https://github.com/user-attachments/assets/ab3d6000-fe18-4b7d-9bd3-22fd2ad5a100" />


</details>

<details>
  <summary>Django Challenges Project - Set up Basic URL and View</summary>

  ### Github/python/monthly_challenges/monthly_challenges_project/urls.py

  ```py
  """
  URL configuration for monthly_challenges_project project.
  
  The `urlpatterns` list routes URLs to views. For more information please see:
      https://docs.djangoproject.com/en/5.2/topics/http/urls/
  Examples:
  Function views
      1. Add an import:  from my_app import views
      2. Add a URL to urlpatterns:  path('', views.home, name='home')
  Class-based views
      1. Add an import:  from other_app.views import Home
      2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
  Including another URLconf
      1. Import the include() function: from django.urls import include, path
      2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
  """
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('challenges/', include('challenges.urls')),
  ]

  ```

  ### Github/python/monthly_challenges/challenges/urls.py

  ```py
  from django.urls import path
  
  from . import views
  
  urlpatterns = [
      path('', views.index, name='index'),
      path('january', views.january, name='january'),
      path('february', views.february, name='february'),
      path('march', views.march, name='march'),
  ]

  ```

  ### Github/python/monthly_challenges/challenges/views.py

  ```py
  from django.shortcuts import render
  from django.http import HttpResponse
  
  # Create your views here.


  def index(request):
      return HttpResponse("<h1>Welcome to the challenges app!</h1>")
  
  
  def january(request):
      return HttpResponse("<h1>Eat no meat for the entire month!</h1>")
  
  
  def february(request):
      return HttpResponse("<h1>Walk for at least 20 minutes every day!</h1>")
  
  
  def march(request):
      return HttpResponse("<h1>Learn Django for at least 20 minutes every day!</h1>")

  ```

  <img width="1243" alt="image" src="https://github.com/user-attachments/assets/2f5b8e0d-fb4e-49b0-ac3f-3a9e91bcc9dd" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/eea6eb2a-324b-495b-826d-2a915e9f4718" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/1ca53132-121f-4c8a-be37-66dfa400941a" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/992e04c3-a453-49ac-b38e-6b83f80f83b5" />

</details>

<details>
  <summary>Django Challenges Project - Set up Dynamic URLs and Views </summary>

  ### Github/python/monthly_challenges/monthly_challenges_project/urls.py

  ```py
  """
  URL configuration for monthly_challenges_project project.
  
  The `urlpatterns` list routes URLs to views. For more information please see:
      https://docs.djangoproject.com/en/5.2/topics/http/urls/
  Examples:
  Function views
      1. Add an import:  from my_app import views
      2. Add a URL to urlpatterns:  path('', views.home, name='home')
  Class-based views
      1. Add an import:  from other_app.views import Home
      2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
  Including another URLconf
      1. Import the include() function: from django.urls import include, path
      2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
  """
  from django.contrib import admin
  from django.urls import path, include
  
  urlpatterns = [
      path('admin/', admin.site.urls),
      path('challenges/', include('challenges.urls')),
  ]

  ```

  ### Github/python/monthly_challenges/challenges/urls.py

  ```py
  from django.urls import path
  
  from . import views
  
  urlpatterns = [
      path('', views.index, name='index'),
      path('<int:month>', views.month_challenge_by_number,
           name='month-challenge-by-number'),
      path('<str:month>', views.month_challenge, name='month-challenge'),
  ]

  ```

  ### Github/python/monthly_challenges/challenges/views.py

  ```py
  from django.shortcuts import render
  from django.http import HttpResponse, HttpResponseNotFound
  
  # Create your views here.
  
  monthly_challenges = {
      "january": "Eat no meat for the entire month!",
      "february": "Walk for at least 20 minutes every day!",
      "march": "Learn Django for at least 20 minutes every day!"
  }
  
  
  def index(request):
      return HttpResponse("<h1>Welcome to the challenges app!</h1>")
  
  
  def month_challenge_by_number(request, month):
      if month > 12 or month < 1:
          return HttpResponseNotFound("<h1>Invalid month!</h1>")
      return HttpResponse(f"<h1>Challenge for Month {month}</h1>")
  
    
  def month_challenge(request, month):
      challenge_text = None
      try:
          challenge_text = monthly_challenges[month]
      except:
          if month in ["april", "may", "june", "july", "august", "september", "october", "november", "december"]:
              challenge_text = f"Challenge for {month} is coming soon!"
          else:
              return HttpResponseNotFound("<h1>Invalid month!</h1>")
      return HttpResponse(f"<h1>{challenge_text}</h1>")

  ```

  <img width="1415" alt="image" src="https://github.com/user-attachments/assets/f79d9a8a-a696-456b-a527-6aa479c825e0" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/ebb9459b-4359-4776-95f4-4b81b016a0e6" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/0d50135e-f409-429f-a7e3-4fc01ffdf419" />
  <img width="1453" alt="image" src="https://github.com/user-attachments/assets/cd58d679-0af9-42b2-b3ba-ca69e22771ed" />

</details>




















<details>
  <summary>Django Challenges Project - Set up </summary>

  ### Print String

  ```py

  ```

  ### Print String

  ```

  ```

</details>





<hr>


