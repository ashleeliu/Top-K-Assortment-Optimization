# Featurized Choice Models for Top-K Restaurant Assortment Optimization

For this group project, we study the problem of top-K restaurant assortment optimization in digital food marketplaces (e.g., DoorDash), where platforms must choose a limited set of restaurants to display to customers.

We compare machine learning recommenders that score items independently against substitution-aware revenue management models, asking whether explicitly modeling cannibalization can outperform flexible predictive approaches in high-intent, capacity-constrained settings.


## Problem Setting

- Platform can display only K = 5 restaurants
- Customers must choose exactly one item from the offered set
- Goal: maximize expected revenue, not just clicks or hit rate
- Trade-off between:
  - Customer utility and preference matching
  - Revenue extraction via substitution and upselling

## Methodology

### Ground Truth Simulation
- Simulated 100 restaurants in Berkeley with features:
  - Cuisine type, price tier, rating, location
- Generated 10 latent customer profiles with heterogeneous preferences
- Customer choice governed by a deterministic ranked choice utility model
- Created synthetic transaction logs for training and evaluation

## Models Compared

### 1. Machine Learning Baselines
- **Random Forest**
- **XGBoost**
- Predict purchase probability independently for each restaurant
- Assortment formed by ranking items by expected revenue:
Expected Revenue = P(buy | user, restaurant) × price

Strengths:
- High hit rate
- High average customer utility

Limitations:
- Ignores substitution effects
- Suffers from revenue cannibalization

### Featurized Multinomial Logit (MNL)

- Single global preference vector estimated via MLE
- Explicitly models substitution across items
- Uses a greedy revenue optimization heuristic
- Rejects items that dilute total assortment revenue

Strengths:
- Substitution-aware
- Revenue-maximizing

Trade-off:
- Lower hit rate
- Lower customer utility

### Max Utility Oracle

- Uses true latent preferences
- Serves as a theoretical upper bound on customer satisfaction

## Evaluation

Assortments are evaluated using a Ground Truth Oracle that simulates real customer behavior.

Metrics:
- Total revenue
- Average revenue per customer
- Hit rate (favorite restaurant shown)
- Average true utility


## Key Results

- MNL (Greedy) achieves the highest revenue
- Average revenue per customer increases by ~46% relative to ML baselines
- ML models maximize hit rate but dilute revenue
- MNL sacrifices utility to extract surplus in captive demand settings


## Tools & Technologies

- Python  
- NumPy / SciPy  
- Scikit-learn  
- XGBoost  
- Optimization heuristics  
- LaTeX (for the final project report)


## Notes

This project was completed as part of a final project for INDENG 145: Fundamentals of Revenue Management at UC Berkeley.

Group members: Rishika Gorai, Ryan Gu, Ashlee Liu, Kenny Wongchamcharoen

