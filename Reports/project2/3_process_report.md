# 프로세스 검토 결과 보고서

## 1. 프로젝트 진행 프로세스

### 1. 프로젝트 흐름 및 단계
1. 데이터 수집
2. 데이터 전처리 
3. 모델 설계
4. 모델 학습 및 평가
5. 모델 적용 및 테스트
   - 웹캠으로 실시간 영상을 입력받아 실시간 눈 감지를 통한 졸음 여부 판단
   - 뜬 눈과 감은 눈을 구분하여 눈을 감기 시작하면 시간을 재고 화면에 출력
   - 눈을 감은지 2초가 되면 warning 메세지출력
  
### 2. 각 단계 참여자 
- 김문선:데이터 수집, 전처리, 모델 설계, 학습, 평가,  감지 시스템 개발
- 이성재:데이터 수집, 전처리, 모델 설계, 학습, 평가,  감지 시스템 개발

### 3. 단계별 사용 도구 및 시스템 
- Pytorch, openCV, YOLOv8-pose

## 2. 각 프로세스 결과 분석

### 1. 성과 
1. 학습 데이터 생성 : 이미지에서 얼굴 keypoints 좌표를 추출해  sequential 데이터를 생성
2. 모델 학습 : 모델 구조 개선, 하이퍼 파라미터 튜닝, 학습 데이터 feature scaling으로 성능을 개선함
3. 모델 적용 및 테스트 : 실시간 영상을 입력받아 sequence 데이터로 생성한 후 추론 결과 클래스와 확률을 화면에 출력함 

### 2. 문제점과 해결 방법
1. 이미지 데이터를 텐서로 변환하고, 정규화하는 과정에서 오류가 나는 등 입력값이나 출력값의 형태에 따른 오류가 많이 발생.
 → 오류를 통해 shape이 틀린 곳을 확인하고 input, output shape을 확인하며 오류 해결
2. 눈의 정확한 좌표값을 찾아 주지 못함.
 → 이미지상의 사람의 평균적인 눈 크기로 박스를 생성

### 4. 개선할 점
- OpenCV에서 모델이 너무 무거운 탓에 버벅임 감지
- 눈동자 좌표를 통해 적당한 눈 사이즈에 맞춰 박스를 만들어줬더니  이미지 사이즈에 따라 박스 크기가 달라짐

### 5. 활용 방안 
- 사고방지를 위한 실시간 졸음 방지 시스템에 활용 
    - delay없이 실시간으로 추론이 가능하며 성능이 우수함
    - ex) 눈 감은 지 몇 초가 되면 '졸음'으로 판단해 알람 등으로 운전자를 깨우는 시스템 
      
