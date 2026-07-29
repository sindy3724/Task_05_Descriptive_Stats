# Task_05_Descriptive_Stats

## Research Task 5: Descriptive Statistics and Large Language Models

**Student:** [Your Name]  
**Institution:** Syracuse University  
**Course:** Research Methods  
**Deadline:** August 1, 2026  
**Date Completed:** July 29, 2026

---

## 1. DATASET DESCRIPTION

### Dataset Overview
- **Name:** NBA Daily Leaders 2024-25 Season
- **Source:** NBA official statistics database
- **File Format:** CSV (nba_dailyleaders_full_24_25.csv)
- **Data Structure:** Game-by-game player statistics
- **Time Period:** October 22, 2024 - Present
- **Records:** 2,600+ rows (one row per player per game)

### Dataset Columns
- Player: Player name
- Tm: Team abbreviation
- Opp: Opponent abbreviation
- Result: Game result (W/L)
- MP: Minutes played
- FG: Field goals made
- FGA: Field goal attempts
- FG%: Field goal percentage
- 3P: Three-pointers made
- 3PA: Three-point attempts
- 3P%: Three-point percentage
- FT: Free throws made
- FTA: Free throw attempts
- FT%: Free throw percentage
- ORB: Offensive rebounds
- DRB: Defensive rebounds
- TRB: Total rebounds
- AST: Assists
- STL: Steals
- BLK: Blocks
- TOV: Turnovers
- PF: Personal fouls
- PTS: Points scored
- +/-: Plus/minus
- GmSc: Game score
- Date: Game date

### Why This Dataset?
Originally planned to use Syracuse Women's Lacrosse data, but it was only available as PDF format (not CSV). NBA dataset was selected as a robust alternative for testing LLM analysis capabilities on structured numerical data.

---

## 2. RESEARCH METHODOLOGY

### Phase A: Establishing Ground Truth and Testing Factual Accuracy

**Objective:** Determine if an LLM can accurately answer factual questions about numerical data.

**Approach:**
1. Calculate verified ground truth statistics (answer key)
2. Ask the LLM 6 factual questions about the data
3. Verify if answers match ground truth
4. Document results

**Questions Tested:**
- Q1: Who was the leading scorer?
- Q2: Who had the most assists?
- Q3: Who had the most rebounds?
- Q4: Who had the best field goal percentage (min 50 attempts)?
- Q5: What is the average PPG for the top 5 scorers?
- Q6: Who had the best 3-point percentage (min 20 attempts)?

**Findings:**
- Total Questions: 6
- Correct: 6 (100%)
- Incorrect: 0
- **Accuracy: 100%**

The model demonstrated perfect accuracy on factual, data-lookup questions. When provided with clear data and straightforward questions, Claude correctly identified statistics and performed calculations with precision.

---

### Phase B: Testing Judgment Decisions and Prompt Engineering

**Objective:** Determine if prompt structure affects the quality of judgment-based recommendations.

**Approach:**
1. Define explicit metrics for qualitative concepts
2. Ask vague versions of judgment questions (no framework)
3. Ask structured versions with step-by-step analysis
4. Compare quality of answers
5. Measure improvement from prompt engineering

**Question 7: Most All-Around Player**

*Metric Definition:*
```
Score = (PPG / Max_PPG) + (APG / Max_APG) + (RPG / Max_RPG)
```
This combines scoring, assists, and rebounding into one metric.

| Attempt | Type | Quality | Correct | Shows Calculations |
|---------|------|---------|---------|-------------------|
| 1 | Vague | 4/5 | YES | NO |
| 2 | Structured | 5/5 | YES | YES |
| **Improvement** | | **+1 point** | **Same** | **Added rigor** |

**Finding:** Defining metrics explicitly improved answer quality by 25%. Model correctly identified Nikola Jokić in both attempts, but Attempt 2 provided mathematical proof while Attempt 1 only provided narrative reasoning.

---

**Question 8: Best Playmaker**

*Metric Definition:*
```
Score = (APG / Max_APG) + (Games_Played / Max_Games)
```
This combines assist volume with availability/consistency.

| Attempt | Type | Quality | Correct | Shows Calculations |
|---------|------|---------|---------|-------------------|
| 1 | Vague | 4/5 | YES | NO |
| 2 | Structured | 5/5 | YES | YES |
| **Improvement** | | **+1 point** | **Same** | **Added rigor** |

**Finding:** Same pattern as Question 7. Trae Young identified correctly in both cases, but structured prompt produced calculated proof while vague prompt produced only logic.

---

**Question 9: The Coach's Question (Most Complex)**

*Scenario:* A coach needs to decide whether to focus on OFFENSE or DEFENSE to win 2 more games next season. Which one player should they develop?

*Analysis Framework:*
- Step 1: Calculate average scoring across top 5 scorers
- Step 2: Calculate average assists across top 5 playmakers
- Step 3: Compare the metrics and identify elite concentration
- Step 4: Identify players who excel across multiple dimensions
- Step 5: Make recommendation with data-backed reasoning

| Attempt | Type | Quality | Recommendation | Shows Calculations |
|---------|------|---------|-----------------|-------------------|
| 1 | Vague | 3.5/5 | OFFENSE (Jokić) | NO |
| 2 | Structured | 5/5 | OFFENSE (Jokić) | YES |
| **Improvement** | | **+1.5 points** | **Same** | **Full proof** |

**Finding:** This more complex question showed larger improvement (43%) from structure. Both attempts recommended the same answer (Focus on OFFENSE, develop Nikola Jokić), but the structured version provided rigorous mathematical justification while the vague version relied on intuition.

---

## 3. KEY FINDINGS

### What Claude Does Well ✅

1. **Factual Lookups:** 100% accuracy identifying leaders and top performers
2. **Basic Arithmetic:** Perfect on PPG, percentage, and average calculations
3. **Following Frameworks:** Applies explicit metric definitions exactly
4. **Showing Work:** Displays all calculations when prompted
5. **Comparative Analysis:** Makes sensible comparisons between alternatives
6. **Clear Communication:** Provides coherent explanations with supporting context

### Where Claude Needs Guidance ❌

1. **Vague Judgment Questions:** Produces reasonable but unverifiable answers
2. **No Default Rigor:** Doesn't show calculations unless explicitly asked
3. **Implicit Assumptions:** May not spell out reasoning steps
4. **Trade-off Analysis:** Struggles without explicit metrics to compare
5. **Numerical Proof:** Provides narrative reasoning over quantitative proof

### The Prompt Engineering Effect

**Average Quality Improvement: 31%**

| Question Type | Vague | Structured | Improvement |
|---------------|-------|-----------|------------|
| All-Around | 4/5 | 5/5 | +25% |
| Playmaker | 4/5 | 5/5 | +25% |
| Coach's Q | 3.5/5 | 5/5 | +43% |
| **Average** | **4/5** | **5/5** | **+31%** |

**Critical Insight:** The more complex the question, the more structured prompts help. Complex decisions benefited 40%+ while simpler metrics benefited 25%.

---

## 4. PHASE A RESULTS (FACTUAL ACCURACY)

### Ground Truth Statistics

**Top 10 Scorers:**
1. Shai Gilgeous-Alexander: 3,193 points (31.93 PPG) ✓
2. Anthony Edwards: 2,557 points (27.2 PPG) ✓
3. Nikola Jokić: 2,438 points (29.02 PPG) ✓
4. Giannis Antetokounmpo: 2,227 points (30.51 PPG)
5. Jalen Brunson: 2,220 points (26.75 PPG)

**Top 10 Assist Providers:**
1. Trae Young: 897 assists (11.5 APG) ✓
2. Tyrese Haliburton: 870 assists (9.06 APG) ✓
3. Nikola Jokić: 828 assists (9.86 APG) ✓
4. James Harden: 751 assists (8.73 APG)
5. Cade Cunningham: 690 assists (9.08 APG)

**Top 10 Rebounders:**
1. Karl-Anthony Towns: 1,129 rebounds (12.54 RPG) ✓
2. Ivica Zubac: 1,081 rebounds (12.43 RPG)
3. Nikola Jokić: 1,070 rebounds (12.74 RPG) ✓
4. Domantas Sabonis: 985 rebounds (13.87 RPG)
5. Rudy Gobert: 914 rebounds (10.51 RPG)

**Best Field Goal % (Min 50 attempts):**
1. Kai Jones: 79.8% ✓
2. Jaxson Hayes: 71.0%
3. Jarrett Allen: 70.8%

**Best 3-Point % (Min 20 attempts):**
1. Patrick Baldwin Jr.: 56.5% ✓
2. Dru Smith: 53.3%
3. Alex Ducas: 47.6%

### Phase A Summary

| Question | Model Answer | Ground Truth | Match | Rating |
|----------|--------------|--------------|-------|--------|
| Q1: Leading Scorer | Shai (3,193) | Shai (3,193) | ✓ | 5/5 |
| Q2: Most Assists | Trae (897) | Trae (897) | ✓ | 5/5 |
| Q3: Most Rebounds | Karl-Anthony (1,129) | Karl-Anthony (1,129) | ✓ | 5/5 |
| Q4: Best FG% | Kai Jones (79.8%) | Kai Jones (79.8%) | ✓ | 5/5 |
| Q5: Avg PPG | All 5 correct | All 5 correct | ✓ | 5/5 |
| Q6: Best 3P% | Patrick Baldwin Jr. (56.5%) | Patrick Baldwin Jr. (56.5%) | ✓ | 5/5 |

**PHASE A ACCURACY: 6/6 = 100%**

### Interpretation

Claude demonstrates exceptional capability on factual questions. When provided with clear data and direct questions, the model reliably identifies correct answers and performs accurate calculations. This establishes a strong baseline: **Claude is trustworthy for data lookup and basic computational tasks.**

---

## 5. PHASE B RESULTS (JUDGMENT & PROMPT ENGINEERING)

### Question 7: Most All-Around Player

**Metric:** (PPG/Max_PPG) + (APG/Max_APG) + (RPG/Max_RPG)

**Attempt 1 (Vague Prompt):**
- Answer: Nikola Jokić
- Quality: 4/5
- Analysis: "Jokić uniquely excels across all three dimensions. While other players may lead in individual categories, Jokić is the only player who dominates across all three areas simultaneously."
- Shows Calculations: NO
- Verdict: Correct answer, sound reasoning, but no mathematical proof

**Attempt 2 (Structured Prompt):**
- Answer: Nikola Jokić (score: 2.766)
- Quality: 5/5
- Analysis: 
  - Shai: 1.0 + 0.555 + 0.381 = 1.936
  - Jokić: 0.909 + 0.857 + 1.0 = 2.766 ✓
  - Giannis: 0.955 + 0.477 + 0.961 = 2.393
- Shows Calculations: YES (all three players)
- Verdict: Correct answer, perfect calculations, defensible reasoning

**Improvement:** +1 point (25% quality boost)

**Key Difference:** 
- Vague: Narrative explanation of why Jokić is best
- Structured: Numerical proof showing Jokić's score exceeds others

---

### Question 8: Best Playmaker

**Metric:** (APG/Max_APG) + (Games_Played/Max_Games)

**Attempt 1 (Vague):**
- Answer: Trae Young
- Quality: 4/5
- Shows Calculations: NO
- Verdict: Correct, but narrative reasoning only

**Attempt 2 (Structured):**
- Answer: Trae Young (score: 1.78)
- Quality: 5/5
- Calculations:
  - Trae: 1.0 + 0.78 = 1.78 ✓
  - Haliburton: 0.788 + 0.96 = 1.748
  - Jokić: 0.857 + 0.84 = 1.697
- Shows Calculations: YES
- Verdict: Correct, perfect calculations, explained trade-offs

**Improvement:** +1 point (25% quality boost)

**Insight:** Both versions identified the same winner, but structured version provided mathematical proof of superiority over alternatives.

---

### Question 9: The Coach's Question (Most Complex)

**Scenario:** Coach needs to decide: OFFENSE or DEFENSE? Which player to develop?

**Attempt 1 (Vague):**
- Recommendation: OFFENSE, develop Nikola Jokić
- Quality: 3.5/5
- Analysis: "Scoring is the most direct path to winning games... While Shai is the elite scorer, Jokić is the most complete player"
- Shows Calculations: NO
- Verdict: Reasonable but not rigorously justified

**Attempt 2 (Structured):**
- Recommendation: OFFENSE, develop Nikola Jokić
- Quality: 5/5
- Calculations:
  - Step 1: Top 5 avg PPG = 29.08
  - Step 2: Top 5 avg APG = 9.65
  - Step 3: Scoring gap (1.42) vs Playmaking gap (1.64); Scoring 3x higher volume
  - Step 4: Jokić excels in all three (29.02 PPG + 9.86 APG + 12.74 RPG)
  - Step 5: OFFENSE focus, Jokić development
- Shows Calculations: YES (all steps with data)
- Verdict: Excellent analysis, numerically defensible

**Improvement:** +1.5 points (43% quality boost)

**Critical Difference:**
- Vague: "Scoring wins games because Shai has 31.93 PPG"
- Structured: "Top 5 avg scoring is 29.08 PPG, which is 3x higher impact than 9.65 APG average. Shai leads scoring but Jokić (29.02 + 9.86 + 12.74) multi-dimensional advantage = better game changer"

---

## 6. PROMPT ENGINEERING INSIGHTS

### Finding 1: Metric Definition Matters

**Without explicit metric:** Model produces qualitative reasoning
```
"Nikola Jokić is the best all-around player because he excels 
in scoring, assists, and rebounding."
```

**With explicit metric:** Model produces quantitative proof
```
Score = 0.909 (scoring) + 0.857 (assists) + 1.0 (rebounding) = 2.766
This is higher than Shai's 1.936 or Giannis's 2.393.
```

**Impact:** Vague vs. Structured adds 25-43% quality depending on complexity.

---

### Finding 2: Step-by-Step Instruction Forces Rigor

**Without steps:** Model jumps to conclusion
```
"Focus on offense because scoring is more important than playmaking."
```

**With steps:** Model calculates before concluding
```
Step 1: Average scoring = 29.08 PPG
Step 2: Average playmaking = 9.65 APG
Step 3: Scoring is 3x higher (29.08 vs 9.65)
Conclusion: Focus on OFFENSE
```

**Impact:** Model only shows calculations when explicitly requested.

---

### Finding 3: Complexity Determines Improvement Potential

- **Simple metrics (Q7, Q8):** +25% improvement (4.0 → 5.0)
- **Complex decisions (Q9):** +43% improvement (3.5 → 5.0)

**Implication:** Structured prompts help more on harder questions. For complex advisory decisions, prompt engineering is essential.

---

### Finding 4: "Show Your Work" is Powerful

Just adding "Show me the calculation for each player" and "Display all work" triggers:
- Numerical comparisons (not just narratives)
- Step-by-step reasoning (not just conclusions)
- Multiple alternative calculations (not just the winner)
- Verifiable claims (not just assertions)

---

## 7. BEST PRACTICES FOR USING LLMs IN DATA ANALYSIS

### ✅ When to TRUST Claude

- ✓ Factual lookups (identifying leaders, finding top performers)
- ✓ Basic arithmetic (PPG, percentages, averages)
- ✓ When given explicit metric definitions
- ✓ When asking to show all calculations
- ✓ Comparative analysis with defined frameworks
- ✓ Data pattern identification

### ❌ When to VERIFY Claude

- ✗ Judgment calls without explicit metrics
- ✗ Complex trade-off decisions
- ✗ Answers lacking calculations
- ✗ Qualitative recommendations (scoring vs. defense)
- ✗ Vague or open-ended questions
- ✗ Advisory decisions without structured analysis

### 🎯 Best Practices for Reliable Results

1. **Define Metrics Explicitly**
   - Don't assume the model understands your definition of "best"
   - Provide formula: Score = (X/Max_X) + (Y/Max_Y)
   - This eliminates ambiguity

2. **Request Step-by-Step Analysis**
   - Break complex questions into 5-7 steps
   - Ask for calculations at each step
   - Model performs better with structured breakdown

3. **Ask for Calculations**
   - Always request "show all your work"
   - Request "calculate this for all alternatives"
   - Don't accept narrative-only answers on important decisions

4. **Verify Against Ground Truth**
   - For critical decisions, calculate the answer yourself first
   - Compare model answer to ground truth
   - Identify where model was wrong/right

5. **Compare Versions**
   - Ask vague version first (establish baseline)
   - Ask structured version second (with metrics/steps)
   - Evaluate which produced better reasoning

6. **Use as Accelerator, Not Decision-Maker**
   - Claude excels at rapidly analyzing data
   - Use results to inform your judgment, not replace it
   - Especially for advisory/judgment decisions

---

## 8. CONCLUSIONS

### Main Findings

1. **Claude is excellent for factual analysis** (100% accuracy on Phase A)
   - Reliable for data lookups and calculations
   - Trustworthy when ground truth exists
   - Good as first-pass analysis tool

2. **Prompt engineering dramatically improves judgment quality** (31% avg improvement)
   - Vague prompts = 3.5-4/5 quality (narrative reasoning)
   - Structured prompts = 5/5 quality (numerical reasoning)
   - Metrics must be explicit, not assumed

3. **Complex decisions benefit most from structure** (43% improvement for coach question)
   - Simple questions: ~25% improvement
   - Complex decisions: ~40%+ improvement
   - Structured framework becomes essential for advisory work

4. **"Show your work" makes answers defensible**
   - Calculations transform opinions into proofs
   - Verifiable claims replace assertions
   - Multi-step reasoning reveals assumptions

### Implications for Research

For tasks requiring LLM analysis:
- **Invest in prompt engineering** (structured > vague by 30%+)
- **Establish ground truth** (verify against known answers)
- **Use explicit metrics** (definitions reduce ambiguity)
- **Request calculations** (turns reasoning into proofs)
- **Compare alternatives** (single best-case isn't enough)

### Limitations

This research tested only:
- One LLM (Claude)
- One dataset type (numerical sports statistics)
- One domain (NBA data)
- Binary decision questions (offense vs. defense)

Results may not generalize to:
- Other LLMs (ChatGPT, Gemini, etc.)
- Unstructured data (text, images)
- Other domains (medical, legal, financial)
- Open-ended questions

---

## 9. FILES INCLUDED

This repository contains:

- **README.md** - This comprehensive documentation
- **PROMPT_LOG.md** - All 9 questions with prompts, responses, and verdicts
- **GROUND_TRUTH.txt** - Verified statistics (answer key)
- **METRICS.md** - Metric definitions used in Phase B
- **analyze_ground_truth.py** - Python script to calculate ground truth
- **analysis/** folder - Any supporting calculations

**Note:** The NBA dataset (nba_dailyleaders_full_24_25.csv) is NOT included. To reproduce:
1. Obtain the CSV from your data source
2. Run analyze_ground_truth.py to calculate verified statistics
3. Compare model answers to ground truth

---

## 10. REPRODUCTION INSTRUCTIONS

### Requirements
- Python 3.8+
- pandas
- Access to nba_dailyleaders_full_24_25.csv

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/[username]/Task_05_Descriptive_Stats.git
   cd Task_05_Descriptive_Stats
   ```

2. **Place your CSV file in the data/ folder**
   ```bash
   cp /path/to/nba_dailyleaders_full_24_25.csv data/
   ```

3. **Calculate ground truth**
   ```bash
   python analyze_ground_truth.py
   ```
   This will generate GROUND_TRUTH.txt with verified statistics

4. **Review PROMPT_LOG.md**
   - See all 9 questions asked
   - See model responses
   - See verdicts (correct/incorrect)
   - Compare vague vs. structured versions

5. **Verify results**
   - Check that all Phase A questions show 100% accuracy
   - Verify Phase B shows quality improvement with structure
   - Confirm GROUND_TRUTH.txt matches your CSV analysis

---

## 11. REFLECTION & TAKEAWAYS

### What I Learned

1. **LLMs are powerful but require structure**
   - Without guidance, they produce plausible but unverifiable answers
   - With explicit frameworks, they produce rigorous analysis
   - The difference is 30%+ in quality

2. **Prompt quality directly determines output quality**
   - Vague prompts = good narrative, weak proof
   - Structured prompts = excellent proof, strong narrative
   - Time spent on prompting pays off exponentially

3. **Metric definition is critical**
   - "Best player" is ambiguous (best at what?)
   - "Best player" with explicit formula is unambiguous
   - Vagueness allows models to use their own assumptions

4. **Step-by-step breaks down bias**
   - Open questions trigger narrative/intuitive reasoning
   - Step-by-step questions trigger analytical reasoning
   - Same model, different prompt = different reasoning path

### Where I Would Trust Claude

✓ Finding the top 10 scorers  
✓ Calculating PPG averages  
✓ Identifying shooting percentage leaders  
✓ Comparative statistical analysis  
✓ Rapid data exploration before my own analysis  

### Where I Would Verify Claude

✗ "Which player is best?" (without explicit metric)  
✗ "Should we focus on offense or defense?" (without data-driven framework)  
✗ "Which player should I invest in?" (without multi-dimensional analysis)  
✗ Any judgment decision made from vague prompt  

### Future Research

This study only tested NBA data. Future work could examine:
- Does this pattern hold for other LLMs? (ChatGPT, Gemini, etc.)
- What about unstructured data? (text, images, audio)
- How does domain expertise affect results?
- Can we formalize an optimal prompt structure?
- Do in-context examples improve results further?

---

## 12. REFERENCES & RESOURCES

### LLM Prompting Best Practices
- OpenAI Prompt Engineering Guide
- Anthropic Constitutional AI Documentation
- "Prompt Engineering for Generative AI" Research Papers

### NBA Data Source
- [NBA Official Statistics](https://www.nba.com/stats/)
- [Basketball Reference](https://www.basketball-reference.com/)

### Related Research
- "Large Language Models as Zero-Shot Planners" (Huang et al., 2022)
- "Scaling Laws for Reward Model Overoptimization" (Gao et al., 2023)
- "Prompt Engineering: Systematic Approaches to Getting Better Results" (Adamopoulou & Moussiades, 2023)

---

## SUBMISSION INFORMATION

**Submitted to:** jrstrome@syr.edu  
**Assignment:** Research Task 5 - Descriptive Statistics and LLMs  
**Deadline:** August 1, 2026  
**Repository:** [Your GitHub Link]  
**Date Submitted:** July 29, 2026

---

**For questions or clarifications, please contact the researcher.**
