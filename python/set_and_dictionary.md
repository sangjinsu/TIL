# 세트와 딕셔너리

## Set

- 중복 없이 순서가 없는 데이터 구조
- mutable, unordered, iterable

### functions

- `add(elem)` - 값 추가
- `update([1, 2, 3])` - 여러 값 추가
- ` remove(elem)` - 세트에서 삭제하고 없으면 KeyError
- `discard(elem)` - 섹트에서 삭제하고 없어도 에러가 발생하지 않음
- `pop()` - 임의의 원소 제거하고 반환

## Dictionary

- Key와 Value로 구성된 데이터 구조
- mutable, unordered, iterable

### functions

- `get(key [, default])` - keyError가 발생하지 않으며 default 값 설정 가능
- `pop(key [, default])` - key 가 딕셔너리에 있으면 제거하고 해당 값 반환, 없으면  default 반환, default 값이 없으면 KeyError 
- `update(key=value)` - 값을 제공하는 key, value 업데이트, key가 없는 경우 key, value 생성 
- 딕셔너리는 기본적으로 key를 순회
- `keys()`, `values()`, `items() -  튜플로 구성된 결과`  

### Dictionary Comprehension

```python
{key: value for key, value in example.items() if value > 70}
{key: 0 for key in range(5)}
```



