# Reddit Climate Opinions — Analyse & Insights (Hackathon V7)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Karim7578/Hackathon_1/blob/main/Hackaton_V7.ipynb)

Analyse exploratoire et statistique d’un corpus Reddit lié au **changement climatique**, avec extraction de sentiments (VADER/TextBlob), segmentation des utilisateurs (super/regular), tests statistiques (t-test, ANOVA), et fouille lexicale (WordCloud + top termes filtrés).  
Le notebook génère des visualisations, un **dataset final prêt à l’analyse** et des **insights métier** actionnables.

---

## 📁 Données

- **Fichier d’entrée** : `reddit_opinion_climate_change.csv`  
- **Dimensions initiales** : ~ **1,2 M lignes × 50 colonnes** (après nettoyage : ~ **1,15 M lignes × 30 colonnes**)  
- **Colonnes cibles** : `self_text`, `post_title`, `post_score`, `ups`, `downs`, `user_total_karma`, `score`, `controversiality`, `created_time`, `post_created_time`, `subreddit`, etc.  

- **Sorties générées** :
  - `reddit_comments_processed.csv` — dataset final enrichi (features temps/karma/sentiment)  
  - `strict_climate_terms.png` — barplot des 100 termes climatiques les plus fréquents  

---

## 🧰 Installation

```bash
git clone https://github.com/Karim7578/Hackathon_1.git
cd Hackathon_1
pip install -r requirements.txt
```

Dépendances principales :
- pandas / numpy / matplotlib / seaborn  
- nltk (avec `vader_lexicon` et `stopwords`)  
- scikit-learn / scipy  
- wordcloud / textblob / tqdm / swifter  

---

## 🚀 Exécution

### Option A — Google Colab
- Clique sur le badge **Open in Colab** en haut.  
- Upload le fichier CSV.  
- Exécute toutes les cellules dans l’ordre.  

### Option B — Local (Jupyter)
```bash
jupyter lab
# Ouvre Hackaton_V7.ipynb
```

---

## 📊 Pipeline analytique

1. **Exploration & nettoyage**
   - Suppression colonnes >60% NaN, imputation médiane/“inconnu”, parsing des dates
   - Corrélations : karma ↔ karma_link (r=0.97), post_score ↔ commentaires (r≈0.21)

2. **Features & enrichissement**
   - `account_age_days`, log-transform des karmas, `self_text_length`, sentiment VADER (`positive/neutral/negative`)

3. **Segmentation utilisateurs**
   - `super_user` si `user_total_karma > 100000`
   - Bimodalité claire (regular ~55 karma vs super ~245 karma log-transf.)

4. **Tests statistiques**
   - t-test super vs regular : **t=25.29, p<0.0001** → super_users nettement mieux notés
   - ANOVA score ~ sentiment : **F significatif, p<0.001**

5. **Analyses temporelles**
   - Hausse forte de l’engagement en **2024+** (corrélée à événements climatiques)
   - Sentiment moyen : positif 2018–2021, stabilisation neutre depuis 2022

6. **Insights communautaires**
   - `science`, `worldnews`, `politics` = viralité forte  
   - `changemyview` = espace distinct (scores plus faibles, débats rationnels)  
   - `climate_discussion`/`climate_science` = expertise mais faible visibilité  

7. **Fouille lexicale**
   - Termes dominants : **climate, change, energy, carbon, emissions, government, china**  
   - Polarisation : positif → *hope, solar* ; négatif → *hoax, china* ; neutre → *data, carbon*  

---

## 🔎 Insights clés

- La **réputation (karma)** n’est pas corrélée directement à la visibilité → c’est surtout la **qualité du post** qui compte.  
- La communauté est **bimodale** : masse d’utilisateurs réguliers vs noyau de super-users influents.  
- **76 % des commentaires** alignés émotionnellement avec le post parent (effet de bulle), **24 % divergents** (débat/polarisation).  
- Évolution temporelle : **optimisme initial** → **neutralité/désillusion** depuis 2022.  
- Les discussions combinent 4 axes : climat (thème central), énergie, science, politique.  

---

## 🗺️ Pistes futures

- Sentiment avancé (LLM, ironie/sarcasme)  
- Topic modeling (BERTopic, LDA)  
- Détection automatique de **polarisation**  
- Dashboard Streamlit pour navigation interactive  

---

## 👥 Auteurs

- **Karim Ben Yahia** — analyse, data/ML, visualisation  
- **Léa** — synthèse, QA  

---

## 📜 Licence

GPL-3.0 (voir [LICENSE](./LICENSE))
