# hbase command
- nosql

- sell 실행 `hbase shell`
- create table `create 'students', 'info'`
- table 조회 `list`
- Create 
    - 1번 학생의 이름과 나이
    - 2번 학생의 이름과 주소
```shell
put 'students', '1', 'info:name', 'ruka'
put 'students', '1', 'info:age', '23'
put 'students', '2', 'info:name', 'asa'
put 'students', '2', 'info:address', 'tokyo'
```
- Read
    - 1
    - all
```shell
get 'students', '1'
scan 'students'
```
- Update
```shell
put 'students', '2', 'info:address', 'seoul'
```
- Delete
    - 해당 컬럼 삭제
    - 전체 컬럼 삭제
```shell
delete 'students', '2', 'info:address'
deleteall 'students', '1'
```
- drop table
```shell
disable 'students'
drop 'students'
```

# 채팅 서비스 모델링

- create table
```shell
create 'chatrooms', 'info'
create 'messages', 'info'
```

- 채팅방 생성
```shell
put 'chatrooms', 'room1', 'info:name', 'python chatroom'
put 'chatrooms', 'room2', 'info:name', 'finance chatroom'
```

- 메시지 전송
```shell
put 'messages', 'room1_143900', 'info:text', 'python version?'
put 'messages', 'room1_143901', 'info:text', '3.13.2 :)'

put 'messages', 'room2_144000', 'info:text', 'tesla bad'
put 'messages', 'room2_144030', 'info:text', ':('

put 'messages', 'room1_143902', 'info:text', 'me too'
put 'messages', 'room2_144031', 'info:text', 'me too'
```

- 데이터 확인
```shell
scan 'messages'
```

- 데이터 조회
    - 출력 개수 제한
    - 특정 컬럼만 조회
    - 범위 지정 조회
    - prefix 기준 조회
```shell
scan 'messages', { LIMIT => 3 }
scan 'messages', { COLUMNS => ['info:text'] }
scan 'messages', { STARTROW => 'room1', STOPROW => 'room2' }
scan 'messages', { FILTER => "PrefixFilter('room1')" }
```