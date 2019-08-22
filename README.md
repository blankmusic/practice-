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
```java
package Algorithm.LC;

import Algorithm.commons.TreeNode;

import java.util.*;

/**
 * @auther G.Fukang
 * @date 8/16 21:32
 */
public class Tree {
    /**
     * 前序遍历
     */
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        Stack<TreeNode> stack = new Stack<>();
        // 压入一个节点
        stack.push(root);
        while (!stack.isEmpty()) {
            // 弹出一个节点
            TreeNode node = stack.pop();
            if (node == null) {
                continue;
            }
            // 记录
            res.add(node.val);
            // 栈存储：先压入后遍历，应该先压入右子树后压左子树
            stack.push(node.right);
            stack.push(node.left);
        }
        return res;
    }

    /**
     * 中序遍历
     */
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curNode = root;
        while (curNode != null || !stack.isEmpty()) {
            while (curNode != null) {
                // 不断入栈直到左子树为空
                stack.push(curNode);
                curNode = curNode.left;
            }
            // 出站
            TreeNode node = stack.pop();
            // 记录
            res.add(node.val);
            curNode = node.right;
        }
        return res;
    }

    /**
     * 后序遍历
     */
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        Stack<TreeNode> stack = new Stack<>();
        // 压入一个节点
        stack.push(root);
        while (!stack.isEmpty()) {
            // 弹出一个节点
            TreeNode node = stack.pop();
            if (node == null) {
                continue;
            }
            // 记录
            res.add(node.val);
            // 更改前序为：根右左 -> 后续遍历为 左右根，反转
            stack.push(node.left);
            stack.push(node.right);
        }
        Collections.reverse(res);
        return res;
    }

    /**
     * 层序遍历
     */
    public ArrayList<ArrayList<Integer>> Print (TreeNode pRoot) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if (pRoot == null) {
            return res;
        }
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(pRoot);
        while (!queue.isEmpty()) {
            int size = queue.size();
            ArrayList<Integer> list = new ArrayList<>();
            while (size-- > 0) {
                TreeNode node = queue.remove();
                // 记录
                list.add(node.val);
                // 左右子树入队
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
            // 记录
            res.add(new ArrayList<>(list));
        }
        return res;
    }
}

```

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
# 最长全1串
