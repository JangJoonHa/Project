# Project Motivation
프로그래밍을 하는데에 있어서 Travelling salesman problem이 알고리즘에서 최적하를 하는데에 있어 의미있는 알고리즘을 만드는 데 도움이 될 것이라고 생각했다. 그 안에서 실생활과 연결지어 이러한 프로젝트를 만들고 싶어 연세대학교의 여러 건물을 경도와 위도를 구하여 좌표화를 하고 이 안에서 최단 거리로 방문하여 이동 거리를 최소화하는 알고리즘을 구상하려고 하였다. 그 안에서 단순히 점과 점 사이의 거리를 이용하는 것이 아닌 위도와 경도 좌표를 구하여 지구가 둥글다는 것을 알고 하버사인 공식(Haversine Formula)를 이용하여 더 정밀한 거리를 계산할 생각을 하였다.

# Data Acquisition Method
- 학교 내의 건물 좌표 구하기
연세대학교 내의 주요 건물의 위도와 경도 좌표를 수집하였는데, 이를 구글 맵스를 이용하여 구하였다.
'Underwood Hall': (37.5665, 126.9350), 'Science Hall': (37.5659, 126.9344),
'Engineering Building': (37.5662, 126.9337), 'Library': (37.5657, 126.9331),
'Business School': (37.5650, 126.9325), 'Yonsei Main Gate': (37.5668, 126.9385),
'Yonsei Cancer Center': (37.5664, 126.9381), 'Muak Dormitory': (37.5673, 126.9365),
'Baekyangro': (37.5660, 126.9349), 'Student Union Building': (37.5655, 126.9340),
'Alumni Hall': (37.5662, 126.9345), 'President’s Residence': (37.5659, 126.9360),
'Yonsei University Museum': (37.5655, 126.9355), 'Stimson Hall': (37.5663, 126.9360),
'Nursing Building': (37.5665, 126.9370)

-지구의 반지름
지구의 반지름은 6371km로 알려져 있어 이를 그대로 이용하였다.
R = 6371  # Radius of the Earth in km

- 하버사인 공식 (Haversine Formula)
hav(θ)=hav(φ2−φ1)+cos(φ1)cos(φ2)hav(λ2−λ1)
hav(θ)=sin^2(θ/2)=;{1−cos(θ)}/2
hav(​θ)=2rarcsin(sqrt

# Model
# Performance
