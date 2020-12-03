# 웹 응용 프로그래밍 9주차
## 7주차 입력값 누적 표 만들기
```c
<body>
  <h1 class="main-title">Simple Blog</h1>
  <ul class="blog-container">
    <li>
      <h4 class="item-title">Sample</h4>
      <p>Sample Post</p>
    </li>
  </ul>
  <hr>
  <div class="input-container">
    <div class="control-wrapper">
      <label>제목</label>
      <input type="text" id="title" placeholder="제목을 입력해주세요.">
    </div>
    <div class="control-wrapper">
      <textarea id="content" placeholder="내용을 입력해주세요."></textarea>
    </div>
    <button id="button">게시하기</button>
  </div>
  <script src="assets/js/app.js"></script>
</body>




*****css에서*****

/* 제목 스타일 */
.main-title {
  text-align: center;
  margin-bottom: 2em;
}

/* 컨텐츠 관련 스타일 */
ul {
  list-style: none;
  width: 1000px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}

li {
  width: 300px;
  border: 1px solid #ddd;
  margin: 10px;
  padding: 1.5em;
}

li > .item-title {
  margin-bottom: 2em;
}
/* 입력 컨트롤 관련 스타일 */
.input-container {
  width: 1000px;
  margin: 1em auto;
}

.control-wrapper {
  display: flex;
  align-items: center;
  width: 100%;
  margin: 0 0 1em;
}

label {
  margin-right: 1em;
}

input, textarea {
  flex-grow: 1;
  padding: 0.5em 1em;
}

textarea {
  display: block;
  width: 100%;
  height: 15em;
}

button {
  display: block;
  padding: 0.5em 1em;
  width: 100%;
}



*****java script에서*****
const blogContainer = document.querySelector('.blog-container');
const titleControl = document.querySelector('#title');
const contentControl = document.getElementById('content');
const button = document.getElementById('button');

button.addEventListener('click', () => {
  const title = titleControl.value;
  const content = contentControl.value;

  if (!title.trim() || !content.trim()) return;

  const li = makeBlogElement(title, content);
  blogContainer.appendChild(li);
  titleControl.value = '';
  contentControl.value = '';
});

function makeBlogElement(title, content) {
  const li = document.createElement('li');

  li.innerHTML = `<h4 class="item-title">${title}</h4>
      <p>${content.replace('\n', '<br>')}</p>`

  return li;
}
```
## 스탑워치 만들기
```c
*****index.html에*****
<body>
  <h1>Stop Watch</h1>
  <div class="stop-watch"></div>
  <button id="toggle">Start</button>
  <button id="clear">Clear</button>
    <div class="stop-watch"></div>
  <button id="toggle">Start</button>
  <button id="clear">Clear</button>
  <script src="assets/js/app.js"></script>
  <script>
    const element = document.querySelector('.stop-watch');
    const toggleBtn = document.querySelector('#toggle');
    const clearBtn = document.querySelector('#clear');
    const stopWatch = new StopWatch(element);

    toggleBtn.addEventListener('click', () => {
      if (stopWatch.isStart) {
        stopWatch.stop();
        toggleBtn.innerHTML = 'Start';
      } else {
        stopWatch.start();
        toggleBtn.innerHTML = 'Stop';
      }
    });

    clearBtn.addEventListener('click', () => {
      stopWatch.clear();
      toggleBtn.innerHTML = 'Start';
    });
  </script>
  </body>


*****java script에서*****
class StopWatch {
  constructor(element) {
    this.timer = element;
    this.time = 0;
    this._render();
  }

  get isStart() {
    return !!this.intervalId;
  }

  start() {
    this.intervalId = setInterval(() => {
      this.time++;
      this._render();
    }, 10);
  }

  stop() {
    if (this.intervalId) {
      clearInterval(this.intervalId);
      this.intervalId = null;
    }
  }

  clear() {
    this.stop();
    this.time = 0;
    this._render();
  }
  _render() {
    const tenMs = `${this.time % 100}`.padStart(2, '0');
    const sec = `${parseInt(this.time / 100) % 60}`.padStart(2, '0');
    const min = `${parseInt(this.time / 6000)}`.padStart(2, '0');
    this.timer.innerHTML = `${min}:${sec}:${tenMs}`;
  }
}
```

## 아이디,비먼,비번확인
```c
*****index.html에서*****
<body>
  <h3>회원 가입</h3>
  <form id="sign-up">
    <label for="user-id">아이디</label><br>
    <input type="text" name="userId" id="user-id"><br>
    <label for="password">비밀번호</label><br>
    <input type="password" name="password" id="password"><br>
    <label for="confirm-password">비밀번호 확인</label><br>
    <input type="password" name="confirmPassword" id="confirm-password"><br>
    <input type="submit" value="회원가입">
  </form>

*****js에서*****
    const form = document.querySelector('#sign-up');
    form.onsubmit = function () {
      const userId = document.querySelector('#user-id').value;
      const password = document.querySelector('#password').value;
      const confirmPassword = document.querySelector('#confirm-password').value;
      
      if (!userId.trim()) {
        alert('아이디를 입력해주세요.');
        return false;
      } else if (!password) {
        alert('비밀번호를 입력해주세요.');
        return false;
      } else if (password !== confirmPassword) {
        alert('비밀번호가 일치하지 않습니다.');
        return false;
      }
    };
```
아이디나 비번을 입력하지 않으면 ~를 입력해주세요 창이 뜬다.

## 사소한 거
```c
const, let : 변수 선언 예약어
```
let 은 중간에 수정 가능 const 는 불가능
```c
return;
```
함수종료
#### 함수예시
```c
function () {
if (!userId.trim()) {
        alert('아이디를 입력해주세요.');
        return false;
      } else if (!password) {
        alert('비밀번호를 입력해주세요.');
        return false;
      } else if (password !== confirmPassword) {
        alert('비밀번호가 일치하지 않습니다.');
        return false;
      }
    };
 ```
## css로 팝업창 만들기
```c
*****html에서*****
<div class="popup_btn">
  <a href="#pop01">팝업</a>
</div>

<div id="pop01" class="overlay">
  <div class="popup">
    <a href="#none" class="close">&times;</a>
    열려라 팝업!
  </div>
</div>

*****css에서*****
.popup_btn a {
  display: inline-block;
  padding: 20px;
  background: darkred;
  color: #fff;
}

.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.7);
  transition: opacity 500ms;
  visibility: hidden;
  opacity: 0;
  z-index: 900;
}

.overlay:target {
  visibility: visible;
  opacity: 1;
}

.popup {
  position: fixed;
  width: 60%;
  padding: 10px;
  max-width: 500px;
  border-radius: 10px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(255, 255, 255, .9);
  /* "delay" the visibility transition */
  -webkit-transition: opacity .5s, visibility 0s linear .5s;
  transition: opacity .5s, visibility 0s linear .5s;
  z-index: 1;
}

.popup:target {
  visibility: visible;
  opacity: 1;
  /* cancel visibility transition delay */
  -webkit-transition-delay: 0s;
  transition-delay: 0s;
}

.popup-close {
  position: absolute;
  padding: 10px;
  max-width: 500px;
  border-radius: 10px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: rgba(255, 255, 255, .9);
}

.popup .close {
  position: absolute;
  right: 5px;
  top: 5px;
  padding: 5px;
  color: #000;
  transition: color .3s;
  font-size: 2em;
  line-height: .6em;
  font-weight: bold;
}

.popup .close:hover {
  color: #00E5EE;
}
```

## 내가 만든 거 (주소를 입력하세요)
```c
<!doctype html>
<html>

<head>
    <meta charset="UTF-8">
    <title>Default Event</title>
</head>

<body>
    <h3>회원 가입</h3>
    <form id="sign-up">
        <label for="user-id">우편주소</label><br>
        <input type="text" name="userId" id="user-id"><br>
        <label for="password">상세주소</label><br>
        <input type="password" name="password" id="password"><br>

        <input type="submit" value="회원가입">
    </form>


    <script>
        const form = document.querySelector('#sign-up');
        form.onsubmit = function () {
            const userId = document.querySelector('#user-id').value;
            const password = document.querySelector('#password').value;

            if (!userId) {
                alert('우편번호를 입력해주세요.');
                return false;
            } else if (!password) {
                alert('상세주소를 입력해주세요.');
                }
            



        };
    </script>
</body>

</html>
```
우편번호 안 입력하면 안 입력했다고 뜸

# 그런데 왜 api랑 우편번호 붙어있으면 둘 다 작동을 안 하는가
