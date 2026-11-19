# labo-momentum
Réplications de papiers sur le momentum
## Contenu

### Momentum
[01_momentum_replication](01_momentum_replication.ipynb)
Test d'une stratégie momentum 12 mois.

### Contrôle optimal stochastique LQ
[notebook/riccati_lq_montecarlo.ipynb](notebook/riccati_lq_montecarlo.ipynb)
Résolution par l'équation de Riccati, vérifiée par Monte-Carlo.
Coût optimal 0.678 ± 0.014 contre 0.681 en théorie, et 1.213 sans contrôle.
### Journal 19/11/2026 - Alpaca
-  Testé : lire l'historique des ordres et annuler un ordre en attente. Erreurs              de frappe (ALL, filtre, cancel_orders).
- Vu : Run all a relancé un achat SPY par accident. Gain de 0,06 $ = 730 − 729,94.
- Pas compris : à quoi sert concrètement de lire l'historique des ordres.
- Fait : interrupteur TRADING_ACTIF, Run all ne passe plus d'ordre.   
