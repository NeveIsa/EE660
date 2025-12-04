# EE660 Midterm Exam - October 8, 2024
## Detailed Topic Breakdown

---

## Q1: True/False Questions (10 points)

### (a) Sub-Gaussian Maximal Inequality
- Topic: Sub-Gaussian random variables
- Concept: Independence requirement for E max_{i∈[n]} X_i ≤ σ√(2 log n)
- **Answer: False** - Independence is required

### (b) Perceptron vs SVM
- Topic: Linear classifiers
- Concept: Whether Perceptron and SVM solutions coincide on linearly separable data
- **Answer: False** - Different objectives lead to different solutions

### (c) Feature Maps and Linear Separability
- Topic: Feature transformations
- Concept: Existence of finite-dimensional feature map Φ(x) for arbitrary datasets
- **Answer: True** - Can always find such a map (e.g., one-hot encoding)

### (d) Kernel Properties
- Topic: Valid kernels
- Concept: Whether k(x, x) < 0 is possible
- **Answer: False** - Kernels must satisfy k(x, x) ≥ 0 (PSD property)

### (e) Shift-Invariant Kernels
- Topic: Kernel properties
- Concept: Whether k(x, y) = ⟨x, y⟩² is shift-invariant
- **Answer: False** - Not shift-invariant (k(x, y) ≠ k(x-y))

### (f) Loss Function Properties
- Topic: Surrogate losses
- Concept: Relationship 1{y ≠ ŷ} ≤ 1{yŷ ≤ ε}
- **Answer: True** - Valid for ε ≥ -1

### (g) VC Dimension Monotonicity
- Topic: VC dimension
- Concept: Monotonicity property H ⊆ H' ⟹ VCdim(H) ≤ VCdim(H')
- **Answer: True** - VC dimension is monotonic

### (h) VC Dimension and Rademacher Complexity
- Topic: Complexity measures
- Concept: If VCdim(H) = ∞, must R_n(H) = ∞?
- **Answer: False** - Infinite VC dimension doesn't imply infinite Rademacher complexity

### (i) Finite Hypothesis Classes
- Topic: PAC learnability
- Concept: Whether finite |H| < ∞ implies agnostic PAC learnability
- **Answer: True** - Finite classes are always PAC learnable

### (j) Finite Parameters and Rademacher Complexity
- Topic: Function class complexity
- Concept: Does finite number of parameters imply R_n(F) < ∞?
- **Answer: False** - Finite parameters don't guarantee bounded Rademacher complexity

---

## Q2: Random Features (20 points)

### Part (a) - 5 points
**Topic: Unbiased Estimator**
- Kernel approximation k(x, y) = E_{ω∼p(·)}[φ(x, ω)φ(y, ω)]
- Random feature map Φ(x) := 1/√m (φ(x, ω₁), ..., φ(x, ω_m))
- **Prove:** E[⟨Φ(x), Φ(y)⟩] = k(x, y)
- Concepts: Expectation, Monte Carlo approximation

### Part (b) - 15 points
**Topic: Concentration Inequality**
- Finite subset D ⊂ X with |D| < ∞
- **Prove:** With probability ≥ 1 - δ:
  - max_{x,y∈D} |k(x, y) - ⟨Φ(x), Φ(y)⟩| ≤ √(2 log(2|D|²/δ)/m)
- **Tools used:**
  - Hoeffding's inequality (two-sided)
  - Union bound over all pairs (x, y) ∈ D
- Concepts: Concentration, finite sample bounds

---

## Q3: VC Dimension (25 points)

### Part (a) - 10 points
**Topic: Lower Bound on VC Dimension**
- Hypothesis class: H = {x ↦ h_{w,b}(x) := sgn(⟨x, w⟩ + b) | w ∈ ℝ^d, b ∈ ℝ}
- **Prove:** VCdim(H) ≥ d + 1
- **Approach:** Construct d+1 points that can be shattered
  - Use standard basis vectors e_i and origin
  - Show all 2^(d+1) labelings achievable

### Part (b) - 10 points
**Topic: Upper Bound on VC Dimension**
- Same hypothesis class H
- **Prove:** VCdim(H) ≤ d + 1
- **Key idea:** Use relationship with H' = {x ↦ sgn(⟨x̄, w̄⟩) | w̄ ∈ ℝ^(d+1)}
- **Given fact:** VCdim(H') = d + 1
- Embed d-dimensional problem into (d+1)-dimensional space

### Part (c) - 5 points
**Topic: VC Dimension of Interval Functions**
- Hypothesis class: {x ↦ sgn(1{x ∈ [a, a+1]} - 1/2) | a ∈ ℝ}
- **Prove:** VCdim = 2
- Concepts: Shattering, interval functions

---

## Q4: CDF Estimation - Glivenko-Cantelli Theorem (25 points)

### Setup
- Distribution μ over ℝ with CDF F(t) := P_{x∼μ}{x ≤ t}
- Empirical estimate: F̂_n(t) := 1/n ∑ᵢ₌₁ⁿ 1{xᵢ ≤ t}
- **Goal:** Prove E sup_{t∈ℝ} |F(t) - F̂_n(t)| ≤ c₀√(log(c₁n)/n)

### Part (a) - 5 points
**Topic: Rademacher Complexity Relationship**
- Let H := {x ↦ sgn(t - x) | t ∈ ℝ}
- **Prove:** R_n({x ↦ 1{x ≤ t} | t ∈ ℝ}) = 1/2 R_n(H)
- **Hint:** Use identity 1{x ≤ t} = (sgn(t-x) + 1)/2

### Part (b) - 5 points
**Topic: Rademacher Complexity Bound**
- **Prove:** R_n(H) ≤ √(2 log(en)/n)
- Acceptable: Any bound of form c₀√(log(c₁n)/n)
- Concepts: VC dimension bounds on Rademacher complexity

### Part (c) - 15 points
**Topic: Final CDF Bound**
- Use alternative Rademacher definition: R̄_n(F)
- **Given inequality:** E sup_{f∈F} |1/n ∑(E[f(xᵢ)] - f(xᵢ))| ≤ 2R̄_n(F)
- **Given fact:** If |f| ≤ 1 for all f ∈ F, then R̄_n(F) ≤ 2R_n(F) + 1/√n
- **Prove:** E sup_{t∈ℝ} |F(t) - F̂_n(t)| ≤ 4√(2 log(en)/n)
- Combines all previous parts into final concentration result

---

## Key Mathematical Tools Used

1. **Hoeffding's Inequality** (Q2b)
   - Two-sided: P{|S_m - E[S_m]| ≥ t} ≤ 2 exp(-t²/(2∑a_i²))

2. **Union Bound** (Q2b, Q4c)
   - Bounding probability over multiple events

3. **VC Dimension Theory** (Q1, Q3)
   - Shattering coefficients
   - Growth functions

4. **Rademacher Complexity** (Q1, Q4)
   - R_n(F) := E[sup_{f∈F} n⁻¹ ∑ εᵢf(xᵢ)]
   - Relationship to VC dimension

5. **Concentration Inequalities** (Q2, Q4)
   - High probability bounds
   - Expectation bounds

---

## Topics Summary

### Core Theory
- VC Dimension
- Rademacher Complexity
- PAC Learning
- Concentration Inequalities

### Kernel Methods
- Kernel properties (PSD, shift-invariance)
- Random Fourier Features
- Feature maps

### Statistical Learning
- Empirical Risk Minimization
- Generalization bounds
- CDF estimation (Glivenko-Cantelli)

### Loss Functions
- Zero-one loss
- Surrogate losses
- Hinge loss (implicitly via SVM)

### Optimization/Algorithms
- Perceptron
- SVM
- Linear classifiers
