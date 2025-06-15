
# Traffic Jitter Optimization Problem

## Problem Statement

You are given:

- **20 traffic types**, each with a **maximum tolerable jitter limit** (e.g., 50, 100, 200 ms).
- **20 network links**, where each link is represented as a tuple `(latency, bandwidth)`.

### Jitter Calculation

If a traffic type uses multiple links, jitter is defined as:

```

Jitter = max(latency) - min(latency)

````

If the computed jitter is within the traffic type's allowable threshold, the traffic can use the combination, and the **total usable bandwidth** is the sum of the individual link bandwidths.

#### Example

Given two links:

- Link A: `(200 ms, 50 Mbps)`
- Link B: `(300 ms, 20 Mbps)`

Jitter = `300 - 200 = 100 ms`.  
If a traffic type has a jitter threshold of 120 ms, it can use both links, and total bandwidth = `50 + 20 = 70 Mbps`.

---

## Objective

Write a Python program that:

- Accepts 20 traffic types with different jitter thresholds.
- Accepts 20 links with random latency and bandwidth values.
- For each traffic type, finds the **maximum bandwidth** that can be allocated while ensuring jitter stays within the allowed threshold.

---

## Approaches

### Approach 1: Brute Force

1. Iterate over each traffic type.
2. Generate **all possible combinations** of the available links.
3. For each combination:
   - Compute `jitter = max(latency) - min(latency)`.
   - If within threshold, calculate total bandwidth.
4. Track and select the combination with **maximum bandwidth** that satisfies the jitter constraint.

---

### Approach 2: Optimized (Sliding Window on Sorted Links)

1. **Sort** the links by latency.
2. For each traffic type:
   - Use a **sliding window** over the sorted list.
   - Expand the window as long as `max_latency - min_latency ≤ jitter_threshold`.
   - For each valid window, compute and track total bandwidth.
   - Shrink the window when jitter exceeds the threshold.

## Output

For each traffic type, the script will output:

- The best combination of links.
- The total bandwidth provided.
- The jitter observed.

---