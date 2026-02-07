# 07-02-2026
#
#theory
#today i complete sura anna topics
✅ What is given?

You have:
1️⃣ An integer array
Example:

nums = [1, 12, -5, -6, 50, 3]
2️⃣ An integer k
k = 4
✅ What is a "contiguous subarray"?

Contiguous = elements must be next to each other (no skipping).

Examples for above array:

Valid (contiguous):

[1, 12, -5, -6]
[12, -5, -6, 50]
[-5, -6, 50, 3]


Invalid:

[1, -5, 50, 3] ❌ (skipped elements)

✅ What do you need to find?
Step 1:

Pick subarrays of length k only  

Here k = 4, so length must be 4.

So possible subarrays:

[1, 12, -5, -6]
[12, -5, -6, 50]
[-5, -6, 50, 3]

Step 2:

Find average of each

Formula:

average = sum / k

Step 3:

Return the maximum average

✅ Example calculation
Subarray 1
[1, 12, -5, -6]
sum = 1+12-5-6 = 2
avg = 2/4 = 0.5

Subarray 2
[12, -5, -6, 50]
sum = 51
avg = 51/4 = 12.75

Subarray 3
[-5, -6, 50, 3]
sum = 42
avg = 42/4 = 10.5

✅ Maximum average
max(0.5, 12.75, 10.5) = 12.75


So answer:

12.75

✅ In simple sentence

👉
"From all consecutive groups of size k, find the one whose average is largest."

✅ Key points

✔ Must be contiguous
✔ Length must be exactly k
✔ Calculate average
✔ Return maximum

If you'd like, next I can explain:
✅ brute force method
✅ sliding window method (best solution, O(n))
✅ with code
✅ with dry run

Just tell 👍

give me hints

Great 👍 let’s solve it step-by-step using hints only (not full solution).

🔹 Hint 1 — Understand the goal

You are not asked to:
❌ find all averages
❌ return subarray

You only need:
✅ maximum average value

🔹 Hint 2 — Brute force thinking first

Ask yourself:

👉 For every subarray of length k
👉 calculate sum
👉 calculate average
👉 track maximum

This works but…

Time complexity = O(n × k) (slow for large input)

🔹 Hint 3 — Notice something important

When moving from one subarray to the next:

Example:

[1, 12, -5, -6]
[12, -5, -6, 50]


What changed?

👉 First element removed → 1
👉 New element added → 50

So instead of recomputing sum again:

new_sum = old_sum - removed + added

🔹 Hint 4 — Use Sliding Window

This problem is perfect for Sliding Window technique

Steps:

Step 1

Find sum of first k elements

Step 2

Loop from k → n-1:

window_sum = window_sum - nums[i-k] + nums[i]

Step 3

Keep updating max_sum

🔹 Hint 5 — Avoid extra work

Since:

average = sum / k


k is constant

So:
👉 maximizing sum = maximizing average

So you can:
✔ compare sums directly
✔ divide once at the end

🔹 Hint 6 — Final complexity

Sliding window gives:

Time  = O(n)
Space = O(1)

class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        n=len(nums)
        curr_sum=0
        for i in range(k):
            curr_sum+=nums[i]
        max_avg=curr_sum/k
        for i in range(k,n):
            curr_sum+=nums[i]
            curr_sum-=nums[i-k]
            avg=curr_sum/k
            max_avg=max(max_avg,avg)
        return max_avg
