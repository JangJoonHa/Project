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
  'Yonsei University Museum': (37.5655, 126.9355), 'Stimson Hall': (37.5663,         126.9360),
  'Nursing Building': (37.5665, 126.9370)

-지구의 반지름
지구의 반지름은 6371km로 알려져 있어 이를 그대로 이용하였다.
R = 6371  # Radius of the Earth in km

- 하버사인 공식 (Haversine Formula)
hav(θ)=hav(φ2−φ1)+cos(φ1)cos(φ2)hav(λ2−λ1)
hav(θ)=sin^2(θ/2)=;{1−cos(θ)}/2
d=2rarcsin(sqrt(hav(θ))
으로 알려져 있어 이를 알고리즘을 만드는데 이용하였다.

# Model

  # Step 1: Define the buildings and their coordinates
    buildings = {
    'Underwood Hall': (37.5665, 126.9350),
    'Science Hall': (37.5659, 126.9344),
    'Engineering Building': (37.5662, 126.9337),
    'Library': (37.5657, 126.9331),
    'Business School': (37.5650, 126.9325),
    'Yonsei Main Gate': (37.5668, 126.9385),
    'Yonsei Cancer Center': (37.5664, 126.9381),
    'Muak Dormitory': (37.5673, 126.9365),
    'Baekyangro': (37.5660, 126.9349),
    'Student Union Building': (37.5655, 126.9340),
    'Alumni Hall': (37.5662, 126.9345),
    'President’s Residence': (37.5659, 126.9360),
    'Yonsei University Museum': (37.5655, 126.9355),
    'Stimson Hall': (37.5663, 126.9360),
    'Nursing Building': (37.5665, 126.9370)
    }
처음에는 각 건물 간의 위치를 경도와 위도를 이용하여 나타내어 건물의 정보를 입력한다.

 # Step 2: Function to calculate the distance between two coordinates (Haversine formula)
    def haversine(coord1, coord2):
    R = 6371  # Radius of the Earth in km
    lat1, lon1 = coord1
    lat2, lon2 = coord2
    phi1 = math.radians(lat1)
    phi2 = math.radians(lat2)
    delta_phi = math.radians(lat2 - lat1)
    delta_lambda = math.radians(lon2 - lon1)
    a = math.sin(delta_phi / 2) ** 2 + math.cos(phi1) * math.cos(phi2) * math.sin(delta_lambda / 2) ** 2
    distance = 2 * R * math.asin(math.sqrt(a))  # in kilometers
    return distance
각 건물 간의 거리를 구하기 위해 하버사인 공식과 지구의 반지름을 이용하여 각 건물 간 거리의 알고리즘을 구하였다.

# Step 3: Function to calculate the total distance of a given route
    def total_distance(route):
    distance = 0
    for i in range(len(route) - 1):
        distance += haversine(route[i], route[i + 1])
    return distance
다양한 방법으로 각 건물 간 사이의 거리의 합을 구할 수 있는데, 이때 내가 만들어낸 알고리즘에서 건물 수가 적기 때문에 브루트 포스 알고리즘을 활용하였다. 이를 이용하여 건물을 n개 지정했을 때, n!의 경우의 수의 총 거리의 합을 구한다.

# Step 4: Function to solve the Traveling Salesman Problem
    def find_shortest_route(building_names):
    coords = [buildings[name] for name in building_names]
    min_distance = float('inf')
    best_route = None
    for perm in itertools.permutations(coords):
        current_distance = total_distance(perm)
        if current_distance < min_distance:
            min_distance = current_distance
            best_route = perm
브루트 포스 알고리즘을 이용하여 각각의 total distance를 구한 뒤, 각 current distance를 지정하고 알고리즘이 계속 돌아가면서 current distance가 min distance보다 작으면 계속 min distance가 바뀌면서 알고리즘이 n!만큼 돌아갔을 때, 가장 작은 min distance가 best route가 된다.

이후 건물들을 입력해서 각각의 최소 거리를 구하는데, 건물들의 목록을 나타내어 어떠한 건물들을 입력할 수 있는지 나타내기 위해

    # List of available buildings
    available_buildings = list(buildings.keys())
    print("Available buildings for selection:")
    for building in available_buildings:
    print(building)
을 이용하여 어떠한 건물들을 입력할 수 있는지 알 수 있다.

마지막으로, 검색을 하였을 때, 건물을 잘못 입력 했을 때와 제대로 입력 했을 때의 결과를 나타내기 위한 코드를 만들어냈다.

    while True:
    # User input for buildings
    building_names = input("Enter the names of the buildings, separated by commas:        ").split(", ")
    # Check if all entered buildings are valid
    invalid_buildings = [name for name in building_names if name not in buildings]
    if invalid_buildings:
        print(f"The following building(s) are not valid: {',           '.join(invalid_buildings)}")
        print("Please enter the correct building names from the available list.")
    else:
        break
    # Find the shortest route
    shortest_route, shortest_distance = find_shortest_route(building_names)
    # Output the result
    print("The shortest route to visit all buildings is:")
    for i, building in enumerate(shortest_route):
    if i == len(shortest_route) - 1:
        print(f"{building}")
    else:
        print(f"{building} -> ", end="")
    print(f"Total distance: {shortest_distance:.2f} km")

을 이용하였고, 위의 코드에서 확인을 할 수 있다시피 올바르지 않은 코드에 대해서 Please enter the correct building names from the available list.의 결과가 나오고
올바른 코드에 대해서는
building1 -> building2 ->...
Total distance : [  ]km
로 나타낼 수 있다.

# Performance
1. 위 알고리즘의 복잡도를 분석했을 때, O(n!)임을 브루트 포스 알고리즘에서 알 수 있다.
O(n!)의 경우 n이 커질수록 연산 횟수가 급격히 증가하므로 건물의 개수가 많아지면 다른 알고리즘을 유도해내어야 한다.

이에 대해 다양한 알고리즘을 생각할 수 있었는데, 비스마스킹, DP, DFS를 이용하여 해결할 수 있다.
