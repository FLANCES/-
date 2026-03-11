# 🧠 MindLog — AI 정신건강 자가진단 & 감정 일기 앱

<p align="center">
  <img src="https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/Claude_API-6B4FBB?style=for-the-badge&logo=anthropic&logoColor=white"/>
  <img src="https://img.shields.io/badge/TensorFlow_Lite-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white"/>
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black"/>
  <img src="https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white"/>
</p>

---

## 📌 프로젝트 개요

**MindLog**는 AI 기반 감정 분석 기술을 활용하여 사용자의 정신건강을 스스로 관리할 수 있도록 돕는 모바일 앱입니다.

매일 감정 일기를 작성하면 **온디바이스 TFLite 모델**이 즉각적으로 1차 감정을 분류하고, **Claude AI**가 심층 분석과 맞춤형 공감 피드백을 제공합니다. 인터넷 연결 없이도 기본 감정 분석이 가능하며, 부정적 감정이 지속될 경우 위험 징후를 조기 감지하여 전문가 상담을 안내합니다.

---

## 🎯 개발 배경 및 목적

- 일상에서 감정 변화를 스스로 인식하기 어려운 문제
- 정신건강 관리를 위한 접근성 부족
- 네트워크 환경에 관계없이 즉각적인 감정 분석 필요
- 위기 상황에서 신속한 도움 연결 체계 미비

온디바이스 AI(TFLite)와 클라우드 AI(Claude API)를 결합한 **하이브리드 AI 아키텍처**를 통해 빠른 응답속도와 심층 분석을 동시에 제공합니다.

---

## ✨ 주요 기능

| 기능 | 설명 |
|------|------|
| 📝 감정 일기 작성 | 텍스트 일기 + 감정 태그 + 수면/식사/운동 체크 |
| ⚡ 온디바이스 감정 분류 | TFLite 모델로 오프라인 즉각 감정 분류 |
| 🤖 Claude AI 심층 분석 | 감정 강도 점수화, 공감 피드백, 셀프케어 추천 |
| 📊 패턴 시각화 | 주간/월간 감정 변화 그래프 및 요약 리포트 |
| 🚨 위험 징후 감지 | 오프라인 1차 + Claude AI 2차 정밀 감지 및 위기 알림 |

---

## 🛠️ 기술 스택

| 분류 | 기술 | 용도 |
|------|------|------|
| **Frontend** | Flutter (Dart) | 크로스플랫폼 모바일 앱 |
| **온디바이스 AI** | TensorFlow Lite | 오프라인 1차 감정 분류 |
| **클라우드 AI** | Claude API (claude-sonnet-4-6) | 심층 감정 분석 및 피드백 |
| **Backend** | Python, FastAPI | REST API 서버 |
| **DB** | SQLite + Firebase | 로컬 저장 + 클라우드 백업 |

---

## 🗂️ 시스템 구조도

```mermaid
flowchart TD
    subgraph Client["📱 Flutter 앱 (Client)"]
        A[홈 화면] --> B[감정 일기 작성]
        A --> C[대시보드 / 시각화]
        A --> D[셀프케어 추천]
        B --> B1[감정 이모지 태그 선택]
        B --> B2[텍스트 일기 입력]
        B --> B3[수면 / 식사 / 운동 체크]
        C --> C1[주간 감정 그래프]
        C --> C2[월간 패턴 차트]
        C --> C3[감정 요약 리포트]
    end

    subgraph OnDevice["⚡ 온디바이스 AI (TFLite)"]
        TF1[텍스트 전처리\nTokenizer]
        TF2[감정 분류 모델\nTFLite Inference]
        TF3[1차 감정 결과\n기쁨 / 슬픔 / 불안 / 화남 / 평온]
        TF4[위험 키워드 감지\n오프라인 1차 필터]
        TF1 --> TF2 --> TF3
        TF2 --> TF4
    end

    subgraph Backend["⚙️ FastAPI 서버 (Backend)"]
        E[API Gateway] --> F[심층 감정 분석 엔드포인트]
        E --> G[위험 징후 감지 엔드포인트]
        E --> H[셀프케어 추천 엔드포인트]
        F --> I[프롬프트 엔지니어링 모듈]
        G --> I
        H --> I
    end

    subgraph AI["🤖 Claude API (클라우드 AI)"]
        I --> J[심층 감정 분석\n맥락 파악 및 강도 점수화]
        I --> K[공감 피드백 생성]
        I --> L[셀프케어 활동 추천]
        I --> M[위험 징후 2차 정밀 감지]
    end

    subgraph DB["🗄️ 데이터 저장"]
        O[(SQLite\n로컬 DB)]
        P[(Firebase\n클라우드 백업)]
    end

    subgraph Alert["🚨 위기 대응"]
        TF4 -->|오프라인 1차 감지| Q[즉시 경고 알림]
        M -->|온라인 2차 정밀 감지| Q
        Q --> R[전문가 상담 안내]
        Q --> S[위기상담 전화\n1393 / 1577-0199]
    end

    B2 -->|텍스트 입력| TF1
    TF3 -->|1차 분류 결과| E
    TF3 -->|즉각 표시| A
    J -->|심층 분석 결과| C
    K -->|피드백 텍스트| A
    L -->|추천 활동| D
    B -->|저장| O
    O -->|백업| P

    style Client fill:#E8F4FD,stroke:#2196F3,stroke-width:2px
    style OnDevice fill:#FFF8E1,stroke:#FFC107,stroke-width:2px
    style Backend fill:#FFF3E0,stroke:#FF9800,stroke-width:2px
    style AI fill:#F3E5F5,stroke:#9C27B0,stroke-width:2px
    style DB fill:#E8F5E9,stroke:#4CAF50,stroke-width:2px
    style Alert fill:#FFEBEE,stroke:#F44336,stroke-width:2px
```

---

## 🤖 하이브리드 AI 아키텍처

| 구분 | TFLite (온디바이스) | Claude API (클라우드) |
|------|-------------------|-------------------|
| 동작 환경 | 오프라인 가능 | 인터넷 필요 |
| 응답 속도 | 매우 빠름 (ms 단위) | 초 단위 |
| 분석 깊이 | 1차 감정 분류 | 심층 맥락 분석 |
| 역할 | 즉각 반응 + 오프라인 지원 | 정밀 분석 + 피드백 생성 |

---

## 📁 프로젝트 구조

```
MindLog/
├── app/                              # Flutter 앱
│   ├── lib/
│   │   ├── screens/                  # 화면 (홈, 일기 작성, 대시보드)
│   │   ├── services/
│   │   │   ├── tflite_service.dart   # TFLite 추론 서비스
│   │   │   ├── api_service.dart      # FastAPI 통신
│   │   │   └── db_service.dart       # SQLite DB 서비스
│   │   └── widgets/                  # 재사용 UI 컴포넌트
│   ├── assets/
│   │   └── models/
│   │       └── emotion_model.tflite  # 온디바이스 감정 분류 모델
│   └── pubspec.yaml
│
├── server/                           # FastAPI 백엔드
│   ├── main.py
│   ├── routers/
│   ├── services/
│   └── requirements.txt
│
├── model/                            # TFLite 모델 학습
│   ├── train.py
│   └── convert_tflite.py
│
└── README.md
```

---

## 🚀 실행 방법

### 백엔드 서버

```bash
cd server
pip install -r requirements.txt
uvicorn main:app --reload
```

### Flutter 앱

```bash
cd app
flutter pub get
flutter run
```

### 환경 변수 설정

```
# server/.env
ANTHROPIC_API_KEY=your_api_key_here
FIREBASE_PROJECT_ID=your_project_id
```

---

## 📞 위기상담 안내

본 앱은 전문적인 의료 서비스를 대체하지 않습니다.

- **정신건강 위기상담** : 1577-0199 (24시간)
- **자살예방 상담전화** : 1393 (24시간)
- **청소년 상담전화** : 1388

---

## 📄 License

MIT License
