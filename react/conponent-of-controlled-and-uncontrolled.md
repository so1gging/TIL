# 제어 컴포넌트와 비제어 컴포넌트

* 제어 컴포넌트
   *  입력 값이 생길 때 마다 상태를 새롭게 갱신하여 항상 최신값으로 유지한다. 데이터와 UI에서 입력한 값이 항당 동기화되고 있다.
   *  즉, 사용자가 입력을 할 때 마다 재렌더링 되고 있다.

* 비제어 컴포넌트
   * state를 사용하지 않는 방식
   * input에 사용자입력 이벤트가 발생해도 그 값을 React system에 저장하지 않겠다는 것. 
   *  특정 값이 제출시에만 값을 알 수 있다.


### Controlled Component (제어 컴포넌트)
제어 컴포넌트는 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트 한다.

[예시]
```typescript
import { useState } from 'react';

const App = () => {
    const [name, setName] = useState('');
    
    const handleSubmit = e => {
    	e.preventDefault();
        alert(`Your name is ${name}`);
    };
    
    const nameChangeHandler = e => {
    	e.preventDefault();
        setName(e.target.value);
    };
    
    return(
    	<form onSubmit={handleSubmit}>
            <input 
             	type="text"
                placeholder="Enter Name"
                value={name}
                onChange={nameChangeHandler}
            />
            <button>Add</button>
        </form>
    );
};

export default App;
```
위 코드는 이름을 기록하는 `Controlled Component`의 예시이다.

1. 사용자가 `input`에 값을 입력한다.
2. 사용자가 값을 입력할 때 마다 `onChange` event handler 가 발생하여, `name state`를 update한다.
3. 변경된 `name state`값을 input value에 할당한다.


### Controlled Component (제어 컴포넌트)



[예시]
```typescript
import { useRef } from 'react';

const App = () => {
    const inputRef = useRef();

    const handleSubmit = () => {
      const name = inputRef.current.value;
      alert(`Your name is ${name}`);
    };
    
    return(
    	<form onSubmit={handleSubmit}>
            <input 
             	type="text"
                placeholder="Enter Name"
                ref={inputRef}
            />
            <button>Add</button>
        </form>
    );
};

export default App;
```
위 코드에서 `UnControlled Component`가 동작하는 순서는 아래와 같다.

1. 사용자가 input에 값을 입력한다.
2. 사용자가 Add 버튼을 클릭하면 ref를 통해 값을 얻는다.

> **참고자료**
> 
>*  https://dori-coding.tistory.com/entry/React-%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8Controlled-Component%EC%99%80-%EB%B9%84%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8Uncontrolled-Component