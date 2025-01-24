# LLM 기초
### 오늘은 api로 LLM 사용하는 코드를 작성해 보았습니다다
```py
import openai
import os
from dotenv import load_dotenv

load_dotenv()

openai.api_key = os.getenv("OPENAI_API_KEY")

prompt = [
			{"role": "system", "content": "you are simple movie commenter"}
		]

while True:
    user_input = input("궁금한 것을 물어보세요 : ")
    if user_input.lower() != "exit":
        prompt.append({"role": "user", "content": user_input})
        response = openai.ChatCompletion.create(
		model="gpt-3.5-turbo",
		messages=prompt
		)
        print(response['choices'][0]['message']['content'])
        with open("messages.txt", "a", encoding="utf-8") as file:
            file.write(f'질문 : {user_input}\n답변 : {response['choices'][0]['message']['content']}\n----------------\n')
    else:
        print("저희 서비스를 이용해주셔서 감사합니다!")
        break
```
- append를 사용해 While문이 돌아가는 동안 질문을 누적하여 학습할 수 있게 하였습니다.
- with as file 사용해 질문 내용을 txt 파일에 기록

### 오늘의 회고
- 오늘은 LLM과 API 사용법에 대해 처음 배웠습니다.
- 빠르게 필수과제와, 도전과제를 구현하였습니다
- 이번 주말에는 남은 장고강의를 다 들어야할듯합니다,,,,