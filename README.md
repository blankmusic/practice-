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
```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public int eraseOverlapIntervals(Interval[] intervals) {
        if(intervals.length == 0) return 0;
        
        Comparator<Interval> comp = new Comparator<Interval>() {
            public int compare(Interval interval1, Interval interval2) {
                if(interval1.end > interval2.end) return 1;
                else if(interval1.end < interval2.end) return -1;
                else return 0;
            }
        };
        
        Arrays.sort(intervals, comp);
        int lastend = intervals[0].end;
        int remove = 0;
        for(int i = 1; i < intervals.length; i++) {
            if(intervals[i].end == lastend) remove++;
            else if(intervals[i].start < lastend) remove++;
            else lastend = intervals[i].end;
        }
        
        return remove;
    }
}
```
