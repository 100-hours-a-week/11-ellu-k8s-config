# 11-ellu-k8s-config
Ellu's Looper 프로젝트 Kubernetes 메니페스트 리포지토리

## 프로젝트 개요
Looper는 AI 기반 일정 자동화 서비스로 회의록 및 문서를 기반으로 일정을 자동 생성해주는 서비스입니다.
- AI 챗봇을 통한 일정 생성
- 문서 요약 및 분석
- 프로젝트 관리 및 팀원 초대
- [서비스 바로가기] (https://looper.my)

## 시스템 아키텍처
**[프로젝트 아키텍처 다이어그램]**
![final_arc](https://github.com/user-attachments/assets/a6df23e7-e743-4aa7-90e3-b8e92dc629eb)

### 서비스 개요
- `Frontend`: Next.js 기반 웹 프론트엔드
- `Backend`: Spring Boot API 서버
- `AI-Chatbot`: 챗봇 서비스  
- `AI-Summary`: 문서 요약 및 분석 서비스
- `VLLM-Server`: LLM 추론 서버 (GPU)
- `ChromaDB`: 임베딩용 벡터 데이터베이스 
- `Kafka`: 메시지 스트리밍
- `Redis`: 인메모리 캐시 및 세션 스토어

**[서비스 구조도]**
<img width="1227" height="1386" alt="service_diagram" src="https://github.com/user-attachments/assets/bb73c2ad-0bdc-438e-9f10-d61c155a4e0b" />

## 환경 구성


### 디렉토리 구조

- `argocd/`: ArgoCD Application CRD 정의 파일들이 위치합니다. 각 환경(dev, prod, monitoring)별 ArgoCD Application을 정의합니다.
- `base/`: 모든 환경에서 공통으로 사용되는 Kubernetes 매니페스트의 기본(base) 설정이 위치합니다.
- `environments/`: 각 환경(dev, prod)을 위한 Kustomize 오버레이(overlay) 설정이 위치합니다. 이곳에서 `base` 설정을 기반으로 환경별 차이점을 정의합니다.
- `monitoring/`: 모니터링 스택(Prometheus, Grafana, Loki, Tempo 등)에 대한 설정 파일이 위치합니다.

### 개발 환경 (Dev)
- **네임스페이스**: `looper-dev`
- **특징**: 최소 리소스, 최신 이미지 태그 사용

### 운영 환경 (Prod)  
- **네임스페이스**: `looper-prod`
- **특징**: 고가용성, 안정 이미지 태그, HPA 적용

## GitOps 워크플로우

### ArgoCD 애플리케이션
1. **looper-prod-application**: 운영 환경 자동 배포
2. **looper-dev-application**: 개발 환경 자동 배포  
3. **monitoring-stack**: 모니터링 스택 관리

**[GitOps 워크플로우 다이어그램]**
![CD_PIPELINE](https://github.com/user-attachments/assets/c8379531-793a-410d-bad7-61153f643a87)


## 모니터링 스택
- **Prometheus**: 메트릭 수집 및 저장
- **Grafana**: 시각화 대시보드
- **Tempo**: 분산 트레이싱
- **Loki**: 로그 수집 및 분석
- **OpenTelemetry Collector**: 텔레메트리 데이터 수집

**[Tempo Service Graph]**
<img width="665" height="536" alt="스크린샷 2025-07-17 오후 1 42 09" src="https://github.com/user-attachments/assets/572a53b4-effe-432b-b877-09d1c29be977" />

## 디렉토리 구조
```
├── argocd/              # ArgoCD 애플리케이션 설정
├── base/                # 기본 Kubernetes 매니페스트
├── environments/        # 환경별 설정 (dev, prod)
└── monitoring/          # 모니터링 스택 설정
```

## 서비스 바로가기 (https://looper.my)

### GitHub 저장소
- 🌐 **Frontend**: [https://github.com/100-hours-a-week/11-ellu-fe](https://github.com/100-hours-a-week/11-ellu-fe)
- 🔧 **Backend**: [https://github.com/100-hours-a-week/11-ellu-be](https://github.com/100-hours-a-week/11-ellu-be)
- 🤖 **AI-Chatbot**: [https://github.com/100-hours-a-week/11-ellu-chatbot-ai](https://github.com/100-hours-a-week/11-ellu-chatbot-ai)
- 📝 **AI-Summary**: [https://github.com/100-hours-a-week/11-ellu-ai-summary-service](https://github.com/100-hours-a-week/11-ellu-ai-summary-service)

---
*Looper*
