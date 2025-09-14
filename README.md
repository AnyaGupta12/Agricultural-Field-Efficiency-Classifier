#  FoML 2024 Hackathon – Agricultural Field Efficiency Classifier

##  Problem Statement
The goal of this hackathon was to **predict if an agricultural field is being used efficiently**.  
Fields are classified into three categories:
- **High performing**
- **Moderately performing**
- **Low performing**

These labels measure whether a field is achieving its potential given its resources, size, and other characteristics.  
For example, a “low performing” field may still produce a decent yield, but inefficiencies (e.g., distance from market) prevent it from reaching its full potential.

The evaluation metric is **Macro F1 Score**.

---

##  Dataset
- **Training samples**: 112,569  
- **Features**: 57  
- **Target classes**: `{high, medium, low}`  
- **Class distribution**:
  - High: 22,514  
  - Medium: 67,541  
  - Low: 22,514  

 The dataset was **highly imbalanced**, requiring resampling/oversampling techniques.

---

##  Approach & Implementation
### Preprocessing
- Handled missing values
- Normalization of features
- **Oversampling** to handle class imbalance (near-equal distribution across all classes)

### Models Explored
1. **Random Forest Classifier**
   - Hyperparameter tuning: `n_estimators`, `max_depth`, `min_samples_split`, `max_features`
   - Validation F1 Score: ~0.35

2. **Neural Networks (MLP)**
   - Tuned: number of layers, neurons, activation functions, epochs
   - Prevented overfitting via careful epoch tuning
   - Validation F1 Score: ~0.38

3. **Gradient Boosting (XGBoost/GBM)**
   - Tuned: number of trees, learning rate, max depth
   - Validation F1 Score: **0.43**
   - Test F1 Score: **0.435**

4. **Ensemble Model**
   - Combined Random Forest, XGBoost, and MLP (weighted average of probabilities)
   - Achieved highest validation F1 (~0.44)  
   - Overfitting observed (large gap between train and validation accuracy)

---

## Final Model Choice
We submitted the **Gradient Boosting Classifier** as the final model:
- Balanced generalization (less overfitting compared to ensemble)
- Achieved **F1 Score of 0.435** on the test set
- More consistent results across train/validation splits

---

## Results Summary

| Model              | Validation F1 | Test F1 |
|--------------------|--------------:|--------:|
| Random Forest      | 0.355         | 0.364   |
| Neural Network     | 0.380         | 0.380   |
| Gradient Boosting  | **0.430**     | **0.435** |
| Ensemble (RF+XGB+NN) | 0.442 (val) | Overfit |

---

## Files in Repository
- `cs24mtech11020_foml24_hackathon.ipynb` → Jupyter Notebook with preprocessing, training, and evaluation
- `cs24mtech11020_foml24_hackathon_report.pdf` → Detailed report of methods, results, and analysis
- `submission.csv` → Example Kaggle submission format

---

