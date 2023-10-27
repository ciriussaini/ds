## Ques 1 Sliding window Maximum (Hard)
https://leetcode.com/problems/sliding-window-maximum/

3 Approaches

1 O(NlogK) :
<details>
<summary>
using multiset
</summary>
    simple approach: maintaing k size window and removing first element from start

```vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    if (k == 0) return result;
    multiset<int> w;
    for (int i = 0, n = (int)nums.size(); i < n; i++) {
        if (i >= k)
            w.erase(w.find(nums[i-k]));
        w.insert(nums[i]);
        if (i >= k-1)
            result.push_back(*w.rbegin());
        }
    return result;
    }
```
</details>

2 O(NlogN)
<details>
<summary>
using priority queue:
</summary>
storing num and index both and removing top element of PQ if index diff is greater than K

```vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    if (k == 0) return result;
    priority_queue<pair<int, int>> w;
    for (int i = 0, n = (int)nums.size(); i < n; i++) {
        while (!w.empty() && w.top().second <= i-k)
            w.pop();
        w.push(make_pair(nums[i],i));
        if (i >= k-1)
            result.push_back(w.top().first);
    }
    return result;
}

```
</details>

3 O(N)

<details>
<summary>
using deque:
</summary>
remove from front :: to maintain index diff
remove from back :: to maintain greater element

add to back every element i

no changing in order of index happens 


```vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    vector<int> result;
    if (k == 0) return result;
    deque<int> w;
    for (int i = 0, n = (int)nums.size(); i < n; i++) {
        while (!w.empty() && w.front() <= i-k)
            w.pop_front();
        while (!w.empty() && nums[w.back()] <= nums[i])
            w.pop_back();
        w.push_back(i);
        if (i >= k-1)
            result.push_back(nums[w.front()]);
        }
    return result;
    }
```
</details>
