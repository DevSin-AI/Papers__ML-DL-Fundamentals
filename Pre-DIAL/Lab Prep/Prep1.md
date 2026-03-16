2026-02-09  

Title: Why is Normalization Necessary for Linear Recommenders?

Venue (Conference/Journal):  The 48th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR), Padua, Italy, July 13-17, 2025
Link: https://arxiv.org/abs/2504.05805

<Topic>
How normalization affects LAEs - with a focus on popularity and neighborhood biases,
Proposes Data Adaptive Normalization
  Information systems → Recommender systems.
  Collaborative filtering; linear autoencoders; normalization; popularity bias; neighborhood bias

==============================  
I.
===

1) Category (type of paper)  
- Method / Applied research paper  

2) Problem & Context  
- Core problem the paper addresses:
  LAE can achieve competitive gain over non-linear but has;
   - Popularity bias (learned weight matrix is influenced by popular items leading it to be excessively recommended)
   - Neighborhood bias (focus too much on local item relationships of individual preference of extreme case users, 활동량 많은 사용자들이 만든 아이템 관계에 과다집중)
- The basis of Approach:
  Normalization
    Mathematically analyze Normalization and its effects on biases
    Suggest a 'Data-Adaptive' normalization (has item-adaptive + user-adaptive normalization)

- Why this problem is important:
  LAEs are used widely in practice due to their efficiency, and being less prone to overfit in sparse user-item relationships. However, their performance and fairness is sensitive to biases.
  Midigating biases via normalization could make linear systems more reliable without much increased complexity.

- 2–3 key related approaches or prior work:  to-be-continued; 

3) Assumptions & their correctness  
- Explicit assumptions:  
  - LAE-based recommenders are representative of efficient recommender systems // this is important
  - Popularity bias and neighborhood bias are undesirable behaviors // we don't want this
  - Interaction data can be meaningfully normalized without changing its semantic meaning // we can normalize - it's just reshaping, no significant loss

- Implicit assumptions:  
  - Normalization is a dominant factor driving these biases, or at least a dominant enough one.
  - Changing normalization affects bias more than it harms recommendation quality.
  - Bias patterns observed in offline evaluation reflect real-world behavior

- Most questionable or risky assumption:
 Implicit[1] >> there might be an even better solution, core cause of biases?

4) Main contributions (one line each)  
- C1: first to mathematically analyze normalization methods on LAEs
- C2: proposes DAN that adjusts the degree of biases by dataset characteristics
- C3: demonstrates DAN achieve superior performance over 14 CF models on 6 datasets, and add negligible costs

5) Clarity  
- Is the structure clear? Yes 
- Do figures help understanding? Yes
- Reproducibility: High

==============================  
II.
1–2 hours — Conceptual understanding (Second Pass)  
=== 

1) Summary of the main idea (≤ 5 lines)  
-  

2) Core structure of the method  
- Input:  
- Model / Algorithm:  
- Output:  
- Key insight or trick:  

3) Figures and experiments  
- Meaning of x-axis:  
- Meaning of y-axis:  
- Are comparisons fair? (Yes/No)  
- Are error bars shown? (Yes/No)  
- Do the results actually justify the claims?  

4) References to read later (pick 3)  
- R1: Probably for a survey read on Recommenders, focus on biases.
Jiawei Chen, Hande Dong, Xiang Wang, Fuli Feng, Meng Wang, and Xiangnan He.
2023. Bias and Debias in Recommender System: A Survey and Future Directions.
ACM Trans. Inf. Syst. 41, 3 (2023), 67:1–67:39.

- R2:  
- R3:  

==============================  
III.
2–4 hours — Reconstruction & critique (Third Pass)  
===
0) General Questions
- If bias is a problem - isn't noticing where the problem happens first better than simply fixing a part that helps?

1) Challenge the assumptions  
- Case where the method would fail:  
  -  

2) If I redesigned this work  
- What I would simplify:  
- What I would change:  

3) Future work ideas  
- Extension idea:  
- Connection to another paper:  
- Connection to my interests (XAI / Efficient ML / Data-centric ML):  

4) Anything to Add

==============================
The following summery is done by a format inspired by 'Three Pass Approach' written by S.Keshav
(https://jongwuklee.weebly.com/uploads/4/4/8/0/44808947/p83-keshav.pdf)