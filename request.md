**TIL: Django의 request 객체**

Django에서 `request`는 클라이언트가 보낸 HTTP 요청에 대한 정보를 담고 있는 객체입니다. `request` 객체는 뷰 함수에서 요청을 처리할 수 있게 해주며, 요청의 HTTP 메서드, URL 파라미터, 폼 데이터, 사용자 정보, 헤더 등을 다룰 수 있습니다.

### 주요 속성
1. **request.method**
   - 클라이언트가 보낸 HTTP 메서드(GET, POST, PUT, DELETE 등)를 확인할 수 있습니다.
   - 예시:
     ```python
     if request.method == "GET":
         # GET 요청 처리
         return HttpResponse("This is a GET request")
     ```

2. **request.GET**
   - URL 쿼리 문자열을 담고 있는 딕셔너리와 유사한 객체입니다.
   - GET 요청 시 URL 파라미터를 처리합니다.
   - 예시:
     ```python
     page = request.GET.get("page", 1)
     category = request.GET.get("category", "all")
     return HttpResponse(f"Page: {page}, Category: {category}")
     ```

3. **request.POST**
   - POST 요청에서 클라이언트가 보낸 데이터를 담고 있는 객체입니다. 주로 폼 데이터를 처리할 때 사용됩니다.
   - 예시:
     ```python
     username = request.POST.get("username")
     password = request.POST.get("password")
     return HttpResponse(f"Username: {username}, Password: {password}")
     ```

4. **request.user**
   - 현재 요청을 보낸 사용자의 정보를 담고 있는 객체로, Django의 인증 시스템과 연동됩니다.
   - 인증된 사용자는 `User` 객체, 인증되지 않은 사용자는 `AnonymousUser` 객체가 반환됩니다.
   - 예시:
     ```python
     if request.user.is_authenticated:
         return HttpResponse(f"Hello, {request.user.username}")
     else:
         return HttpResponse("Hello, Guest")
     ```

5. **request.path**
   - 요청된 URL의 경로를 나타냅니다.
   - 예시:
     ```python
     return HttpResponse(f"You accessed the path: {request.path}")
     ```

6. **request.META**
   - 요청 헤더와 관련된 정보를 담고 있는 딕셔너리입니다. 클라이언트의 IP 주소나 `User-Agent` 등을 확인할 때 유용합니다.
   - 예시:
     ```python
     user_agent = request.META.get("HTTP_USER_AGENT")
     ip_address = request.META.get("REMOTE_ADDR")
     return HttpResponse(f"User-Agent: {user_agent}, IP: {ip_address}")
     ```

7. **request.FILES**
   - 파일 업로드가 포함된 POST 요청에서 업로드된 파일 데이터를 처리합니다.
   - 예시:
     ```python
     if request.method == "POST" and request.FILES:
         uploaded_file = request.FILES["file"]
         file_name = uploaded_file.name
         file_size = uploaded_file.size
         return HttpResponse(f"Uploaded file: {file_name}, Size: {file_size}")
     ```

### `listview`에서의 활용 예시
`listview` 함수는 `request` 객체를 활용하여 클라이언트의 요청을 처리하고, 특정 `pk`(primary key)에 해당하는 데이터를 반환하는 방식으로 구현됩니다. `request.method`를 통해 요청의 유형을 확인하고, 적절한 응답을 제공합니다.

예시:
```python
from django.http import HttpResponse
from .models import Article

def listview(request, pk):
    if request.method == "GET":
        try:
            article = Article.objects.get(pk=pk)
            return HttpResponse(f"Article: {article.title}")
        except Article.DoesNotExist:
            return HttpResponse("Article not found", status=404)
    else:
        return HttpResponse("Unsupported request method", status=405)
```

### 결론
- `request`는 Django에서 클라이언트의 요청에 대한 중요한 정보를 담고 있는 객체입니다.
- 이를 통해 HTTP 메서드, URL 파라미터, 폼 데이터, 사용자 정보, 헤더 등을 처리할 수 있습니다.
- `listview`와 같은 뷰 함수에서 `request`를 활용하여 클라이언트의 요청을 분석하고 적절한 응답을 생성합니다.

### 오늘의 회고
- 오늘은 과제 제출을 하고 쉬어가는 날이었습니다
- 내일부터 달릴 듯 합니다