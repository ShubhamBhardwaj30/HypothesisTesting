# Hypothesis Testing — Theory

## General steps (short)
1. State hypotheses:
   - Null: $H_0$ (no effect / no difference)
   - Alternative: $H_a$ (effect / difference)
2. Choose significance level $\alpha$ (e.g. $0.05$).
3. Select appropriate test based on data type and assumptions.
4. Compute test statistic (Z, t, F, $\chi^2$, etc.).
5. Decision: reject $H_0$ if (p-value < $\alpha$) **or** statistic beyond critical value.

---

# 1. Z tests (large-sample / proportions / known sigma)

### One-sample mean Z-test
Use when population SD ($\sigma$) is known.
- Test statistic:
  - $$Z = \frac{\bar{X} - \mu_0}{\sigma / \sqrt{n}}$$
- Decision: compare $|Z|$ to $Z_{\text{crit}}$ (e.g. $1.96$ for two-tailed $\alpha=0.05$)
- Or use p-value: $$p = 2 \times (1 - \Phi(|Z|))$$

### One-sample proportion Z-test
- $$\hat{p} = \frac{\text{successes}}{n}$$
- Standard error under $H_0$: $$SE = \sqrt{\frac{p_0 (1-p_0)}{n}}$$
- Test statistic:
  - $$Z = \frac{\hat{p} - p_0}{SE}$$

### Two-sample proportion Z-test (independent groups)
- $$\hat{p} = \frac{x_1 + x_2}{n_1 + n_2} \quad \text{(pooled proportion under } H_0)$$
- $$SE = \sqrt{\hat{p} (1 - \hat{p}) \left(\frac{1}{n_1} + \frac{1}{n_2}\right)}$$
- $$Z = \frac{\hat{p}_1 - \hat{p}_2}{SE}$$

---

# 2. t tests (unknown sigma, small samples)

### One-sample t-test
- Test statistic:
  - $$t = \frac{\bar{X} - \mu_0}{s / \sqrt{n}}$$
- Where the sample standard deviation $s$ is defined as
  - $$s = \sqrt{\frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X})^2}$$
- Degrees of freedom:
  - $$df = n - 1$$

### Paired t-test (dependent samples)
- Compute differences $d_i = \text{before}_i - \text{after}_i$
- $$\bar{d} = \text{mean}(d_i), \quad s_d = \text{sd}(d_i)$$
- $$t = \frac{\bar{d}}{s_d / \sqrt{n}}$$
- $$df = n - 1$$

### Two-sample independent t-test (pooled variance, equal variances assumed)
- $$s_p^2 = \frac{(n_1 - 1) s_1^2 + (n_2 - 1) s_2^2}{n_1 + n_2 - 2}$$
- $$t = \frac{\bar{X}_1 - \bar{X}_2}{s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}}$$
- $$df = n_1 + n_2 - 2$$

### Welch’s t-test (unequal variances, recommended)
- $$t = \frac{\bar{X}_1 - \bar{X}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}$$
- Approximate degrees of freedom (Welch–Satterthwaite):
$$
df = \frac{\left(\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}\right)^2}{\frac{\left(\frac{s_1^2}{n_1}\right)^2}{n_1 - 1} + \frac{\left(\frac{s_2^2}{n_2}\right)^2}{n_2 - 1}}
$$

- Use $t$ with that $df$.

---

# 3. Chi-square tests (categorical data)

### Goodness-of-fit
- $$\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$$
- $$df = k - 1 \quad (k = \text{number of categories})$$

### Test of independence (contingency table $r \times c$)
- $$E_{ij} = \frac{\text{row}_i^{\text{total}} \times \text{col}_j^{\text{total}}}{\text{grand total}}$$
- $$\chi^2 = \sum_{\text{cells}} \frac{(O_{ij} - E_{ij})^2}{E_{ij}}$$
- $$df = (r - 1)(c - 1)$$

### Decision
- Compare $\chi^2$ to $\chi^2_{\text{crit}}(df, \alpha)$ or compute $$p = 1 - \text{CDF}_{\chi^2}(\chi^2, df)$$.

### McNemar’s test (paired binary before/after)
- Only discordant pairs $b$ and $c$ matter:
- $b$ = before = Yes, after = No
- $c$ = before = No,  after = Yes
- Test statistic (large-sample approx):
- $$\chi^2 = \frac{(b - c)^2}{b + c} \quad (df = 1)$$
- For small $b+c$, use exact binomial version.

---

# 4. ANOVA (analysis of variance)

### One-way ANOVA (k groups)
- Let $k$ = number of groups, $n_i$ = size of group $i$, $N$ = total observations.
- Group means: $\bar{X}_i$, grand mean: $\bar{X}_{\text{grand}}$.

**Between-group sum of squares (SSB):**
- $$SSB = \sum_i (n_i (\bar{X}_i - \bar{X}_{\text{grand}})^2)$$
- $$df_B = k - 1$$

**Within-group sum of squares (SSW):**
- $$SSW = \sum_i \sum_j (X_{ij} - \bar{X}_i)^2$$
- $$df_W = N - k$$

**Mean squares and F:**
- $$MSB = \frac{SSB}{df_B}$$
- $$MSW = \frac{SSW}{df_W}$$
- $$F = \frac{MSB}{MSW} \quad \text{(compare to } F_{\text{crit}}(df_B, df_W))$$

**Decision**: reject $H_0$ (all means equal) if $F$ large (or p-value < alpha).

### Two-way ANOVA (factors A and B)
- Partition total SS into: $SS_A$, $SS_B$, $SS_{AB}$ (interaction), $SS_{\text{Error}}$.
- Compute $MS$ for each and compare:
- $$F_A = \frac{MS_A}{MS_{\text{Error}}}$$
- $$F_B = \frac{MS_B}{MS_{\text{Error}}}$$
- $$F_{AB} = \frac{MS_{AB}}{MS_{\text{Error}}}$$
- df: $df_A = a - 1$, $df_B = b - 1$, $df_{AB} = (a - 1)(b - 1)$, $df_{\text{Error}} = N - ab$.

---

# 5. p-value interpretation (brief)
- $p$-value = probability of seeing data as (or more) extreme than observed **if $H_0$ is true**.
- If $p < \alpha$ → reject $H_0$.
- If $p \geq \alpha$ → fail to reject $H_0$.
- **Do not** interpret $p$ as $P(H_0 \text{ is true})$.

---

# Quick reference: which test to use
- Continuous outcome:
- 1 sample mean: one-sample t (or Z if $\sigma$ known & large $n$)
- 2 independent means: two-sample t (Welch recommended)
- Paired means: paired t-test
- 3+ groups: one-way ANOVA (or Kruskal–Wallis if nonparametric)
- Binary / proportions:
- 1 sample proportion: one-sample proportion Z-test (or exact binomial)
- 2 independent proportions: two-sample proportion Z-test
- Paired binary (before/after): McNemar’s test
- Categorical association: chi-square test of independence

---

# Notes & practical tips
- When population SD is unknown, use $s / \sqrt{n}$ as the estimated standard error and t-distribution.
- Use Welch’s t-test if variances likely unequal.
- For small counts in proportion/chi-square tests, prefer exact tests (binomial, Fisher's exact).
- Always report test statistic, df (if applicable), and p-value. Also report effect size (difference in means, risk difference, odds ratio) and confidence intervals when possible.

---