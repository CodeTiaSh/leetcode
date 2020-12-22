[leetcode 01 Two Sum](https://leetcode.com/problems/two-sum/)

解析：数组元素无序且有重复，不能对数组元素进行排序，通过空间换取时间，使用Map以值作为key，数组下标作为value，时间复杂度o(n)。

1、遍历数组两遍

```java
public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        int index = 0;
        for (Integer value : nums) {
            map.put(value, index++);
        }

        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i]) && i != map.get(target - nums[i])) {
                return new int[]{i, map.get(target - nums[i])};
            }
        }
        return new int[]{-1, -1};
    }
```

2、遍历数组一遍

```java
public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{map.get(target - nums[i]), i};
            } else {
                map.put(nums[i], i);
            }
        }
        return new int[]{-1, -1};
 }
```

