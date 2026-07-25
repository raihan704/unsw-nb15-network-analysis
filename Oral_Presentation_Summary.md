# Oral Presentation Summary — 5 minutes

**Project:** Hypothesis Testing Analysis of Network Traffic Attacks Using the UNSW-NB15 Dataset
**Student:** MEKCI RAIHAN — Group B1 — Probability and Statistics — 2025/2026

---

## Slide 1 — Title (15 s)
"Good morning. My project applies the hypothesis testing methods from Chapter 3 of the course
to a real cybersecurity dataset, the UNSW-NB15 testing set. The goal is to use simple statistical
tests to compare normal traffic and attack traffic."

## Slide 2 — The dataset (40 s)
- 82,332 network connections, 45 features, no missing values.
- Two classes: Normal (44.94%) and Attack (55.06%).
- 9 attack categories, dominated by Generic and Exploits.
- Main variables I used: `dur` (duration), `rate` (packet rate), `proto` (protocol), `attack_cat`.

## Slide 3 — Method (40 s)
For every test I followed the course structure:
1. State H0 and H1.
2. Compute the test statistic.
3. Read the critical value from the table at α = 0.05.
4. Build the acceptance region A.
5. Accept H0 if the statistic is in A, reject otherwise.
6. Interpret the result.

I used four tests: **Student t-test** (and its **normal approximation** for large samples),
**Fisher F-test** for variances, **chi-squared goodness-of-fit**, and **chi-squared homogeneity**.

## Slide 4 — Tests on means (1 min 15 s)
- **Test 1:** Mean duration Normal vs Attack on the full data (n = 37,000 vs 45,332).
  Z = 0.34, critical value ±1.96. Z is in A → **accept H0**.
  The mean duration alone does not separate normal from attack: both have heavy outliers.

- **Test 2:** Mean rate Normal vs Attack. Z = −104.38 → **reject H0**.
  Attack traffic has a much higher mean rate (≈ 126,500) than normal traffic (≈ 28,350).

- **Test 3 (F-test):** Variance of duration, Generic vs Exploits. F = 42.39, outside [0.967; 1.034] → **reject H0**.
  The variances are very different, so the equal-variance assumption fails. I used the
  normal approximation with separate variances for the next test.

- **Test 4:** Mean duration Generic vs Exploits. Z = −29.49 → **reject H0**.
  Exploits last on average about 1.72 s, Generic only 0.06 s.

I also repeated tests 1, 2 and 4 on a random sample of n = 200 per group using the Student t(398)
distribution. The conclusions were identical.

## Slide 5 — Tests on proportions (1 min)
- **Test 5 (goodness-of-fit):** Are attack categories uniformly distributed?
  D = 63,201.04, critical = 15.51 → **reject H0**. Categories are very unbalanced.

- **Test 6 (homogeneity):** Protocol distribution, Normal vs Attack.
  D = 15,247.19, critical = 7.81 → **reject H0**. Normal traffic is mostly tcp,
  attacks use udp and unas much more.

- **Test 7 (homogeneity):** Protocol distribution, Generic vs Exploits.
  D = 26,655.58, critical = 7.81 → **reject H0**. Generic is almost only udp,
  Exploits is mostly tcp.

## Slide 6 — Conclusion (40 s)
- **Packet rate** is a strong discriminator between normal and attack traffic.
- **Duration** does not separate normal from attack but separates attack types.
- **Attack categories** are highly unbalanced.
- **Protocol** is a strong signature of both attack vs normal and of the attack type.

These results extend my previous descriptive analysis with formal statistical evidence
and give a solid basis for a future intrusion-detection system.

"Thank you. I am happy to answer your questions."

---

## Likely teacher questions

**Q. Why do you use the normal distribution instead of Student?**
Because for very large samples (n > 30) the Student distribution t(n+p−2) is very close to N(0,1)
by the Central Limit Theorem. The course mentions this explicitly.

**Q. The F-test for Test 3 rejected H0 — why did you still compare the means in Test 4?**
With equal variances rejected, the standard t-test does not apply. But because n and p are both
very large, the normal approximation with separate variances (Welch-type) is still valid.

**Q. What is the difference between goodness-of-fit and homogeneity?**
Goodness-of-fit tests one sample against a fixed theoretical distribution (Test 5 against uniform).
Homogeneity tests whether two or more samples share the same distribution (Tests 6 and 7).

**Q. Why α = 0.05?**
Standard significance level in the course. It means we accept a 5% probability of rejecting H0
when it is true (type I error).

**Q. Are your chi-squared tests valid?**
Yes. All expected counts d_i are well above 5 (the usual threshold). Test 5 had d_i ≈ 5,037
per category, Test 6 and 7 all expected counts above 35.
