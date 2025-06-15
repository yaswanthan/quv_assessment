# Problem Setting

You are an assistant to the king, who has scheduled a party tomorrow. There are **1000 wine bottles** in the king's possession, and unfortunately, **3 of them are poisonous**. Consuming from any of these bottles will result in death the following day.

Your task is to identify the **3 poisonous bottles by tomorrow morning** to ensure the safety of all the guests.

## Possible Solution

You have the option to use **prisoners** to help you in this endeavor. One possible approach is to assign each of the 1000 prisoners to drink from a different bottle. By observing the 3 prisoners who die the next day, you can determine which bottles are poisonous.

---

## Objective

However, your challenge is to find a solution that **uses the fewest number of prisoners possible** to achieve this objective.

We request you to create a document outlining your solution and explaining the algorithm you have developed for this task.

---

# Solution Approaches

## Approach 1: Grouping Wines for Testing

In this method, we **combine every 3 glasses of wine into a single batch** and give that batch to one prisoner. Since there are 1000 glasses, we can divide them into **333 groups of 3**, and we’ll need **1 extra prisoner** to test the remaining glass — making a total of **334 prisoners**.

On the next day, in the **worst-case scenario**, **3 prisoners could die**, indicating that up to **9 glasses** (3 batches of 3) are poisoned and should not be served at the party.

If we have **another day** for testing, we can test those 9 suspicious glasses by again test them using **9 more prisoners**. This allows us to **identify the exact 3 poisoned glasses**.

**Total number of prisoners used** becomes:  
- 334 (initial round)  
- +9 (second round of testing individually)  
= **343 prisoners**

---

## Approach 2: Binary (Bitwise) Testing

This approach leverages the **binary system**, which fits well because each prisoner can either **live or die** — just **two outcomes**.

We need to identify which **3 out of the 1000 wine glasses** are poisoned. The number of such possible combinations is:  
**1000C3 ≈ 16.6 million**

To uniquely represent each of these combinations, we calculate the number of bits needed:  
**log₂(16.6 million) ≈ 28 bits**  

Each wine glass is assigned a unique **28-bit binary number** from 1 to 1000. Each **bit position corresponds to a specific prisoner** — a `1` in the bit means that prisoner drinks that glass, and a `0` means they don't.

**Example**:  
Wine glass #5 → Binary: `0000000000000000000000000101`  
Here, **prisoners at positions 26 and 28** (counting from right to left) would taste this glass.

By observing **which prisoners die**, we can reconstruct the **binary number** that corresponds to each poisoned glass, and thus identify **exactly which glasses are poisoned** — all using just **28 prisoners**.

---

## Files

I will attach:
- An **Excel** file for 1000 glasses with 3 poisoned and 6 glasses with 2 poissoned
- An **IPython Notebook** for simulations
- A **mini example** with 6 glasses and 2 poisoned bottles
