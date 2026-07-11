
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name="index"), #/challenges/ refered
    path('<int:month>',views.monthly_challenges_by_number, name="month-challenge-by-number"),
    path('<str:month>',views.monthly_challenges, name="month-challenge")
]
```


