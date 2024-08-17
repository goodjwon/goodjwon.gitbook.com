# 1. useState

1. 타이머 만들기
    1. 요구사항 
        1. 화면에 시간을 표시 한다. 
        2. 시간은 1~12로 표시한다.
        3. 12가 된 후 에는 1로 초기화 한다.
        4. 시간의 증가는 update 버튼을 통해서 한다.
    2.  화면구성
        
        ![image.png](1%20useState%20e165d57fead7457cb3cb986a195975cd/image.png)
        
    3. 코드 작성
        1. 앱 생성
        
        ```jsx
        npx create-react-app 0.tutorial_star
        ```
        
        b. 파일정리
        
        > 불필요한 파일은 모두 지운다.
        > 
        
        ![image.png](1%20useState%20e165d57fead7457cb3cb986a195975cd/image%201.png)
        
        c. 코드 정리 
        
        1. 기본 상태
            
            ```jsx
            function App() {
              return (
                <div>
                </div>
              );
            }
            export default App;
            
            ```
            
        2. 변수 선언
            
            ```jsx
            function App() {
              let time;
              return (
                <div>
            	    <span>현재시각 {time}</span>
            	    <button>update<button>
                </div>
              );
            }
            export default App;
            
            ```
            
        3. 동작작성 
            
            ```jsx
            import { useState } from 'react'
            
            function App() {
              const [time,  setTime] = useState(1);
              
              let time;
              
              const handleClick = () => {
            	  setTime = time + 1;
              }
              
              return (
                <div>
            	    <span>현재시각 {time}</span>
            	    <button onClick='{handleClick}'> update<button>
                </div>
              );
            }
            export default App;
            
            ```
            
        4. 12시간 조건 충족 
            
            ```jsx
            import { useState } from 'react'
            function App() {
              const [time,  setTime] = useState(1);
            
              const handleClick = () =>{
                let newTime;
                if(time >= 12){
                  newTime = 1;
                } else {
                  newTime = time+1;
                }
            
                setTime(newTime);
              }
            
              console.log('update 화면!!!');
            
              return (
                <div>
                  <span>현재시각 {time} </span>
                  <button onClick={handleClick}>update</button>
                </div>
              );
            }
            
            export default App;
            
            ```
            
2. 목록 갱신 처리 하기
    1. 요구사항
        1. 입력창에 텍스트를 넣는다.
        2. update 버튼을 누르면 하단에 목록을 갱신한다.
    2. 화면구성
        
        ![image.png](1%20useState%20e165d57fead7457cb3cb986a195975cd/image%202.png)
        
    3. 코드정리
        1. 코드 기본 작성 
        
        ```jsx
        import { useState } from 'react'
        function App() {
        
          return (
            <div>
             <input type="text"/>
             <button type="button">upload</button>
            </div>
          );
        }
        
        export default App;
        
        ```
        
        1. 초기값 설정 
        
        ```jsx
        import { useState } from "react";
        function App() {
            const [name, setName] = useState(["호랑이", "사자", "코끼리"]);
        
            return (
                <div>
                    <input type="text" />
                    <button type="button">update</button>
                    <div>
                        {name.map((item, index) => (
                            <div key={index}>{item}</div>
                        ))}
                    </div>
                </div>
            );
        }
        
        export default App;
        
        ```
        
        1. 텍스트 박스 이벤트 작성  
        
        ```jsx
        import { useState } from "react";
        function App() {
            const [name, setName] = useState(["호랑이", "사자", "코끼리"]);
            const [input, setInput] = useState('');
        
            const handleInput = (e) =>{
                setInput(e.target.value);
            }
        
            console.log(input);
        
            return (
                <div>
                    <input type="text" onChange={handleInput} />
                    <button type="button">update</button>
                    <div>
                        {name.map((item, index) => (
                            <p key={index}>{item}</p>
                        ))}
                    </div>
                </div>
            );
        }
        
        export default App;
        
        ```
        
        4. 버튼 이벤트 작성 
        
        ```jsx
        import { useState } from "react";
        function App() {
            const [name, setName] = useState(["호랑이", "사자", "코끼리"]);
            const [input, setInput] = useState('');
        
            const handleInput = (e) =>{
                setInput(e.target.value);
            }
        
            const handleUpdate = () => {
                setName((prevStat)=>{
                    return [input, ...prevStat];
                });
            }
        
            return (
                <div>
                    <input type="text" onChange={handleInput} />
                    <button type="button" onClick={handleUpdate}>update</button>
                    <div>
                        {name.map((item, index) => (
                            <p key={index}>{item}</p>
                        ))}
                    </div>
                </div>
            );
        }
        
        export default App;
        
        ```
        
        5. 초기값 불러오기 및 튜닝 작업 
        
        ```jsx
        function heavyWork(){
          console.log("엄청 무거운 초기화 작업.. 데이터를 한 1000건 불려서 연산해 ㅎㅎ")
          return ["호랑이", "사자", "코끼리"];
        }
        
        // 개전 전
        function App() {
            const [name, setName] = useState(heavyWork());
            
        ```
        
        ![image.png](1%20useState%20e165d57fead7457cb3cb986a195975cd/image%203.png)
        
        1. 개선 후 
        
        > 함수를 useState 인자 값으로 넘기는 경우와 값을 넘기는 경우는 성능에 많은 차이점을 일으키는데 기본적으로 함수 자체를 인자 값으로 넘길때는 1번만 실행 하여 useState에 값을 전달 함.
        > 
        
        ```jsx
        //개선 후
        function App() {
            const [name, setName] = useState(()=>{
              return heavyWork();
            });
            
        or 
        
        function App() {
           const [name, setName] = useState(heavyWork);
          
        ```