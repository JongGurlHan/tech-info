### 1. var
``` javascript
var variable = '변수선언함';
console.log(variable); //변수선언함

var variable = '또 변수선언함';
console.log(variable); //또 변수선언함
```
변수 선언을 여러 번해도 에러없이 각기 다른 값이 출력될 수 있습니다.  

이는 필요할 때 마다 변수를 사용할 수 있다는(편리하다는) 장점이 될 수 도 있지만, 같은 이름의 변수명을 남용하는 문제를 야기할 가능성이 높아지기에 단점이 더 크다고 할 수 있습니다.  
이를 보완하기 위해 ES6부터 let, const가 추가되었습니다.  

var는 선언하기 전에 사용할 수 있다.(물론 undefined 뜬다)
``` javascript
console.log(name); //undefined
var name = 'Mike';
```

왜나하면 var는 다음과 같이 동작하기 때문이다.  
**호이스팅** : 스코프 내부 
선언(name)은 호이스팅 되지만 할당(Mike)은 호이스팅 되지 않기 때문!

``` javascript
var name;
console.log(name); //undefined
name = 'Mike'; //할당
```
 </br> </br>
let은 ReferenceError에러가 뜬다! let또한 호이스팅이 되지만
**Temporal Dead Zone** 때문에 ReferenceError가 뜨는거다.
 ``` javascript
console.log(name); //ReferenceError
let name = 'Mike'; 
```
</br></br>
**Temporal Dead Zone**
let 과 const는 TDZ의 영향을 받는다, 할당을 받기전에는 사용할 수 없다.  
-> 이는 코드를 예측가능하게 하고 잠재적인 버그를 줄일 수 있다. 

이 코드는 문제가 없지만
 ``` javascript
let age = 30;

function showAge(){
  console.log(age);
}

showAge();
```

이 코드는 문제가 생긴다
 ``` javascript
let age = 30;

function showAge(){
  console.log(age);;
  let age = 20;
}

showAge();
```
호이스팅은 스코프 단위로 이뤄진다. 여기서 스코프는  
function 함수내부 를 의미한다.  
let으로 선언된 두 번째 변수가 호이스팅을 일으킨다.

**변수의 생성과정**  
var: 
1. 선언 및 초기화 단계
2. 할당 단계   

var는 선언과 초기화가 동시에 된다. 그래서 할당전에 호출하면 error를 내지 않고 undefined를 낸다.  
</br>

let: 
1. 선언 및 
2. 초기화 단계
3. 할당 단계   

let은 선언과 초기화가 분리된다. 호이스팅되면서 선언단계가 이뤄지지만 초기화단계는 실제 코드에 도달됐을때 된다.   

</br>
const: 
1. 선언 + 초기화+ 할당  

const는 이 셋이 동시에 돼야한다.    


**스코프**
var : 함수스코프(fuction-scoped)
let, const: 블록 스코프(block-scoped)

블록스코프: 코드 블록(함수, if문, for문, while문, try/catch문 등) 내에서만 선언된 변수가 유효하며, 외부에선 접근할 수 없다.   
즉 코드 블록 내에서 선언한 변수는 지역변수다.  

함수스코프: 함수 내에서 선언된 변수만 지역변수가 된다. 

``` javascript
const age = 30;

if(age>19){
  var txt = '성인';
}

console.log(txt);
 ```
 예를들어, if문 안에서 선언된 변수는 if문 밖에서도 사용가능  
 하지만 let 과 const는 이렇게 사용할 수 없다. (중괄호 내에서만 사용가능)
 
``` javascript
function add(num1, num2){
  var result = num1 + num2;
}

add(2,3);

console.log(result); //error: Uncaught ReferenceError: result is not defined
 ```
 var도 함수내에서 선언되면 함수 밖에서 선언될 수 없다. 유일하게 벗어날 수 없는 스코프가 함수다.


### 2. let (변수 재선언 불가능, 변수 재할당 가능)
``` javascript
let variable = '변수선언함';
console.log(variable); //변수선언함

variable = '변수 재할당함';
console.log(variable); //변수 재할당함

let variable = '또 변수선언함';
console.log(variable); //또 변수선언함
 ```
let은 변수의 재할당은 가능하지만 var처럼 재 선언은 되지 않습니다.  
실제로 재선언 후 크롬 개발자도구에서 확인해보면, 아래 이미지와 같은 에러 문구를 확인하실 수 있습니다.



### 3. const (변수 재선언 불가능, 변수 재할당 불가능)
``` javascript
const variable = '변수선언함';
console.log(variable); //변수선언함

variable = '변수 재할당함';
console.log(variable); //변수 재할당함(에러)

const variable = '또 변수선언함';
console.log(variable); //또 변수선언함(에러)
```
const의 경우 constant(상수)의 의미 그대로 한 번만 선언하고 또 값을 재할당을 통해 바꿀 수도 없습니다. 


### 4. 결론
재할당이 필요없는 경우, const를 사용해 불필요한 변수의 재사용을 방지하고, 재할당이 필요한 경우 let을 사용하는 것이 좋음.



출처: https://backstreet-programmer.tistory.com/76 [글쓰는 개발자]
