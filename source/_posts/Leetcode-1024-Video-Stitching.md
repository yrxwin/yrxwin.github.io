---
title: '[Leetcode 1024] Video Stitching'
categories:
  - leetcode
author: '大猩猩'
date: 2019-04-12 22:21:16
tags: ['Google']
keywords:
description:
---
#### 原题说明
You are given a series of video clips from a sporting event that lasted `T` seconds.  These video clips can be overlapping with each other and have varied lengths.

Each video clip `clips[i]` is an interval: it starts at time `clips[i][0]` and ends at time `clips[i][1]`.  We can cut these clips into segments freely: for example, a clip `[0, 7]` can be cut into segments `[0, 1] + [1, 3] + [3, 7]`.

Return the minimum number of clips needed so that we can cut the clips into segments that cover the entire sporting event (`[0, T]`).  If the task is impossible, return `-1`.

**Example 1:**
{% blockquote %}
**Input:** `clips = [[0,2],[4,6],[8,10],[1,9],[1,5],[5,9]], T = 10`
**Output:** `3`
**Explanation:** 
We take the clips [0,2], [8,10], [1,9]; a total of 3 clips.
Then, we can reconstruct the sporting event as follows:
We cut [1,9] into segments [1,2] + [2,8] + [8,9].
Now we have segments [0,2] + [2,8] + [8,10] which cover the sporting event [0, 10].
{% endblockquote %}
**Example 2:**
{% blockquote %}
**Input:** `clips = [[0,1],[1,2]], T = 5`
**Output:** `-1`
**Explanation:** 
We can't cover [0,5] with only [0,1] and [0,2].
{% endblockquote %}
**Example 3:**
{% blockquote %}
**Input:** `clips = [[0,1],[6,8],[0,2],[5,6],[0,4],[0,3],[6,7],[1,3],[4,7],[1,4],[2,5],[2,6],[3,4],[4,5],[5,7],[6,9]], T = 9`
**Output:** `3`
**Explanation:**
We can take clips [0,4], [4,7], and [6,9].
{% endblockquote %}
**Example 4:**
{% blockquote %}
**Input:** `clips = [[0,4],[2,8]], T = 5`
**Output:** `2`
**Explanation:**
Notice you can have extra video after the event ends.
{% endblockquote %}

#### 解题思路
先对`clips`按起始段位置从小到大排序。然后我们用贪心算法，用`cur_end`记录当前实际位置的最远端，`potential_end`记录目前可能的最远端。分别初始化为`-1`和`0`。

对clips进行遍历：
1. 当`potential_end`大于T或者`clip`的起始位置大于`potential_end`，意味着之后所有的`clip`都不需要再做考虑了，要么已经满足题意，要么就会出现不能覆盖的区间。
2. 否则，当`clip`的起始位置大于`cur_end`，意味着为了覆盖所有区间，必须更新`cur_end` 和 `potential_end`，同时有一个`clip`需要加入`res`中。

#### 示例代码 (cpp)
```cpp
class Solution {
private:
    static bool clipCmp(vector<int> clipA, vector<int> clipB) {
        return clipA[0] == clipB[0] ? clipA[1] <= clipB[1] : clipA[0] < clipB[0]; 
    }
public:
    int videoStitching(vector<vector<int>>& clips, int T) {
        sort(clips.begin(), clips.end(), clipCmp);
        int res = 0;
        int cur_end = -1; // 当前实际的最远端
        int potential_end = 0; // 当前可能的最远端
        for (auto clip : clips) {
            if (potential_end >= T || clip[0] > potential_end) {
                break;
            }
            else if (clip[0] > cur_end) { //当前的这个clip不可能被选取，需要更新cur_end，并让res++
                res++;
                cur_end = potential_end;
            }
            potential_end = max(potential_end, clip[1]);
        }
        return potential_end >= T ? res : -1;
    }
};
```

#### 复杂度分析
时间复杂度: O(n\*log n)
空间复杂度: O(1)

#### 归纳总结
我们在**Youtube**上更新了[视频讲解](https://youtu.be/tEx3z4L7F-c)，欢迎关注！