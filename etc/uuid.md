# UUID (Universally unique identifier)
- 네트워크 상에서 모든 개체를 식별하고, 구별하기 위한 고유한 이름
- 국제기구에서 고유성을 보장하기 위한 표준을 제정
- UUID는 고유성을 완벽하게 보장할 수는 없지만, 실제로 중복될 가능성의 거의 없다고 함
- UUID는 128비트이며, 32개의 16진수로 표현되며 하이픈(-)을 포함한 8자리-4자리-4자리-4자리-12자리로 구성 (ex: 550e8400-e29b-41d4-a716-446655440000)
- 5가지 버전으로 구현할 수 있음

# Python UUID
```python
import uuid

id = uuid.uuid4()

print(id)
print(id.hex)  # 32자리 16진수 
print(id.int)  # 128비트 정수
```

## UUID를 이용해 64비트 고유한 정수 만들기
참고: [guid - How to generate unique 64 bits integers from Python? - Stack Overflow](https://stackoverflow.com/a/3530326)
```python
import uuid

id = uuid.uuid1()
print(id.int>>64)
```

