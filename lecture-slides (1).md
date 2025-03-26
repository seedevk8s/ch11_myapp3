# 파이썬과 Qt Designer로 배우는 실용적인 데이터베이스 관리
## SQL 학습의 새로운 접근법

---

## 소개

* 이름: [강사명]
* 분야: 소프트웨어 공학, 데이터베이스 시스템
* 주요 경력: [관련 경력 요약]

> "코드는 읽기보다 쓰는 시간이 10배 더 걸리니, 읽기 쉽게 작성하는 것이 중요합니다."
> - Robert C. Martin

---

## 오늘의 특강 목표

* SQL과 데이터베이스 관리의 핵심 개념 이해
* 파이썬과 PyQt를 활용한 데이터베이스 응용 프로그램 개발
* Qt Designer를 통한 효율적인 UI 설계 방법 습득
* 이론과 실습을 통합한 실용적 학습 경험 제공

---

## 전통적인 SQL 학습의 문제점

* 👨‍💻 단조로운 커맨드 라인 환경
* 🔄 즉각적인 피드백 부족
* 🧩 실제 응용과의 연결성 부족
* 📊 시각화 및 상호작용 제한
* 💤 학습 과정의 지루함

---

## 새로운 접근법: 시각화와 상호작용

![GUI vs CLI](https://via.placeholder.com/800x400?text=GUI+vs+Command+Line+Interface)

---

## 파이썬: 현대 개발의 중심

* 🔥 AI, 데이터 사이언스 분야의 주력 언어
* 📚 풍부한 라이브러리 생태계
* 🧠 직관적인 문법과 가독성
* 🛠️ 다양한 도메인 통합 가능
* 📈 취업 시장에서 높은 수요

---

## 관계형 데이터베이스의 핵심 개념

![Database Structure](https://via.placeholder.com/800x400?text=RDBMS+Structure+Diagram)

---

## 기본 SQL 명령어

```sql
-- 테이블 생성
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 데이터 삽입
INSERT INTO users (username, email) VALUES ('user1', 'user1@example.com');

-- 데이터 조회
SELECT * FROM users WHERE username = 'user1';

-- 데이터 수정
UPDATE users SET email = 'new_email@example.com' WHERE id = 1;

-- 데이터 삭제
DELETE FROM users WHERE id = 1;
```

---

## CRUD 작업의 이해

* **C**reate: 데이터 생성/삽입
* **R**ead: 데이터 조회
* **U**pdate: 데이터 수정
* **D**elete: 데이터 삭제

> 거의 모든 데이터 관리 애플리케이션의 기본 기능

---

## PyQt 소개

* Qt: 강력한 크로스 플랫폼 GUI 프레임워크
* PyQt: 파이썬 바인딩으로 제공되는 Qt
* 주요 특징:
  * 풍부한 위젯 세트
  * 시그널/슬롯 메커니즘
  * 다양한 운영체제 지원
  * 이벤트 기반 프로그래밍

---

## Qt Designer의 강점

![Qt Designer Interface](https://via.placeholder.com/800x400?text=Qt+Designer+Interface)

---

## Qt Designer: 코드와 디자인의 분리

```python
# UI 파일 로드 방식
from PyQt6 import uic

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        
        # UI 파일 로드
        uic.loadUi('main_window.ui', self)
        
        # 이벤트 핸들러 연결
        self.saveButton.clicked.connect(self.save_data)
```

---

## 데이터베이스 연결 기본

```python
import pymysql

def connect_db():
    try:
        connection = pymysql.connect(
            host="localhost",
            port=3307,
            user="root",
            password="password",
            database="testdb"
        )
        return connection
    except pymysql.Error as e:
        print(f"데이터베이스 연결 오류: {e}")
        return None
```

---

## 실습: 데이터베이스 관리 애플리케이션

![Application Structure](https://via.placeholder.com/800x400?text=Database+Management+App+Structure)

---

## 데이터베이스 관리자 클래스

```python
class DatabaseManager:
    def __init__(self):
        self.connection = None
        self.cursor = None
        self.connect()
    
    def connect(self):
        # 데이터베이스 연결 코드
        pass
    
    def execute_query(self, query, params=None):
        # 쿼리 실행 코드
        pass
    
    def fetch_all(self, query, params=None):
        # 데이터 가져오기 코드
        pass
```

---

## Qt Designer로 UI 만들기 - 단계별 과정

1. Qt Designer 실행
2. "Main Window" 템플릿 선택
3. 위젯 배치 (테이블, 버튼, 입력 필드 등)
4. 레이아웃 적용 및 조정
5. 객체 이름 지정 (프로그래밍 접근용)
6. UI 파일 저장

---

## 실습 코드 살펴보기: UI 로드

```python
def __init__(self):
    super().__init__()
    
    # UI 파일 로드
    uic.loadUi('pyqt6-mysql-crud.ui', self)
    
    self.db_manager = DatabaseManager()
    self.current_table = ""
    self.columns = []
    self.input_fields = {}
    
    # UI 요소 연결
    self.setup_connections()
```

---

## 실습 코드 살펴보기: 이벤트 연결

```python
def setup_connections(self):
    """UI 요소와 이벤트 핸들러 연결"""
    # 테이블 콤보박스 변경 이벤트
    self.tableCombo.currentTextChanged.connect(self.on_table_changed)
    
    # 버튼 이벤트 연결
    self.refreshButton.clicked.connect(self.load_data)
    self.createButton.clicked.connect(self.create_record)
    self.updateButton.clicked.connect(self.update_record)
    self.deleteButton.clicked.connect(self.delete_record)
```

---

## 실습 코드 살펴보기: CRUD 구현

```python
def create_record(self):
    """새 레코드 생성"""
    # 입력 필드에서 데이터 가져오기
    values = []
    for column in self.columns:
        value = self.input_fields[column].text()
        values.append(value if value else None)
    
    # INSERT 쿼리 구성 및 실행
    placeholders = ", ".join(["%s"] * len(self.columns))
    columns_str = ", ".join(self.columns)
    query = f"INSERT INTO {self.current_table} ({columns_str}) VALUES ({placeholders})"
```

---

## 실습 데모

* 애플리케이션 실행 및 동작 방식 시연
* 데이터베이스 테이블 로드 및 표시
* 새 레코드 추가
* 기존 레코드 수정
* 레코드 삭제
* 사용자 정의 SQL 쿼리 실행

---

## GUI와 CLI 접근법 비교

| 기능 | GUI 접근법 | CLI 접근법 |
|------|------------|------------|
| 데이터 조회 | 테이블 클릭으로 시각화 | SELECT 쿼리 실행 후 텍스트 결과 |
| 레코드 추가 | 폼 작성 후 버튼 클릭 | INSERT 쿼리 직접 작성 |
| 레코드 수정 | 셀 선택 후 값 수정 | UPDATE 쿼리 직접 작성 |
| 학습 난이도 | 직관적이고 시각적 | 구문과 명령어 암기 필요 |

---

## UI와 로직 분리의 이점

* 코드 유지보수성 향상
* 디자인 변경 시 코드 수정 최소화
* 협업 효율성 증가 (디자이너/개발자)
* MVC(Model-View-Controller) 패턴 준수
* 코드 재사용성 개선

---

## 현업 활용 사례

* 회사 내부 데이터 관리 시스템
* 고객 관계 관리(CRM) 시스템
* 재고 관리 시스템
* 데이터 수집 및 분석 도구
* 학생 관리 시스템

---

## 확장 가능성

* 데이터 시각화 기능 추가 (그래프, 차트)
* 사용자 인증 및 권한 관리
* 다양한 데이터베이스 엔진 지원
* 클라우드 데이터베이스 연동
* 데이터 백업 및 복원 기능

---

## AI와의 연계 가능성

* 데이터 수집 및 정제 도구로 활용
* 머신러닝 모델 학습 데이터 관리
* 예측 결과 시각화
* 자동화된 데이터 분석 통합

---

## 핵심 학습 포인트

1. SQL은 실제 애플리케이션 컨텍스트에서 학습하면 더 효과적
2. UI와 데이터베이스 로직의 분리는 좋은 소프트웨어 설계 원칙
3. 시각적 도구가 학습 동기 부여와 이해도를 높임
4. 파이썬과 PyQt는 빠른 프로토타이핑에 이상적
5. 현업에서는 CLI와 GUI 접근법을 상황에 맞게 혼합

---

## 추천 학습 리소스

* **도서**: "Python과 PyQt를 활용한 GUI 프로그래밍"
* **온라인 강좌**: "파이썬으로 배우는 데이터베이스 기초"
* **웹사이트**: Qt 공식 문서, PyQt 튜토리얼
* **GitHub**: 오픈 소스 PyQt 프로젝트 예제

---

## 질의응답

* 질문이 있으신가요?
* 실습 중 어려웠던 부분이 있으셨나요?
* 현업에서의 활용 방안에 대한 아이디어가 있으신가요?

---

## 감사합니다!