# Simulateur de Remboursement MGC

Outil de simulation, vérification et comparaison des remboursements santé pour les contrats de la Mutuelle Générale des Cheminots (MGC).

**[→ Voir la démo en ligne](https://mohammadaima.github.io/simulateur-mgc/)**

---

## Contexte

Les gestionnaires MGC ont besoin d'une base de vérification fiable pour contrôler les montants de remboursement calculés par les systèmes de liquidation.

Au-delà du calcul, j'ai choisi d'enrichir chaque résultat de commentaires contextuels — explication du régime applicable, règles légales en jeu, avertissements sur les plafonds et cas particuliers — afin que l'outil puisse aussi servir de support au conseil adhérent, pas uniquement à la vérification.

---

## Ce qui distingue ce projet d'un simple simulateur

Un simulateur standard retourne un montant. Celui-ci :

- **Détaille chaque étape** du calcul (DR → MRO → gap → base MGC → Min STS-AMC → RAC) avec la formule affichée et commentée
- **Explique le contexte réglementaire** à chaque étape : participation forfaitaire, règle de la dépense engagée, contrats responsables vs non-responsables, spécificités des régimes spéciaux
- **Compare tous les contrats** sur un même acte et régime pour orienter le conseil
- **Signale les cas particuliers** : dépassements hors plafond, actes non couverts, forfaits annuels vs par acte

---

## Fonctionnalités

- Simulation pour **22 actes médicaux** (consultations, hospitalisation, dentaire, optique, kinésithérapie, pharmacie)
- **22 régimes de Sécurité Sociale** (RG, Fonction Publique, SNCF Actifs, SNCF Retraités, RATP, MSA…)
- **Comparaison de 35 contrats MGC** sur un même acte et régime, affichée en tableau après chaque simulation
- Détail du calcul étape par étape, basé sur la formule STS-AMC :

```
MGC = Min ( DR − MRO , Plafond , %TR + forfait + %DR + %TM + %PMSS )
```

- Tableau Excel joint : 224 lignes × 35 contrats × 4 colonnes (Typique, Sécu AMO, MGC AMC, RAC) — onglets RG, SNCF Actifs, SNCF Retraités

---

## Glossaire

| Acronyme | Signification |
|---|---|
| **MGC** | Mutuelle Générale des Cheminots |
| **AMO** | Assurance Maladie Obligatoire (Sécurité Sociale) |
| **AMC** | Assurance Maladie Complémentaire (mutuelle) |
| **STS-AMC** | Système de Tiers-payant AMC |
| **DR** | Dépense Réelle — montant facturé au patient |
| **MRO** | Montant Remboursé par l'Organisme obligatoire (part AMO) |
| **RAC** | Reste À Charge — montant définitif à la charge du patient |
| **%TR** | Pourcentage du Tarif de Responsabilité (= BR × coefficient contractuel) |
| **%TM** | Pourcentage du Ticket Modérateur (= BR × (1 − taux AMO)) |
| **%PMSS** | Pourcentage du Plafond Mensuel de la Sécurité Sociale (3 864 €/mois en 2024) |
| **%DR** | Pourcentage de la Dépense Réelle (contrats "frais réels") |
| **BR** | Base de Remboursement — tarif de référence fixé par l'Assurance Maladie |
| **RG** | Régime Général |
| **TDG** | Tableau de Garanties — référentiel contractuel source (TDG_QUARK MGC) |

---

## Ce que l'outil révèle

Le tableau comparatif et le fichier Excel permettent de dégager des indicateurs concrets :

- **Pertinence des gammes par régime** — certains contrats sont nettement plus avantageux pour les régimes spéciaux (SNCF, RATP) que pour le RG, du fait de taux AMO différents
- **Seuils de déclenchement des garanties** — on identifie à quel montant de dépense un contrat supérieur devient réellement utile vs un contrat de base
- **RAC résiduel par poste** — dentaire, optique et hospitalisation restent les postes à fort RAC même avec les meilleurs contrats
- **Impact des régimes spéciaux** — les retraités SNCF bénéficient de taux AMO plus élevés (75-100%) qui réduisent mécaniquement le rôle de l'AMC sur certains postes

---

## Aperçu du simulateur : 

> *<img width="767" height="467" alt="image" src="https://github.com/user-attachments/assets/27584ae1-055a-4d89-8939-573ae6357fd3" />*

---

## Fichiers

| Fichier | Description |
|---|---|
| `index.html` | Simulateur complet — autonome, aucune dépendance externe |
| `remboursements_mgc.xlsx` | Tableau précalculé (généré par Python/openpyxl) |

---

## Choix techniques

**JavaScript vanilla sans framework** — fichier HTML unique déployable sans build step ni serveur. Maintenabilité maximale pour une équipe non technique, compatibilité universelle.

**Données embarquées** — les garanties contractuelles (35 contrats, 22 actes) sont encodées directement dans le JS à partir du TDG source. Fonctionnement hors-ligne, aucune dépendance API.

**Formule STS-AMC** — la logique de calcul reproduit fidèlement la formule utilisée par les systèmes de tiers-payant AMC, avec décomposition explicite de chaque terme (DR, MRO, %TR, TM, PMSS, forfaits).

---

## Ce que ce projet m'a appris

- Modélisation d'une règle métier complexe en logique algorithmique
- Traitement et normalisation de données hétérogènes issues d'un référentiel réel (formats mixtes : multiplicateurs, forfaits €/jour, pourcentages, frais réels)
- Construire un outil utilisable par des non-développeurs sans formation préalable

---

## Lancer en local

Ouvrir `index.html` directement dans un navigateur — aucune installation requise.

---

## Stack

`HTML` `CSS` `JavaScript vanilla` `Python` `openpyxl`

---

## Auteur

**De Mohammad Aima - Support MAPS DSIO** -

---

## Licence

MIT
