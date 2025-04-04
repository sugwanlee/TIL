# Django의 request.user 활용

- **작동 방식**:
  1. **로그인**: 사용자가 로그인하면, Django는 사용자의 정보를 세션에 저장합니다. 이 정보는 데이터베이스에 저장된 사용자 모델의 인스턴스와 연결됩니다.
  2. **세션**: 사용자가 로그인한 후, Django는 세션 ID를 클라이언트에게 쿠키로 전달합니다. 이후 요청이 들어올 때마다 이 쿠키를 통해 사용자를 식별합니다.
  3. **요청 처리**: 요청이 들어오면 Django는 세션 ID를 확인하고, 해당 세션에 연결된 사용자 정보를 `request.user`에 할당합니다. 이 과정에서 사용자의 인증 상태가 확인됩니다.
  4. **헤더**: 만약 JWT(JSON Web Token)와 같은 토큰 기반 인증을 사용하는 경우, 사용자는 요청 헤더에 토큰을 포함시켜 서버에 요청을 보냅니다. Django는 이 토큰을 검증하여 사용자의 정보를 가져오고, `request.user`에 할당합니다.

- **게시물 수정 로직**:
  - 게시물의 작성자와 댓글의 작성자를 구별하기 위해 `request.user`를 사용했습니다.
  - 예시 코드:
    ```python
    if post.author == request.user:
        # 게시물 수정 로직
    if comment.author == request.user:
        # 댓글 수정 로직
    ```

요청이 들어왔을 때 토큰을 검증하고 서버에서 사용자의 정보를 가져와 `request.user`에 할당한다는 것을 배웠습니다.
