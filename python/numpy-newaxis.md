## Numpy.newaxis

|  |  |
| :-: | :-: |
| **A =np.array([2, 0, 1, 8])** |
| **A.shape(4,)** |
| **A[np.newaxis, :]** | **A[:,np.newaxis]** |
| **array(\[[2, 0, 1, 8]])** | **array(\[[2], [0], [1], [8]])** |
| **A.shape(1, 4)** | **A.shape(4, 1)** |
| **Row Vector** | **Column Vector** |
