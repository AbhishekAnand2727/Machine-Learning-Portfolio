
# Ads Click-Through (CTR) Optimization

This repository contains a Reinforcement Learning project to solve the "Multi-Armed Bandit" problem. The goal is to determine which of 10 different ad versions has the highest Click-Through Rate (CTR) in the shortest amount of time, thereby maximizing the total number of clicks.

I implemented and compared two foundational algorithms: **Upper Confidence Bound (UCB)** and **Thompson Sampling**.

---

## Dataset

The dataset (`Ads_CTR_Optimisation.csv`) is a simulation representing **10,000 users** (or "rounds").
* It contains 10 columns, one for each version of the ad.
* Each row represents a user.
* A `1` in a cell means that if this ad (`column`) was shown to this user (`row`), the user clicked it.
* A `0` means the user did not click.

The challenge is that the algorithm can only show **one** ad to each user. It must "explore" all 10 ads to find the best one, and then "exploit" that ad by showing it more often to maximize the total number of clicks.

---

## Algorithms & Approaches

I implemented two different algorithms to solve this "explore-exploit" dilemma:

### How Upper Confidence Bound works:

**UCB score** for each add consists of two parts, it adds up the **Exploration part** and the **Exploitation part**. The main goal for this algorithm is to see what's the best way to find out the ads which are most clicked by people and do it most efficiently. We need to do this in the best possible way, there are two paths :

1. **The Exploitation path**: Once the algorithm finds out the ad with the highest score, it exploits it to get an even higher score. The main                                     drawback of this path is it fails to find out other Ads with higher scores.
2. **The Exploration path**: Once the Ad finds the highest score, it also checks if other Ads have higher scores or not this could lose possible time.

### How UCB combines Exploration and Exploitation in the most optimal amount

The algorithm will assign a **UCB Score** to each Ad which is **The Uncertainity Bonus** + **The Average Reward**. 
**Exploration**:This score consists of **Confidence(or Uncertainity)** it tends to prioritize Ads which it has tested less compared to Ads which have been selected most of the time. **The Uncertainity Bonus** consits of  **whole root(1.5Logt/Ni(t))** where t is the number of rounds totally. Ni(t) is the number of times the Ad is chosen by the algorithm at that round depending on the UCB score.  
                            
**Exploitation**:The score also consists of the **Average Reward** (**Ui(t)=Ri(t)/Ni()**) where **Ri(t)**: is the total number of clicks we have recieved from Ad i until round (t). **Ni(t)** is the total number of times the Ad is chosen by the algorithm at that round depending on the UCB score.(at round 0 it is 0)

The main determiner is  **Ni(t)**, if it's small meaning the uncertainity bonus becomes large (since it's in the denominator). This encourages the algorithm to explore less chosen Ads. When Ni(t) is large then the algorithm is more confident on the Ad and the UCB score will depend more on ui(t) which is the average reward till turn t. 

**UCB= ui(t)+whole root(2/3Log(t)/Ni(t))**


### 2. Thompson Sampling

Since we have already run  **Upper Confidence Bound RL** on the Ads Click Through Optimization DataSet, It got **Ad#5** to be the most selected ad in 1000 rounds for it to be a significant jump over the other ads. **Upper Confidence Bound** is a **Deterministic** Approach whereas Thompson Sampling is a **Probabilistic** Approach. We predict the values of each Ad from the **Probabilty Distribution** of Each Ad and in each round, we draw one random sample from each ad's probability distribution. The ad that pulls the highest sampled value is the one we choose to show.

This probabilistic approach is known as Bayesian inference which naturally balances exploitation and exploration where as UCB had a **Upper Confidence Bound Value** after each and every turn. **Thompsons Sampling does not need to update after every turn** it can update after a bunch of turns and it does not affect the approach. This makes it Optimal For **Website Clicks and Ad clicks** where it would take a lot of processing power to update thousands of clicks immediately. 

**Our final Goal is to find out if Thompson Sampling can beat UCB by finding out that Ad#5 is significantly clicked upon in less than 1000 tries**

## Results: UCB vs. Thompson Sampling

While both algorithms eventually identify **Ad 5** as the clear winner after 10,000 rounds, the true test of efficiency is how *quickly* they converge on the best ad.

To test this, I ran a comparative analysis limiting the simulation to only **500 rounds**.

### UCB at 500 Tries

After 500 rounds, the UCB algorithm was still in a heavy **exploration** phase.

* While **Ad 5** was selected the most, the algorithm was not yet confident in this choice.
* It continued to waste a significant number of selections on other, suboptimal ads (like Ad 2, Ad 7, and Ad 8) to gather more data.
* **Conclusion:** UCB, being a deterministic algorithm, **failed to find and converge on the single best ad** within this short timeframe.

### Thompson Sampling at 500 Tries

In contrast, Thompson Sampling **successfully identified Ad 5 as the most optimal** choice well within the 500-round limit.

* The algorithm's probabilistic (Bayesian) approach allowed it to become "confident" in Ad 5's superior performance much faster.
* It had already shifted from exploration to **exploitation**, dedicating the vast majority of its 500 selections to Ad 5.

### Final Conclusion

This experiment clearly demonstrates that **Thompson Sampling is the more powerful and efficient algorithm** for this dataset. It found the best ad and began maximizing the total reward in a fraction of the time it took the UCB algorithm, which was still exploring. For a business needing to find the best-performing ad quickly to maximize revenue, Thompson Sampling is the superior choice.



