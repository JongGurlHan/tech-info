## 조인(Inner Join, Outer Join)
조인(Join)이란 2개 이상 테이블을 서로 엮어 조회하는 것이다.  


**`Inner Join`** 은 서로 매칭되는 것만 엮어 조회한다.



**`Outer Join`** 은 매칭 뿐만 아니라 미매칭 데이터도 함께 조회한다.

Outer Join에는 Left Outer Join, Right Outer Join, Full Outer Join이 있다.  
Left, Right는 미매칭 데이터도 조회할 테이블 방향이다.  
따라서 Left Outer Join은 왼쪽에 기입한 테이블이 매칭여부와 관계없이 모두 나오게 된다.  


사례를 통해 익혀보자.



A와 B라는 2개의 코드성 테이블이 있고   
각 테이블의 코드를 비교하면서 어떻게 작동하는지 알아보자.  


우선 실습할 2개 테이블 생성하고 데이터를 넣는다.
```
CREATE TABLE A(
	CODE INT NOT NULL,
	CODE_NAME NCHAR(100) NOT NULL
	CONSTRAINT PK_A PRIMARY KEY(CODE)
);

CREATE TABLE B(
	CODE INT NOT NULL,
	CODE_NAME NCHAR(100) NOT NULL
	CONSTRAINT PK_B PRIMARY KEY(CODE)
);

INSERT INTO A(CODE, CODE_NAME) VALUES(1, 'ALPHA')
INSERT INTO A(CODE, CODE_NAME) VALUES(2, 'BETA')

INSERT INTO B(CODE, CODE_NAME) VALUES(2, 'BETA')
INSERT INTO B(CODE, CODE_NAME) VALUES(3, 'GAMMA')
```

1) 테이블 A에만 존재하는 코드를 조회한다.
![11](https://user-images.githubusercontent.com/60098769/148558501-980f97bf-ba01-4f70-8e4a-baf3a0486b7d.png)

```
SELECT *
FROM A LEFT OUTER JOIN B ON A.CODE = B.CODE
WHERE B.CODE IS NULL
```

![22](https://user-images.githubusercontent.com/60098769/148558572-fe84a685-80bf-4c2a-915b-59e03038f9e9.png)


<br><br>
2) 테이블 A와 테이블 B 모두에 존재하는 코드를 조회한다.

![33](https://user-images.githubusercontent.com/60098769/148558639-29ffdf5c-32f1-4b38-8830-0554b5544b8b.png)

```
SELECT *
FROM A INNER JOIN B ON A.CODE = B.CODE
```

![44](https://user-images.githubusercontent.com/60098769/148558703-e846035b-4e17-4efc-a916-59aef44bc6f7.png)
<br><br>
3) 테이블 A의 모든 코드는 매칭여부와 관계없이 모두 조회한다.

![55](https://user-images.githubusercontent.com/60098769/148558773-5d0ed4b4-27e4-4fd9-b77c-5e0e8331164d.png)

```
SELECT *
FROM A LEFT OUTER JOIN B ON A.CODE = B.CODE
```

![66](https://user-images.githubusercontent.com/60098769/148558851-7731514e-5057-4689-9c0e-9ec3e708b378.png)
<br><br>
4) A테이블과 B테이블 매칭이 안되는 나머지를 모두 조회한다.

![77](https://user-images.githubusercontent.com/60098769/148558937-a79119e9-cbfe-46b3-9839-4ee442a840bb.png)

```
SELECT *
FROM A FULL OUTER JOIN B ON A.CODE = B.CODE
WHERE A.CODE IS NULL OR B.CODE IS NULL
```

![88](https://user-images.githubusercontent.com/60098769/148558993-7776fc10-a252-4e07-8e15-c74d9a25a055.png)



