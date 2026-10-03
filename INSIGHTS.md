# Insights Summary — Titanic EDA

Dataset: Titanic passengers (891 rows, 12 columns). Target: `Survived`.

1. **Overall survival was 38.4%** (342 of 891 passengers); most passengers did not survive.
2. **Sex was the strongest factor:** 74% of women survived versus 19% of men (chi-square p ≈ 1e-58, Cramér's V ≈ 0.54).
3. **Social class mattered:** survival fell from 63% (1st class) to 47% (2nd) to 24% (3rd). Combined with sex, 97% of first-class women survived but only 14% of third-class men.
4. **Children had an advantage, but age overall did not:** 58% of children (0–12) survived, yet the overall age difference between survivors and non-survivors is *not* statistically significant (p ≈ 0.16).
5. **Family size has a "sweet spot":** passengers with 2–4 family members survived at 58%, those travelling alone at 30%, and large families (5+) at only 16%.
6. **Fare and cabin mostly reflect class:** survivors' median fare was £26 vs £10.50, and passengers with a recorded cabin survived 67% vs 30%. But a cabin was recorded for 81% of first-class and 2% of third-class passengers. Fare is heavily right-skewed (skew ≈ 4.8), so `log(1 + Fare)` is better for modelling.
7. **Port of embarkation is partly confounded with class:** Cherbourg's 55% survival rate is linked to its high share of first-class passengers (51%), although a gap remains within third class (Cherbourg 38% vs Southampton 19%).
8. **Data quality:** `Cabin` was 77% missing and `Age` 20% missing. They were handled with feature extraction (`HasCabin`, `Deck`) and group-based median imputation (by Title and Pclass). No duplicate rows were found.

**Limitations:** relationships are associations, not proof of cause; imputed ages are estimates; the data is a sample of passengers.

**Next step:** build a classification model (logistic regression / random forest) using `IsFemale`, `Pclass`, `Title`, `FamilyGroup`, `FareLog` and `AgeGroup`.
