# Class Based View (CBV)

## Class Based View 의 특징!
- 클래스형 뷰에서는 http Method에 대한 처리를 함수로 분리 할 수 있습니다
  - 기존에는 하나의 함수에서 if문으로 요청을 나눴던것과는 다르게 직관적으로 나누어집니다!

- 클래스를 사용하기 때문에 코드의 재사용성과 유지보수성이 향상됩니다.
- 기본 APIView외에도 여러 편의를 제공하는 다양한 내장 CBV가 존재합니다.

## Class Based View 종류
- `APIView` - DRF CBV의 베이스 클래스
- `GenericAPIView`
    - 일반적인 API 작성을 위한 기능이 포함된 클래스
    - 보통 CRUD 기능이 대부분인 상황을 위해 여러가지 기능이 미리 내장되어 있습니다.
- `Mixin`
    - 재사용 가능한 여러가지 기능을 담고있느 클래스
    - 말그대로 여러 클래스를 섞어서 사용하기 위한 클래스
        - `ListModelMixin` - 리스트 반환 API를 만들기 위해 상속 받는 클래스
        - `CreateModelMixin` - 새로운 객체를 생성하는 API를 만들기위해 상속 받는 클래스
- `ViewSets`
    - 여러 엔드포인트(endpoint)를 한 번에 관리할 수 있는 클래스
    - RESTful API에서 반복되는 구조를 더 편리하게 작성할 수 있는 방법을 제공합니다.


## 예시 코드
``` py
from rest_framework.views import APIView

class ArticleListAPIView(APIView):
    def get(self, request):
        articles = Article.objects.all()
        serializer = ArticleSerializer(articles, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = ArticleSerializer(data=request.data)
        if serializer.is_valid(raise_exception=True):
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
```
- 위 처럼 기존 함수형 뷰에 있는 기능들을 http method에 따라 함수로 분리해서 작성하면 된다
- 요청에 따라 `get()` , `post()` 등의 메서드로 요청에 따른 처리를 나누기 때문에 유지보수가 편리함
- 따라서 복수의 기능이 동일한 url을 사용할 수 있기 때문에 특정한 api 규약을 만들기 용이 하고 기능마다 url을 만들지 않아도 돼서 편리함

### 오늘의 회고
- 오늘은 나쁘지 않은 하루였지만 역시 피곤한 날이었다
- 내일부터 아마 도전과제를 시작할 수 있을 듯 하다
- 이번 주 내로 도전과제는 완성 할 수 있을 것 같다.