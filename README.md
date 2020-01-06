# leetcode_practice
A project for arithmetic study , daily update        

[1.给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。](#1.给定一个大小为n的数组。找到其中的多数元素。多数元素是指在数组中出现次数大于⌊n/2⌋的元素)

[2.给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。](#2.给定一个数组nums，编写一个函数将所有0移动到数组的末尾，同时保持非零元素的相对顺序。)

# 1.给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:
输入: [3,2,3]
输出: 3

示例 2:
输入: [2,2,1,1,1,2,2]
输出: 2

解题：

```
    public int majorityElement(int[] nums) {
        //投票算法
        int count = 1;
        //将起始值作为计数开始的值
        int temp = nums[0];

        for (int i = 1; i < nums.length; i++) {
            //若遇到一样的+1遇到不一样的-1
            if (temp == nums[i]) {
                count++;
            } else {
                count--;
            }
            if (count == 0) {
                //当计数器重新为0的时候说明前面的数全都抵消，假设下一个数为众数。题目假设必有众数，也就是该数出现的次数比其他数加起来出现的次数都多
                temp = nums[i + 1];
            }
        }
        return temp;
    }
```
优化后：
```
    public int majorityElement(int[] nums) {
        //投票算法
        int count = 0;
        //将起始值作为计数开始的值
        Integer temp = null;
        for (Integer num : nums) {
            //若计数器为0，则将循环中的元素赋值给temp
            if (count == 0) temp = num;
            //计算count值，进行下一次轮询
            count += temp.equals(num) ? 1 : -1;
        }
        return temp;
    }
```
# 2.给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

题解：
```
    public void moveZeroes(int[] nums) {
        //思路 1.使用index记录下当前不为0的数的位置
        int index = 0;
        for (Integer num : nums) {
            if (num != 0) {
                //将每个不等于0的数字按照顺序往数组中排列，并增加index值
                nums[index++] = num;
            }
        }
        //最后将index后面的值赋值为0
        while (nums.length - index > 0) {
            nums[index++] = 0;
        }
    }
```
