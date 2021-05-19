**768
思路：单调栈**
维持一个单调递增栈，存储每个块中的最大值，最终单调栈的长度就是可分块的大小。

class Solution {
    public int maxChunksToSorted(int[] arr) {
        Stack<Integer> stack = new Stack<>();
        // new一个栈对象
        int ans = 0;
        for(int num:arr){
            if(!stack.isEmpty() && num < stack.peek()){
                int tmp = stack.pop();
                while(!stack.isEmpty() && num < stack.peek()){
                    stack.pop();
                }
                stack.push(tmp);
                // 遍历整个数组，当栈不空且栈顶元素大于当前比较元素则出栈，且更新成新的最大值，不增加栈的长度
            }
            else{
                stack.push(num);
                // 如果栈空或栈顶元素小于当前比较元素，则栈顶元素入栈，栈的长度加一
            }
        }
        return stack.size();
    }
}
时间复杂度:O(N)
空间复杂度:O(N)
