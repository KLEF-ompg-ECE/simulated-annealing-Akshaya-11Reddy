# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Guggilla Akshaya  
**Student ID    :** 2310040011  
**Date Submitted:** 25th march

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
The count_clashes() function measures the number of conflicts in the timetable where multiple exams are scheduled in the same time slot for students. It counts how many clashes occur across all subjects. A value of 0 means a perfect timetable with no scheduling conflicts.
Q2
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
The generate_neighbor() function creates a new timetable by making a small random change to the current timetable, such as moving a subject to a different slot or swapping slots. The new timetable is slightly different from the current one. This allows the algorithm to explore nearby possible solutions.

```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept a new solution based on its quality and the current temperature. If the new solution is better (delta < 0), it is always accepted. If it is worse, it may still be accepted with a certain probability, which helps the algorithm escape local minima and explore better solutions.

```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379|
| Clashes at iteration 1 | 12|
| Final best clashes | 3|
| Did SA reach 0 clashes? (Yes / No) | No|

**Copy the printed timetable output here:**
```
  Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The graph shows a rapid decrease in clashes during the early iterations, indicating that the algorithm quickly improves the timetable. After several iterations, the curve begins to flatten, showing slower improvement. The algorithm stabilizes at 3 clashes, indicating convergence without reaching a perfect timetable.

```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|----------- --|---------------|----------------------|--------------------|
| 0.80         |       8       |       ~30            |         no         |
| 0.95         |       3       |       ~130           |         no         |
| 0.995        |       3       |       ~1379          |         no         |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
 When the cooling rate is fast (0.80), the temperature drops quickly and the algorithm converges very early, resulting in a higher number of clashes. With a moderate cooling rate (0.95), the algorithm continues exploring longer and reduces clashes more effectively. With a slow cooling rate (0.995), the algorithm explores the solution space thoroughly and gradually improves, but takes many more iterations. This shows that slower cooling improves solution quality but increases computation time.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
The cooling rate of 0.95 gave the best balance between performance and efficiency. It achieved a low number of clashes similar to the slowest cooling rate but required significantly fewer iterations. Therefore, it provides a good trade-off between speed and solution quality.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3| The algorithm reduces clashes effectively but may not reach zero|
| 2 — Cooling rate | cooling_rate = ___ | 3| Moderate cooling gives good results with fewer iterations|

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
From these experiments, I learned that the cooling rate is a crucial parameter in Simulated Annealing. A fast cooling rate leads to quick convergence but may result in poor solutions due to limited exploration. A slow cooling rate allows thorough exploration and improves solution quality but increases computation time. A moderate cooling rate provides a good balance between efficiency and performance. Accepting worse solutions at higher temperatures helps the algorithm escape local minima and find better solutions.
```

---

## Submission Checklist

- [ ] Student name and ID filled in
- [ ] Q1, Q2, Q3 answered
- [ ] Experiment 1: table filled, timetable pasted, plot observation written
- [ ] Experiment 2: results table filled (3 rows), observation and answer written
- [ ] Summary table completed and reflection written
- [ ] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
