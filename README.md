describe - 웹크롤링을 이용하여 원하는 이미지를 수집하고 전처리 후 CNN 모델을 구성하여 훈련과정의 전체.
d:\imgs 디렉터리 내의 폴더명은 정답으로 처리되며 각 관련 이미지가 내부에 존재 해야 한다.
opencv01.py - def removeBackgroundFolder : 디렉터리 내의 모든 이미지 백그라운 제거 및 이미지 256*256 으로 리사이징
              def singleRemoveBackground : 단일 이미지에 대한 256*256 으로 리사이징              
classification_model.py - def imageAugment_sub : 이미지를 회전,확대축소,밝기조정등으로 다양한 방법으로 이미지 증강
                          def readImageDirect : 디렉터리 내의 이미지를 읽어서 증강함수(imageAugment_sub)를 호출하고,
                                              이미지를 저장하는 함수
                          def load_directory_sub : 증강된 이미지를 읽어서 64*64로 변환후 numpy 리스트로 변환후 
                                                    정답리스트와,ylabel,xdata 리턴
                          def getTrainData : load_directory_sub 함수를 호출하여 정답파일을 기준으로 훈련데이터(80%)와 
                                            테스트데이터(20%)를 랜덤하게 분리
construct_Model.py - 훈련데이터의 minmax 표준화와 정답데이터의 원핫인코딩을 수행하고 이미지와 정답파일의 매칭을 확인후
                      Sequential 모델로 구성된 CNN을 구현하고 컴파일 과 훈련을 실행(조기종료 콜백함수 추가)
                      훈련결과와 모델을 파일로 저장
classification_analize.py - 테스트데이터와 테스트정답파일을 로딩한 후 훈련이 완료된 모델과 훈련결과를 로딩하여 
                            훈련/검증 데이터의 정확도와 훈련/검증 데이터의 손실도를 그래프로 시각화
                            훈련모델의 예측값을 출력하여 실제 정답과 이미지와 예측 정답을 시각화 표현
                            혼동 행렬을 이용한 히트맵 시각화
                            리포팅 요약 이용한 f2 score 등을 분석
