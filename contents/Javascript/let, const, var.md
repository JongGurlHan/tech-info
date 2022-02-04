### 1. var (변수 재선언 가능)
``` javascript
var variable = '변수선언함';
console.log(variable); //변수선언함

var variable = '또 변수선언함';
console.log(variable); //또 변수선언함
```
변수 선언을 여러 번해도 에러없이 각기 다른 값이 출력될 수 있습니다.  

이는 필요할 때 마다 변수를 사용할 수 있다는(편리하다는) 장점이 될 수 도 있지만, 같은 이름의 변수명을 남용하는 문제를 야기할 가능성이 높아지기에 단점이 더 크다고 할 수 있습니다.  
이를 보완하기 위해 ES6부터 let, const가 추가되었습니다.  

 

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
