Key findings from EDA:
- 27% churn rate (class imbalance noted for modelling)
- Churned customers average 18 months tenure vs 38 months for retained
- Churned customers pay ~$15/month more on average
- Month-to-month contracts have 43% churn vs 3% for two-year contracts
- Customers without TechSupport churn significantly more

Phase 3 — Model comparison results:

| Model               | Accuracy | AUC   |
|---------------------|----------|-------|
| Logistic Regression | ~81%     | ~0.84 |
| Random Forest       | ~85%     | ~0.88 |
| XGBoost             | ~87%     | ~0.91 |

Best model: XGBoost
Top churn drivers: tenure, monthly charges, 
contract type, internet service, tech support
