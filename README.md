# EEG 기반 스트레스 분류 프로젝트  
DREAMER 데이터셋을 활용한 머신러닝 기반 감정 인지 연구

본 프로젝트는 EEG(뇌파) 신호를 이용해 피험자의 스트레스(High Arousal) 상태를 자동으로 분류하는 머신러닝 모델을 구축하는 것을 목표로 합니다.
특히 Baseline 보정, 피험자 단위 정규화(Subject-wise Normalization), 특성 선택(RFE), LOSO-CV 등을 적용해 일반화 성능을 강화한 것이 핵심입니다.

---

## 프로젝트 배경

현대 사회에서 스트레스는 집중력 저하, 감정 조절 문제 등 다양한 부정적 영향을 미치며, EEG는 뇌 기능을 직접 반영한다는 점에서 스트레스 모니터링에 매우 유용합니다.

본 연구는 DREAMER EEG 데이터를 활용하여,
- 스트레스 상태를 자동 판별할 수 있는
- 신뢰성 있는 머신러닝 모델을 제안하는 데 목적이 있습니다.

---

## 연구 목표

✔ 스트레스 여부 이진 분류  
✔ EEG 고유 특성 고려한 전처리  
✔ 핵심 feature 선정  
✔ 새로운 사람에게도 강건한 모델(LOSO 검증) 

---

## 데이터셋 (DREAMER)

| 항목 | 내용 |
|------|------|
| Subjects | 23명 |
| Stimuli | 영화 영상 18개 |
| EEG 채널 | 14채널 |
| Sampling Rate | 128 Hz |
| Label | Arousal(1~5) |

### 스트레스 레이블 정의
- Arousal ≥ 4 → **스트레스(1)**
- Arousal ≤ 2 → **비스트레스(0)**
- Arousal = 3 → 제외 (모호구간)

---

## 주요 전처리

### 1. Baseline 보정
Stimuli EEG – Baseline EEG

### 2. Subject-wise Normalization
피험자 비스트레스 구간만 기준으로 Z-score 적용  
→ 개인차 제거 효과

---

## Feature Engineering

14채널 × 12 feature = **총 168개**

- Time-domain
- Frequency-domain (Welch)
- Theta/Alpha, Beta/Alpha ratio
- RFE 로 상위 20개만 사용

---

## 머신러닝 알고리즘

- Logistic Regression
- SVM (Grid Search)
- RandomForest
- **Voting Ensemble (최종 모델)**

---

## 성능 결과 (LOSO-CV)

| 모델 | Accuracy | 비고 |
|-----|----------|------|
| Ensemble (Median) | **73.32%** | 최종 |
| Ensemble | 69% | |
| SVM + RFE(20) | 66% | 단일 최고 |
| SVM Full | 55% | 과적합 |
| Logistic | 50% | baseline |

### 주요 해석
- RFE로 노이즈 제거 시 성능 ↑
- Ensemble이 가장 안정적
- AUC ≈ 0.80

---

## 시각화 포함
- Feature importance
- Baseline normalization 비교
- Confusion Matrix
- ROC Curve

---

## 데이터 다운로드

데이터 용량/라이선스 문제로 GitHub에는 포함하지 않았습니다.  
아래 링크에서 직접 다운로드한 뒤, `DREAMER.mat` 파일을 프로젝트 루트에 위치시키면 됩니다.

https://zenodo.org/record/546113#.WzF9HxJKhaQ

---

## Repository Structure
notebooks/
├─ 01_DREAMER_data_overview.ipynb
├─ 02_EEG_feature_and_model_training.ipynb
README.md


---

## 향후 발전 방향

- DEAP / SEED 등 대규모 EEG 데이터 적용
- 멀티모달 생체 신호 결합 (GSR, ECG)
- 1D-CNN, LSTM, Transformer 적용
- Self-supervised 학습 적용

---

## Author

김승우  
(Data Engineer / ML Engineer)

GitHub: https://github.com/SeungwooKim525  
Velog: https://velog.io/@rjfldhs2/MLEEG-뇌파를-이용한-스트레스-분류-모델-개발

---
