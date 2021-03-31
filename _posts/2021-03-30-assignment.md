# Closest Pair

## 최근접 점의 쌍 찾기



 Closest Pair 문제는 모든 점에 대하여 각각의 두 점 사이의 거리를 계산하여 가장 가까운 점의 쌍을 찾는 방법을 이용한다.  간단한 방법으로는 모든 점에 대하여 각각의 두 점 사의 거리를 계산하는 방법이 있지만, 이 방법은 시간 복잡도 O(n^2)으로 점의 갯수가 많아질수록 걸리는 시간은 기하급수적으로 늘어난다는 단점이 있다.



아래는 분할정복을 이용한 코드이다.

![그림](https://www.cs.mcgill.ca/~cs251/ClosestPair/figure3.2.gif)

```
public void divide(point[] p, int n,int m){     //분할 정복
        if(m-n < 3){
            measure_distance(p,n,m);
            return;
        }
        int k = (n+m)/2;
        divide(p,n,k); //x축을 절반으로 나누어 분할시킨다.
        divide(p,k+1,m);
        min_distance(p,n,k,m);
    }

```

앞에서 입력된 배열 p을 합병 정렬을 통해 x의 크기에 따라 배열된 것을 분할을 해야한다. 이때 분할된 영역의 점의 개수가 3개보다 작으면 measure_distance를 통하여 최소 거리를 측정하고 만족하지 않으면(3개 이상이면) 추가적인 거리를 비교해야하기 때문에 다시 분할을 해야하는데, 이를 조건문 if(m-n<3)을 이용해 표현했다. 또한 아래 코드는 n은 시작점, m 종점으로 그 중앙값인 k를 구하고 이를 divde를 통해 분할하고 거리를 측정하는 것을 보여준다.