# ORM 지연로딩
## 지연로딩이란?
- 데이터 접근이 실제로 필요할 때까지 쿼리를 실행하지 않고 대기하는 방식
- Django의 ORM은 기본적으로 지연 로딩을 수행

## Django ORM에서의 지연 로딩
- QuerySet을 만들 때는 데이터베이스에서 즉시 쿼리를 실행하지 않음
- 데이터를 실제로 사용하려는 순간에 실행한다.

```py
@api_view(["GET"])
def check_sql(request):
    from django.db import connection

    comments = Comment.objects.all()
    for comment in comments:
        print(comment.article.title)

    # print(connection.queries)  # 너 좀 수상하다
    print("-" * 30)
    for query in connection.queries:
        print(query)  # 하나씩 출력해보자

    return Response()
```
![Image](https://github.com/user-attachments/assets/9febad1c-1d45-4f5f-96c8-deb2ebefc341)

이와같이 많은 양의 쿼리가 불필요하게 데이터베이스에 날아가게 된다

```py
SELECT "articles_comment"."id", "articles_comment"."article_id", "articles_comment"."content", "articles_comment"."created_at", "articles_comment"."updated_at" 
FROM "articles_comment"

SELECT "articles_article"."id", "articles_article"."title", "articles_article"."content", "articles_article"."created_at", "articles_article"."updated_at" 
FROM "articles_article" 
WHERE "articles_article"."id" = 16 
LIMIT 21

SELECT "articles_article"."id", "articles_article"."title", "articles_article"."content", "articles_article"."created_at", "articles_article"."updated_at" 
FROM "articles_article" 
WHERE "articles_article"."id" = 31 
LIMIT 21

SELECT "articles_article"."id", "articles_article"."title", "articles_article"."content", "articles_article"."created_at", "articles_article"."updated_at" 
FROM "articles_article" 
WHERE "articles_article"."id" = 38 
LIMIT 21

...
```
- 한 번의 쿼리(1)가 일어난 다음, 비슷한 쿼리(2)가 엄청 많이 일어남

## 해결방법
- 즉시로딩을 이용해 데이터를 로드할 떄 필요한 데이터를 한번에 가져오는 방식
- **Django에서의 Eager Loading**
    - `select_related`
        - one-to-many 또는 one-to-one 관계에서 사용
        - SQL의 JOIN을 이용해서 관련된 객체들을 한 번에 로드하는 방식
    - `prefetch_related`
        - many-to-many 또는 역참조 관계에서 주로 사용
            
            (select_related를 사용하는 관계에서도 동작)
            
        - 내부적으로 두번의 쿼리를 사용해서 동작
        첫번째 쿼리는 원래 객체를 조회하며 두번째 쿼리는 연관된 객체를 가져오는 방식

위 방법을 사용하여 코드를 작성하면

아까의 결과가

```
SELECT "articles_article"."id", "articles_article"."title", "articles_article"."content", "articles_article"."created_at", "articles_article"."updated_at" FROM "articles_article"

SELECT "articles_comment"."id", "articles_comment"."article_id", "articles_comment"."content", "articles_comment"."created_at", "articles_comment"."updated_at" 
FROM "articles_comment" WHERE "articles_comment"."article_id" IN (1, 2, 3, ... , 170)
```

위와같이 필요한 정보만 로드하게 바뀝니다.

## 오늘의 회고
- 오늘은 명절 때문에 헤이해진 자신을 돌아보는 기회가 되었습니다
- 지금부터는 다시 달려야겠습니다.