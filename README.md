## Bagged vs. Basic OMP

Sparse linear models like **Orthogonal Matching Pursuit (OMP)** recover a small set of predictive features, but they can suffer high variance in support selection and prediction error on small or noisy datasets. **Bootstrap aggregating (bagging)** reduces variance by averaging multiple models trained on resampled data (Efron & Tibshirani, 1994). Here, we investigate whether bagging OMP yields more reliable coefficient recovery and lower out-of-sample error.

## 2. Experimental Design

1. **Data generation:** Synthetic regression with 200 samples, 100 features, and 15 true nonzero coefficients. 30% Gaussian noise (σ=0.5).
2. **Sparsity sweep:** Evaluate OMP and Bagged‐OMP at k∈{5,10,15,20,30} nonzero coefficients.
3. **Bagging setup:** B=20 bootstrap estimators, row-only bootstrapping, coefficients averaged by inverse OOB MSE weighting.
4. **Cross-validation:** 5-fold CV for each method and sparsity level. For each fold, record:
   * **Prediction MSE** on held-out fold.
   * **Coefficient error** ‖β\_true−β\_est‖ (ℓ₂ norm).
5. **Summary tables:** Report mean±std across folds for both metrics.

## 3. Results

### 3.1 CV-MSE Comparison

```
Sparsity | OMP CV-MSE      | Bagged CV-MSE
---------+-----------------+----------------
      5  | 23622.6±7009.37 | 14962.2±2114.11
     10  |  3227.92±320.78 |  1721.43±231.60
     15  |     0.32±0.07   |     0.37±0.13  
     20  |     0.36±0.06   |     0.31±0.06  
     30  |     0.39±0.06   |     0.34±0.05  
```

### 3.2 CV Coefficient-Error Comparison

```
Sparsity | OMP CoefErr     | Bagged CoefErr
---------+-----------------+----------------
      5  | 136.40±9.99     | 115.53±5.64    
     10  |  54.12±1.83     |  41.92±1.86    
     15  |   0.17±0.03     |   0.18±0.03    
     20  |   0.31±0.01     |   0.24±0.02    
     30  |   0.42±0.02     |   0.34±0.01    
```

## 4. Conclusions

* **Bagging delivers clear variance reduction** in both MSE and coefficient‐error, especially when the chosen sparsity is below or above the ground truth.
* **Practical recommendation:** Use bagged OMP with inverse‐OOB weighting and k-fold evaluation for more reliable sparse recovery in moderate-noise settings.

*References:* Efron, B., & Tibshirani, R. J. (1994). *An Introduction to the Bootstrap*. Chapman & Hall. Mallat, S., & Zhang, Z. (1993). Matching pursuits with time-frequency dictionaries. *IEEE Transactions on Signal Processing*.
