# #practice-在线编程
# 图的遍历
```java
import java.util.*;
public class Main {
    private static int m;
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        List<List<Integer>> children = new ArrayList<>(N);
        for(int i = 0; i < N; i++) {
            children.add(new LinkedList<>());
        }
        while(sc.hasNextInt()) {
            int a = sc.nextInt();
            int b = sc.nextInt();
            children.get(a-1).add(b-1);
            children.get(b-1).add(a-1);
        }
        dfs(children);
        System.out.println(2*(N-1) - m);
    }
 
    private static void dfs( List<List<Integer>> children) {
        Queue<Integer> queue=new LinkedList<>();
        queue.add(0);
        boolean[] visit=new boolean[children.size()];
        visit[0]=true;
        while(queue.size()!=0){
            m++;
            int size=queue.size();
            while(size-->0){
                int ret=queue.poll();
                List<Integer> retList=children.get(ret);
                for(Integer t:retList){
                    while(!visit[t]){
                        queue.add(t);
                        visit[t]=true;
                    }
                }
            }
        }
       m--;
}
}
```
# 非递归实现树的前-中-后-层-序遍历

# leetcode435 区间覆盖问题

