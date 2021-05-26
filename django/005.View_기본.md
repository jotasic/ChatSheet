# Django View

views.py 를 보기전에 urls.py를 봐야된다.

urls.py에서 어느 url이 들어왔을 때, 어느 app으로 보내줘야될지 정의한다.

urls.py에서는 어느 app으로 보낼지 정도만 분류하고. 각각의 app의 urls.py에서는 세부 작업을 분류한다.

## project의 urls.py
urls.py에서는 보낼때 다음 방식으로 보낸다.

```python
from django.urls import path, include

urlpatterns = [
    # localhost:8000/product
    path('products', include('products.urls'))
]
```

## 각각의 App에 있는 urls.py
urls.py에서 처리한 부분 뒤를 처리한다.

urls.py > # localhost:8000/`product`/11234 GET
app of urls.py > `11234` GET

예시
```python
from django.urls import path
from owners.views import OwnerView, DogView

urlpatterns = [path('/owner' , OwnerView.as_view()), 
               path('/dog' , DogView.as_view()),
]
```

as_view() 메소드는 요청 Metchod에 따라서 Mathod를 Call해준다.

- GET > get()
- POST > post()

## Data 처리
Post의 경우 Data가 Body에 담아서 오는 경우가 있는데, 다음과 같이 딕셔너리 형태로 받는다.

Python의 경우 Json에서 바로 쓸 수 있는 자료형이 많지 않아서 다음과 같이한다고 한다.

```python
import json
...
owner = json.loads(request.body)
```

## Response
응답을 보내기 위해서 여러가지 방법이 있는데, 그중에서 사용한 내용을 정리한다.

### JsonResponse
Json 형태로 Body Message를 만들어준다.

`Body Data` 및  `결과 코드 등를 인자로 받는다`

```python
from django.http  import JsonResponse
..
..
return JsonResponse({"result":"CREATED"}, status=201)
```