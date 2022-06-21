# 최소 신장 트리

## Spanning Tree
 > 그래프 내의 모든 정점을 포함하는 트리
 - Spanning Tree는 그래프의 최소 연결 부분 그래프이다.
 - 즉, 그래프에서 일부 간선을 선택해서 만든 트리

 ### Spanning Tree의 특징
 - DFS, BFS을 이용하여 그래프에서 신장 트리를 찾을 수 있다.
 - 탐색 도중에 사용된 간선만 모으면 만들 수 있다.
 - 하나의 그래프에는 많은 신장 트리가 존재할 수 있다.
 - Spanning Tree는 트리의 특수한 형태이므로 모든 정점들이 연결 되어 있어야 하고 사이클을 포함해서는 안된다.
 - 따라서 Spanning Tree는 그래프에 있는 n개의 정점을 정확히 (n-1)개의 간선으로 연결 한다.

## MST
 > Spanning Tree 중에서 사용된 간선들의 가중치 합이 최소인 트리
 - 각 간선의 가중치가 동일하지 않을 때 단순히 가장 적은 간선을 사용한다고 해서 최소 비용이 얻어지는 것은 아니다.
 - MST는 간선에 가중치를 고려하여 최소 비용의 Spanning Tree를 선택하는 것을 말한다.
 - 즉, 네트워크(가중치를 간선에 할당한 그래프)에 있는 모든 정점들을 가장 적은 수의 간선과 비용으로 연결하는 것이다.

### MST의 특징
 - 간선의 가중치의 합이 최소여야 한다.
 - n개의 정점을 가지는 그래프에 대해 반드시 (n-1)개의 간선만을 사용해야 한다.
 - 사이클이 포함되어서는 안된다.
 
 ![MST예시](https://blog.kakaocdn.net/dn/cAY0yW/btqCBwoBVLE/4PL4BYJQ6JPOo8SREjE7l0/img.png)

### MST 구현방법

#### 1. Kruskal 알고리즘
 > 그래프의 간선들을 가중치의 오름차순으로 정렬한다.
 > 정렬된 간선리스트에서 순서대로 사이클을 형성하지 않는 간선을 선택한다.
 > 즉, 가장 낮은 가중치를 먼저 선택한다.
 > 사이클을 형성하는 간선을 제외한다.
 > 해당 간선을 현재의 MST(최소 비용 신장 트리)의 집합에 추가한다.
 
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;

public class 그래프04_크루스칼 {
	static int[] p;

	public static void main(String[] args) {
		Scanner sc = new Scanner(input);

		int V = sc.nextInt(); // V : 정점의 갯수 인데 0 부터 시작이야
		int E = sc.nextInt(); // E : 간선의 갯수

		// 간선배열을 이용해서 저장을 해야해~~
		int[][] edges = new int[E][3];

		for (int i = 0; i < E; i++) {
			edges[i][0] = sc.nextInt();// [0] 시작점
			edges[i][1] = sc.nextInt();// [1] 끝점
			edges[i][2] = sc.nextInt();// [2] 가중치
		} // 입력 끝

		// 간선을 가중치로 오름차순 정렬을 해야해~~~~
		Arrays.sort(edges, new Comparator<int[]>() {
			@Override
			public int compare(int[] o1, int[] o2) {
				return o1[2] - o2[2];
			}
		});

		p = new int[V];
		// makeset을 하여 나자신을 대표로 초기화 하자.
		for(int i = 0; i<V; i++) {
//			makeSet(i);
			p[i] = i;
		}
		
		int ans = 0;
		
		//mst 만들어 보자.
		//간선을 N-1개 선택하면 break;
		//union이라는 이곳을 쪼금 손대면 어떨까?
		int pick = 0;
		for(int i = 0 ; i<E; i++) {
			int px = findSet(edges[i][0]);
			int py = findSet(edges[i][1]);
			
			if(px != py) {
				union(px, py);
				ans += edges[i][2];
				pick++;
			}
			if(pick == (V-1)) break;
		}

		System.out.println(ans);

	}

	static void makeSet(int x) {
		p[x] = x;
	}
	
	static int findSet(int x){
//		if(x ==p[x]) return x;
//		return p[x] = findSet(p[x]);
		if(p[x] != x) p[x] = findSet(p[x]);
		return p[x];
	}
	
	static void union(int x, int y) {
		p[findSet(y)]= findSet(x); //정석
		
//		p[y] = x ;//이번 경우에서는 이와 같이 작성해도 상관 없음. 
		//어차피 대표를 찾아서 union을 호출할거니까. 
		//항상 왜 사용하는지를 알고 쓰기.
	}
	
	

	static String input = "7 11 \r\n" + "0 1 32\r\n" + "0 2 31\r\n" + "0 5 60\r\n" + "0 6 51\r\n" + "1 2 21\r\n"
			+ "2 4 46\r\n" + "2 6 25\r\n" + "3 4 34\r\n" + "4 6 51\r\n" + "5 3 18\r\n" + "5 4 40\r\n";
}

```

#### 2. Prim 알고리즘 
 > 시작 단계에서는 시작 정점만이 MST(최소 비용 신장 트리) 집합에 포함된다.
 > 앞 단계에서 만들어진 MST 집합에 인접한 정점들 중에서 최소 간선으로 연결된 정점을 선택하여 트리를 확장한다.
 > 즉, 가장 낮은 가중치를 먼저 선택한다.
 > 위의 과정을 트리가 (N-1)개의 간선을 가질 때까지 반복한다.


```java
import java.util.ArrayList;
import java.util.List;
import java.util.PriorityQueue;
import java.util.Scanner;

public class 그래프05_프림2 {
	static class Edge implements Comparable<Edge> {
		int st;
		int ed;
		int cost;

		public Edge(int st, int ed, int cost) {
			this.st = st;
			this.ed = ed;
			this.cost = cost;
		}

		// 우선 순위 큐를 만드는데 최소 힙
		@Override
		public int compareTo(Edge o) {
			return this.cost - o.cost;
//			return Integer.compare(this.cost, o.cost);
		}
	}

	public static void main(String[] args) {
		Scanner sc = new Scanner(input);

		int V = sc.nextInt(); // 정점의 갯수
		int E = sc.nextInt();

		// 간선의 정보를 저장을 해야되는데
		// 인접 리스트

		List<Edge>[] adjList = new ArrayList[V];

		for (int i = 0; i < V; i++)
			adjList[i] = new ArrayList<>();

		for (int i = 0; i < E; i++) {
			int st = sc.nextInt();
			int ed = sc.nextInt();
			int w = sc.nextInt();

			adjList[st].add(new Edge(st, ed, w));
			adjList[ed].add(new Edge(ed, st, w));
		}

		boolean[] visited = new boolean[V];// 박문철2 용도

		PriorityQueue<Edge> pq = new PriorityQueue<>();

		visited[0] = true;// 0번부터 시작할꺼야

		pq.addAll(adjList[0]); // 이거 몽땅 넣어줘잉

		int cnt = 1; // 확보한 정점의 갯수
		int ans = 0;

		while (cnt != V) {
			Edge edge = pq.poll(); // 간선 하나 꺼내기.
			// 이미 확보한 정점이면... 넘어가
			if (visited[edge.ed])
				continue;

			ans += edge.cost;
			pq.addAll(adjList[edge.ed]);
			visited[edge.ed] = true;
			cnt++;
		}
		System.out.println(pq.size());

		System.out.println(ans);

	}// main

	static String input = "7 11 \r\n" + "0 1 32\r\n" + "0 2 31\r\n" + "0 5 60\r\n" + "0 6 51\r\n" + "1 2 21\r\n"
			+ "2 4 46\r\n" + "2 6 25\r\n" + "3 4 34\r\n" + "4 6 51\r\n" + "5 3 18\r\n" + "5 4 40\r\n";
}
```

### 관련문제
 - [BOJ_1197최소 스패닝 트리](https://www.acmicpc.net/problem/1197)

 ### 참고문서
  - https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html
