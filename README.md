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
### Deep Momentum Network v2 · [deep_momentum_alpaca_v2.ipynb](deep_momentum_alpaca_v2.ipynb)

Réplication de l'article **Lim, Zohren & Roberts (2019)**, *Enhancing Time Series Momentum Strategies Using Deep Neural Networks*, sur 16 ETF multi-actifs avec les données Alpaca.

**Méthode**
- Données journalières ajustées de janvier 2016 à novembre 2026 (16 ETF : actions, obligations, matières premières, devises)
- Variables : rendements normalisés (1 j à 12 mois) et indicateurs MACD de Baz (équations 4 à 6)
- Modèle : LSTM à sorties directes (position dans [-1, 1]) entraîné en maximisant le ratio de Sharpe (équation 16)
- Entraînement 2016-2022, test hors échantillon 2023-2026, volatilité cible 15 %, coûts de 2 pb

**Résultats hors échantillon (2023-2026)**

| Stratégie | Rendement an. | Volatilité | Sharpe | Perte max |
|---|---|---|---|---|
| Buy & hold | 9,5 % | 7,7 % | 1,23 | -7,5 % |
| Deep Momentum LSTM | 2,1 % | 3,6 % | 0,58 | -4,5 % |
| Moskowitz 2012 | 3,4 % | 6,2 % | 0,54 | -7,3 % |
| Baz MACD 2015 | 1,3 % | 3,9 % | 0,33 | -5,4 % |

**Analyse**
- Sur cette période haussière, aucune stratégie de momentum ne bat le buy & hold.
- Le LSTM montre un surapprentissage net : le Sharpe d'entraînement monte (0,3 → 0,6) pendant que le Sharpe de validation chute (+0,55 → -0,75). La validation (2021-2022, choc d'inflation) correspond à un régime absent de l'entraînement.
- Le résultat du LSTM n'est donc pas significatif. Seule sa perte maximale plus faible est un point positif.

**Prochaines étapes**
- Réduire la taille du réseau et augmenter la régularisation
- Validation walk-forward sur plusieurs fenêtres
- Test sur plusieurs graines aléatoires pour mesurer la stabilité
