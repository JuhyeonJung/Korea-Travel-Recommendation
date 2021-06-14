## DeepLearning Project

- # 주제

  **주제 : 한국 여행지 추천시스템 - 자신이 좋아하는 분위기의 해외 여행지 사진을 입력했을 때, 비슷한 분위기의 한국 여행지 추천**

  - 주제 선정 이유 :
    - 자신이 마음에 들었던 여행지와 비슷한 분위기인 여행지를 검색하려 할 때 분위기를 텍스트로 설명하기 어려워 검색에 불편함을 느낌. → 여행 사진을 입력하면 비슷한 분위기의 여행지를 보다 빠르고 효율적으로 찾아주는 시스템의 필요성을 느낌.
    - 나아가 이러한 시스템으로 외국인들에게 여행지를 추천해준다면 국내 관광 활성화를 기대해볼 수 있음.
    - 코로나19로 인해 해외여행을 가지 못하는 현재 시국을 반영한다면, 가고싶은 해외 여행지의 대안으로 분위기가 비슷한 국내 여행지를 추천해줄 수 있음.
  - 데이터 설명
    - 국내 이미지(학습)
      - GoogleImageCrawler를 이용해 국내 여행지 사진 수집 → 이후 관련없는 사진 제거
      - 28개의 여행지, 총 1,495개의 이미지 데이터
      - train, validation, test data로 6 : 2 : 2 분리
      - Data augmentation을 통해 데이터를 늘림.
    - 해외 이미지(추천)
      - 가고싶은 여행지 사진 6개 수집
  - 학습 모델
    - VGG16 vs ResNet50 성능비교 → VGG16 채택
      - VGG16_A : 사전훈련된 가중치 이용, fine tuning X
      - VGG16_B : 사전훈련된 가중치 이용, fine tuning O
      - VGG16_C : VGG16_A + Global Average Pooling 이용
      - VGG16_D : VGG16_A + Dropout 이용

- 학습 모델

  - VGG16 vs ResNet50 성능비교 → VGG16 채택
    - VGG16_A : 사전훈련된 가중치 이용, fine tuning X
    - VGG16_B : 사전훈련된 가중치 이용, fine tuning O
    - VGG16_C : VGG16_A + Global Average Pooling 이용
    - VGG16_D : VGG16_A + Dropout 이용

![KakaoTalk_20210613_190518767](README.assets/KakaoTalk_20210613_190518767.jpg)

![KakaoTalk_20210613_190520256](README.assets/KakaoTalk_20210613_190520256-1623653490538.jpg)

![KakaoTalk_20210613_190521492](README.assets/KakaoTalk_20210613_190521492.jpg)

![KakaoTalk_20210613_213519862](README.assets/KakaoTalk_20210613_213519862.jpg)

- 성능 평가
  - test data에 대한 accuracy로 성능 평가
- 이미지 검색
  - 성능이 좋은 모델을 사용하여 국내,해외 이미지에 대한 feature vector 추출
  - 주어진 2개의 feature vector 사이의 cosine-similarity 계산.
  - 입력한 해외 이미지와 cosine-similarity가 높은 상위 5개의 국내 이미지를 플로팅
