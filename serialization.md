# 직렬화(Serialization)

**직렬화**란 객체의 상태를 **바이트 스트림** 형태로 변환하여 저장하거나 전송할 수 있도록 만드는 과정을 의미합니다. 이를 통해 데이터는 파일, 데이터베이스, 네트워크 등을 통해 전달될 수 있습니다.

### 주요 특징
- 데이터를 **JSON**, **XML** 등 특정 포맷으로 변환.
- 다른 시스템과 **호환 가능**하게 데이터를 전달.
- **역직렬화(Deserialization)**: 직렬화된 데이터를 다시 객체로 복원하는 과정.

### 사용 예시
- API 응답 데이터(JSON 형식).
- 네트워크를 통한 객체 전송.
- Django의 Serializer 활용.

### 코드 사용 예시
``` py
post = self.get_object(pk)
serializer = PostSerializer(post)
```
- 여기서 post는 QuerySet이고 serializer은 json형식입니다
- QuerySet은 데이터베이스에 접근할 수 있는 명령어
- serializer은 QuerySet을 통해 반환한 json객체 입니다.