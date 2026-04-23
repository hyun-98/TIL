<img width="977" height="400" alt="image" src="https://github.com/user-attachments/assets/4be3bfdb-62c8-44a1-98f5-9b7cf33fb8ab" />

## SSH 서버 접속하기
```
# 키 파일 권한 설정 (Mac/Linux)
chmod 400 내키파일.pem

# 서버 접속 (IP는 EC2 콘솔에서 확인)
ssh -i "내키파일.pem" ubuntu@내서버IP주소
```

## Node.js + Express로 간단한 API 서버 만들기
```bash
# 1. 패키지 업데이트
sudo apt update && sudo apt upgrade -y

# 2. Node.js 설치
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# 3. 버전 확인 (잘 설치됐는지)
node -v    # v20.x.x 가 나오면 성공!
npm -v

# 4. 프로젝트 폴더 만들기
mkdir todo-server && cd todo-server
npm init -y

# 5. Express 설치
npm install express cors body-parser
```

## 서버 코드 작성
```bash
nano server.js   # nano는 간단한 텍스트 편집기
```


## server.js
```const express = require('express');
const cors = require('cors');
const app = express();

app.use(cors());           // Flutter 앱에서 접근 허용
app.use(express.json());   // JSON 데이터 받기

// 임시 데이터 저장소 (나중에 DB로 교체)
let todos = [
  { id: 1, title: '서버 만들기', done: false },
];

// 할 일 목록 가져오기
app.get('/todos', (req, res) => {
  res.json(todos);
});

// 할 일 추가하기
app.post('/todos', (req, res) => {
  const todo = {
    id: Date.now(),
    title: req.body.title,
    done: false,
  };
  todos.push(todo);
  res.json(todo);
});

// 할 일 완료 토글
app.put('/todos/:id', (req, res) => {
  const todo = todos.find(t => t.id == req.params.id);
  if (todo) todo.done = !todo.done;
  res.json(todo);
});

// 할 일 삭제
app.delete('/todos/:id', (req, res) => {
  todos = todos.filter(t => t.id != req.params.id);
  res.json({ message: '삭제됨' });
});

app.listen(3000, () => {
  console.log('서버 실행 중: http://localhost:3000');
});
```
저장: `Ctrl` + `X` → `Y` → `Enter`

---

## 서버 실행 + 항상 켜두기 (pm2)
``` bash
# pm2 설치 (컴퓨터 꺼도 서버가 살아있게 해주는 도구)
sudo npm install -g pm2

# 서버 시작
pm2 start server.js --name todo-server

# 서버 재부팅 후에도 자동 시작
pm2 startup
pm2 save

# 잘 돌아가는지 확인
pm2 status
```
---


3단계 — 포트 열기 (방화벽 설정)

```
AWS 콘솔 → EC2 → 내 인스턴스 클릭
→ 보안 탭 → 보안 그룹 클릭
→ 인바운드 규칙 편집
→ 규칙 추가:
    유형: 사용자 지정 TCP
    포트: 3000
    소스: 0.0.0.0/0  (모든 곳에서 접근 허용)
→ 규칙 저장
```

이제 브라우저에서 http://내서버IP:3000/todos 를 열면 JSON 데이터가 보여야 해요!


---

<img width="899" height="454" alt="image" src="https://github.com/user-attachments/assets/cc079f92-2120-4893-b7a6-13312cf0facd" />

## http dependecies 추가
```vscode
dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2
  http: ^1.2.0        # ← 이 줄 추가!
```

# flutter 설치
* https://docs.flutter.dev/install/archive
* 환경변수 설정

## vscode terminal에서 
`flutter pub get`
* Process finished 메시지가 뜨면 패키지 설치 완료예요!

## api_service.dart 파일 만들기

```
import 'dart:convert';
import 'package:http/http.dart' as http;

class ApiService {
  // ↓ 본인 EC2 퍼블릭 IP로 바꾸세요!
  static const String baseUrl = 'http://여기에EC2IP:3000';

  static Future<List<Map<String, dynamic>>> getTodos() async {
    final res = await http.get(Uri.parse('$baseUrl/todos'));
    if (res.statusCode == 200) {
      return List<Map<String, dynamic>>.from(jsonDecode(res.body));
    }
    throw Exception('불러오기 실패');
  }

  static Future<void> addTodo(String title) async {
    await http.post(
      Uri.parse('$baseUrl/todos'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode({'title': title}),
    );
  }

  static Future<void> toggleTodo(int id) async {
    await http.put(Uri.parse('$baseUrl/todos/$id'));
  }

  static Future<void> deleteTodo(int id) async {
    await http.delete(Uri.parse('$baseUrl/todos/$id'));
  }
}
```

## main.dart에 추가
`import 'api_service.dart';`


## flutter Project 만드는 방법

* flutter create todo_app
* flutter run

---

# Android Studio 설치


## flutter doctor
-> 작동에 필요한 설치들이 되었는지 확인

---
## 이제 앱 빌드하기!
1. 프로젝트 폴더로 이동
2. 패키지 설치 `flutter pub get`
3. APK 빌드 `flutter build apk --release`
4.  
