# 二分法

1. 确定边界开闭：
   1. 如果是双闭，那就意味着right能被取到，则right要取数组的长度减一
   2. 如果右开的话，则意味right不能被取到，则right要取数组长度
2. left==right是否有意义？
   1. 如果在1.1的情况下，left==right是没有意义的，因为此时的array[left]已经数组越界
   2. 如果在1.2的情况下则有意义
3. 不断二分缩小边界，直到命中target/循环结束

```
class Solution {
    public int search(int[] nums, int target) {
        int right = nums.length - 1;
        int left = 0;
        while(left <= right){

            int mid = left +((right - left )/2);
            if(nums[mid]>target){
                right = mid - 1;
            }else if(nums[mid] < target){
                left = mid +1;
            }else{
                return mid;
            }

            
        }return -1;
    }
}
```

# 双指针法 - 移除元素

1. 确定指针的功能
   1. fast指针是为了寻找新数组的元素，他只会马不停蹄的往下走
   2. slow指针目标是为新元素指定下标，所以他的功能是定位新元素的下标，因此当fast定位到不需要的元素的时候，slow指针就停止移动，直到fast重新定位到新元素

```
class Solution {
    public int removeElement(int[] nums, int val) {
        int slowIndex = 0;
        for(int fastIndex = 0; fastIndex<= nums.length -1 ;fastIndex ++){
            if (nums[fastIndex] != val){
                nums[slowIndex++] = nums[fastIndex];
            }
        }
        return slowIndex;
    }
}
```

# 快速排序算法：

* 基于双指针+哨兵实现

* 左右两个哨兵，左哨兵寻找比基准数大的数，右哨兵寻找比基准数小的数，哨兵找到目标就停止，等待左右哨兵都寻找到一个目标的时候，哨兵交换数值，而后两哨兵复前行，直至相遇

* 相遇时基准数位置和左哨兵位置交换，此时基准数左边是比基准数小的数字，右边是比基准数大的数字

* 以基准数为分界线，将两个分区各自快排（递归操作）

* 递归的结束标志是：传入的分区只有一个元素（i==j）

```
class Solution {
    public int Quick(int[] nums, int low,int hight) {

        if(low == hight){
            //递归停止条件
            return;
        }

        int i = low,j=hight;
        int key = nums[i];
        while (i < j) {
            
            while (i < j
                    && nums[j] > key) {
                j--;
            }
            while (i < j
                    && nums[i] <= key) {
                i++;
            }
            if(i<j){
                temp = nums[i]
                nums[i] = nums[j];
                nums[j] = temp;
            }
            
            
            }

        Quick(nums,j-1,hight);
        Quick(nums,low,i+1);
    }
}
```
