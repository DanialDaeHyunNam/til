## Hierarchy clustering
계층적 클러스터링은 데이터 하나하나를 클러스터로 보고 가장 유사도(거리가 가까운)가 높은 클러스터를 합치면서 개수를 줄여가는 방법이다. 거리 측정에는 두가지 방법이 있다.
- 비귀납적 방법
  + Centroid : 두 클러스터의 중심점을 정의한 다음 두 중심점의 거리를 클러스터간의 거리로 정의한다.
  + Single : 클러스터 u의 모든 데이터 i와 클러스터 v의 모든 데이터 j의 모든 조합에 대해 거리를 측정해서 최소값을 구한다.
  + Complete
  Single과 반대로 모든 조합에 대한 거리 중 가장 큰 값을 구한다.
  + Average
  각 클러스터의 데이터간의 모든 조합에 대한 거리를 측정한 후 평균을 구한다.
- 귀납적 방법
  + Median : 클러스터가 서로 합해질 때마다 새로 거리를 계산하여 중심점을 찾는 것이 아니라, 두 개의 클러스터 중심점의 평균을 사용한다.
  + Weighted : u가 클러스터 s와 클러스터 t가 결합하여 생겼다면<br>
  d(u, v) = (dist(s, v) + dist(t, v))/2를 사용해서 거리를 구한다.
  + Ward : 만약 클러스터 u가 클러스터 s와 클러스터 t가 결합하여 생겼다면 두 클러스터의 거리의 가중 평균에서 원래의 두 클래스터 사이의 거리를 보정한 값을 사용한다.

```python
from scipy.cluster.hierarchy import linkage, dendrogram
np.set_printoptions(precision=5, suppress=True)

np.random.seed(4711)  # for repeatability of this tutorial
a = np.random.multivariate_normal([10, 0], [[3, 1], [1, 4]], size=[100,])
b = np.random.multivariate_normal([0, 20], [[3, 1], [1, 4]], size=[50,])
X = np.concatenate((a, b),)

mpl.rcParams["font.family"] = 'DejaVu Sans'
plt.figure(figsize=(10,30))
ax = plt.subplot(111)
dendrogram(Z, leaf_font_size=10, orientation='right')
plt.title('Hierarchical Clustering Dendrogram')
plt.xlabel('sample index')
plt.ylabel('distance')
ax.set_xlim(xmin=0.03)
ax.set_xscale('log')
plt.show()
```
