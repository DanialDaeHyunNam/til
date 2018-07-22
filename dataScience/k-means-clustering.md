## K-Means clustering

독립 변수의 특성이 유사한 데이터의 그룹을 **Cluster** 이라고 한다. 클러스터의 개수가 K라면 클러스터링은 데이터가 어떤 클러스터에 속하는지 예측하는 작업이다.
<br>
<br>
```Python
from sklearn.cluster import KMeans
model = KMeans(n_clusters=2, init="random", n_init=1,
               max_iter=1, random_state=1).fit(X)
"""
KMeans에 들어간 첫 번째 Parameter를 보면 n_clusters를 미리 지정해주게 되어있다.
max_iter를 통해서 몇번 시도할 것인지를 결정한다.

알고리즘은
1. 임의의 중심값을 고른다. (보통 데이터 샘플 중의 하나를 선택)
2. 중심에서 각 샘플 데이터까지의 거리를 계산
3. 각 데이터 샘플에서 가장 가까운 중심을 선택하여 클러스터 갱신
4. 다시 만들어진 클러스터에 대해 중심을 다시 계산하고 1 ~ 4를 반복한다.
"""           
```

#### K-means Score의 의미
Inertia를 구한 값이다. 모든 데이터별로 가장 가깝다고 판단한 클러스터 중심과의 거리를 구한 후에 제곱한 값의 Sum값을 의미한다.

```python
from sklearn.cluster import KMeans
X = np.array([[7, 5], [5, 7], [7, 7], [4, 4], [4, 6], [1, 4],
              [0, 0], [2, 2], [8, 7], [6, 8], [5, 5], [3, 7]])
plt.scatter(X[:, 0], X[:, 1], s=100)
plt.show()
model1 = KMeans(n_clusters=2, init="random", n_init=1,
               max_iter=1, random_state=1).fit(X)
c0, c1 = model1.cluster_centers_
print(c0, c1)
def kmeans_df(model, c0, c1):
    df = pd.DataFrame(np.hstack([X,
                                 np.linalg.norm(X - c0, axis=1)[:, np.newaxis],
                                 np.linalg.norm(X - c1, axis=1)[:, np.newaxis],
                                 model.labels_[:, np.newaxis]]),
                      columns=["x0", "x1", "d0", "d1", "c"])
    return df
df = kmeans_df(model1, c0, c1)
print(df)
df_0 = df[df["c"] == 0]
df_1 = df[df["c"] == 1]
print()
print("sum(df_1[\"d1\"] ** 2) + sum(df_0[\"d0\"] ** 2) 의 값 : ", end=" ")
print(sum(df_1["d1"] ** 2) + sum(df_0["d0"] ** 2))
print()
print("model1.score(X) 의 값 : ", end=" ")
print(model1.score(X))
```


#### 클러스터링 성능 기준
성능 기준은 정확한 답(클러스터의 개수 및 소속)을 알고 있는 경우와 그렇지 않은 경우에 따라 다른 방식을 사용하게 된다.<br>

##### 답을 알고 있는 경우

정확한 답을 알고 있는 경우에는 **Homogeneity, completeness, V-measure** 를 사용하게 된다.
- Homogeneity : 각 클러스터가 단일 클래스의 데이터만 가지는 정도<br>
**h = 1 - H[C|K] / H[C]**
- Completeness : 같은 클래스의 값이 하나의 클러스터로 모여있는 정도<br>
**c = 1 - H[K|C] / H[K]**
- V-measure : Homogeneity, Completeness의 조화 평균<br>
**v = 2 * (h * c) / h + c**
<br>
**H[C] : 클래스 엔트로피. 여러 클래스에 분산되어 있으면 커진다.** <br>
**H[C|K] : 클러스터링이 끝난 후의 클래스 엔트로피.** <br>
**H[K] : 클러스터 엔트로피. 여러 클러스터에 분산되어 있으면 커진다.** <br>
**H[K|C] : 클래스 별로 분류한 후의 클러스터 엔트로피.**

##### 답을 모르는 경우
**실루엣 계수(Silhouette Coefficient)** <br>
s = b - a / max(a, b) <br>
- a : 같은 클러스터에 속한 원소들의 평균 거리
- b : 다른 클러스터 중 가장 가까운 클러스터까지의 평균 거리
**s값이 음수로 나오는 경우는 이상적이지않은 클러스터로 볼 수 있다.**
