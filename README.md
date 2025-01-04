# 🌟 Chatbot en Arabe pour le Machine Learning 🌟

---  

## Table des matières

1. [📌 Project Overview](#-project-overview)
2. [📋 Étapes Principales du Projet](#-étapes-principales-du-projet)
3. [🛠️ Lancer les Modèles Mistral 7B et Llama 3.2 avec Ollama et Docker](#️-lancer-les-modèles-mistral-7b-et-llama-32-avec-ollama-et-docker)
4. [📊 Évaluation des Modèles LLaMA et Mistral7B](#-évaluation-des-modèles-llama-et-mistral7b)
5. [🚀 Résultats et Prochaines Étapes](#-résultats-et-prochaines-étapes)
6. [📁 Structure du Répertoire](#-structure-du-répertoire)

---

## 📌 Projet en bref

Développement d'un chatbot en arabe spécialisé dans les questions liées au machine learning, avec des étapes couvrant la collecte de données, le nettoyage, la traduction, le fine-tuning des modèles LLM, et la mise en place d'une interface utilisateur intuitive.

---
---

## 📋 Étapes Principales du Projet

### 1️⃣ Scraping des Données 🔍
- **But :** Collecter des questions-réponses (Q/A) pertinentes pour le machine learning en anglais.
- **Sources utilisées :**
  - [`Turing Machine Learning Questions`](https://www.turing.com/interview-questions/machine-learning)
  - [`MyGreatLearning Blog`](https://www.mygreatlearning.com/blog/machine-learning-interview-questions/)
- **Outils :** Utilisation de `Beautiful Soup` (Python) pour le scraping.

---

### 2️⃣ Nettoyage de la Base de Données 🧹
- Suppression des caractères spéciaux, des espaces inutiles et standardisation du format des données.
- Validation manuelle pour garantir la pertinence des données collectées.

---

### 3️⃣ Traduction Anglais → Arabe 🔄
- **Outils utilisés :** Trois modèles de traduction de Hugging Face :
  - [`Helsinki-NLP/opus-mt-en-ar`](https://huggingface.co/Helsinki-NLP/opus-mt-en-ar)
  - [`marefa-nlp/marefa-mt-en-ar`](https://huggingface.co/marefa-nlp/marefa-mt-en-ar)
  - [`t5-v1_1-base`](https://huggingface.co/t5-v1_1-base)
- **Résultat :** Le modèle [`marefa-nlp/marefa-mt-en-ar`](https://huggingface.co/marefa-nlp/marefa-mt-en-ar) a produit les meilleures traductions en termes de qualité et de pertinence.

![marefa-nlp/marefa-mt-en-ar](Media/marefa1.jpg)

---

### 4️⃣ Nettoyage et Formatage des Textes en Arabe ✨
- **Outils :** API Gemini (via prompts avancés) pour :
  - Reformuler et corriger les textes.
  - Générer des données dans le format SQuAD (Q/A structuré), adapté pour l'entraînement des modèles.
- **Approche :** Multi-shot pour garantir des exemples variés et cohérents.

![marefa-nlp/marefa-mt-en-ar](Media/gemini.jpg)

---

### 5️⃣ Fine-tuning des Modèles LLM 🔧
- **Modèles testés :**
  - **Finetuned Google AI Studio** (le meilleur parmi les trois modèles testés)
  - **AraBERT**
  - **T5-Small**
- **Résultat :** Bien que Finetuned Google AI Studio ait surpassé les autres modèles en termes de performances, aucun des trois modèles n'a produit des résultats satisfaisants pour la tâche spécifique.

![Performance Comparison GIF](Media/ai_studio.gif)

---

### 6️⃣ Utilisation de Ollama et Fine-tuning 🚀
- **Plateforme utilisée :** Ollama
- **Modèles testés :**
  - `Mistral 7B`
  - `Llama 3.2`
- **Étapes :**
  - Téléchargement et fine-tuning des modèles avec des fichiers adaptés (`modelfiles`).
- **Comparaison :** Le modèle **Mistral 7B** a démontré des performances supérieures en termes de scores WSSA et de retours qualitatifs.

![marefa-nlp/marefa-mt-en-ar](Media/mistral.png)

---

### 7️⃣ Interface Utilisateur 💻
- Création d'une interface utilisateur avec **Ollama Open UI** pour interagir avec le chatbot.
- Investigation des modèles directement via l'interface pour valider leurs réponses et effectuer des comparaisons.

![marefa-nlp/marefa-mt-en-ar](Media/interface.png)

---
## 🛠️ Lancer les Modèles Mistral 7B et Llama 3.2 avec Ollama et Docker

### 1. Installation d'Ollama 📥
Avant de commencer, installez Ollama sur votre machine en suivant ces étapes :

- Rendez-vous sur le site officiel d'Ollama : [https://ollama.ai](https://ollama.ai).
- Téléchargez la version d'Ollama correspondant à votre système d'exploitation (Windows, macOS ou Linux).
- Installez l'outil en suivant les instructions spécifiques à votre plateforme.

---

### 2. Télécharger les Modèles ⬇️
Une fois Ollama installé, utilisez les commandes suivantes pour télécharger les modèles nécessaires :

#### Télécharger le modèle **Mistral 7B** :
```bash
ollama pull mistral7b 
```

#### Télécharger le modèle Llama 3.2 :
```bash
ollama pull llama3.2
```
---

### 3. Créer et Exécuter les Modèles ⚙️
Pour fine-tuner ou personnaliser les modèles avec vos propres données, utilisez la commande suivante :
```bash
ollama create -f <path-to-modelfile> <nom-du-modele>
```

- Remplacez <path-to-modelfile> par le chemin vers le fichier contenant vos données.
- Remplacez <nom-du-modele> par le nom que vous souhaitez attribuer au modèle.

#### Exemple :
```bash
ollama create -f ./data/mistral_Modelfile mistral7b-custom
```
---

### 4. Lancer les Modèles avec Docker et Open Web UI 🐳
Si vous souhaitez interagir avec les modèles via une interface graphique conviviale, utilisez Open Web UI avec Docker.

#### Étape 1 : Lancer le Conteneur Docker
```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway \
-v open-webui:/app/backend/data --name open-webui --restart always \
ghcr.io/open-webui/open-webui:main
```

#### Étape 2 : Vérifier le Conteneur
```bash
docker ps
```
#### Étape 3 : Accéder à l'Interface
Ouvrez votre navigateur web et rendez-vous à l'adresse suivante :

http://localhost:3000

![MON GIF](Media/Generetive_AI_Mlaa.gif)

---
## 📊 Évaluation des Modèles LLaMA et Mistral7B

Ce projet évalue les performances des modèles **LLaMA** et **Mistral7B** en utilisant différentes métriques pour comparer leurs réponses générées dans un contexte donné, en particulier pour des textes en langue arabe. Nous avons commencé par des métriques classiques telles que **BLEU** et **ROUGE-L**, mais avons adopté une nouvelle métrique **WSAA** (Weighted Semantic Similarity with Arabic-specific Adjustments) pour une évaluation plus précise.

### 1. Résultats **BLEU** et **ROUGE-L** 📈

#### Table des résultats

| **Question** | **Modèle**   | **BLEU** | **ROUGE-L** |
|--------------|--------------|----------|-------------|
| **1**        | LLaMA        | 0.0413   | 0.3000      |
|              | Mistral7B    | 0.0820   | 0.6667      |
| **2**        | LLaMA        | 0.1083   | 0.0000      |
|              | Mistral7B    | 0.0835   | 0.3478      |
| **3**        | LLaMA        | 0.0390   | 0.0000      |
|              | Mistral7B    | 0.0159   | 0.0000      |

#### Observations 🔍

Les résultats des métriques **BLEU** et **ROUGE-L** montrent que ni **LLaMA** ni **Mistral7B** n'ont atteint des performances satisfaisantes, particulièrement dans la question 3 où les scores sont très faibles. Ces métriques classiques ne semblent pas adaptées pour cette tâche spécifique en arabe.

---

### 2. Adopting the **WSAA** Metric 📝

Pour une évaluation plus pertinente, nous avons choisi d'adopter la **métrique WSAA** (Weighted Semantic Similarity with Arabic-specific Adjustments). Cette métrique prend en compte plusieurs aspects importants :

- **Cohérence Sémantique** : Mesure de la similarité sémantique entre la réponse générée et la référence.
- **Couverture de Domaine** : Mesure dans quelle mesure les termes spécifiques au domaine sont couverts dans les réponses générées.
- **Composants supplémentaires** : BLEU et ROUGE sont également pris en compte dans cette métrique ajustée pour l'arabe.

---

### 3. Résultats **WSAA** 📊

#### Table des résultats

| **Question** | **Model**   | **Final Score** | **Semantic Coherence** | **Domain Coverage** |
|--------------|-------------|-----------------|------------------------|-------------------|
| **1**        | LLaMA       | 0.3788          | 0.8449                 | 0.0000            |
|              | Mistral7B   | 0.3662          | 0.8205                 | 0.0000            |
| **2**        | LLaMA       | 0.3798          | 0.9058                 | 0.0000            |
|              | Mistral7B   | 0.3461          | 0.8538                 | 0.0000            |
| **3**        | LLaMA       | 0.5015          | 0.9201                 | 0.5000            |
|              | Mistral7B   | 0.3900          | 0.9289                 | 0.5000            |

---

### 4. Conclusion : Le Meilleur Modèle 🏆

En conclusion, bien que **LLaMA** ait montré des performances initiales acceptables selon certaines métriques, **Mistral7B** s'avère être le modèle le plus performant sur la base de notre métrique **WSAA**. Cela en fait le choix optimal pour générer des réponses cohérentes et pertinentes, en particulier dans un contexte en arabe.

Nous recommandons donc **Mistral7B** comme modèle principal pour les tâches de génération de texte dans ce domaine.

---

## 🚀 Résultats et Prochaines Étapes
- **Meilleur modèle :** `Mistral 7B`
- **Prochaines étapes :**
  - Améliorer la robustesse du chatbot sur d'autres dialectes arabes 🌍
  -  Implémenter un système de feedback utilisateur pour améliorer les réponses 📝
  -  Développer une API RESTful pour faciliter l'intégration 🔗

  

---
# 📁 Structure du répertoire
```plaintext
project/
│
├── Improving Squad Files (Api Gemini)/         # Contains formatted datasets and related notebooks
│   ├── clean_text.ipynb                        # Notebook for text cleaning
│   ├── squad_formatted_dataset1-1.json         # Formatted SQuAD dataset version 1.1
│   └── squad_formatted_dataset_multi_shot.json # Multi-shot SQuAD formatted dataset
│
├── data cleaning/                              # Data cleaning scripts and datasets
│   ├── clean.ipynb                             # Notebook for cleaning data
│   ├── cleaned_ml_questions.csv                # Cleaned dataset of ML questions
│   └── greatlearning_ml_questions.csv          # Raw dataset from Great Learning
│
├── Finetune/                                   # Fine-tuning notebooks
│   ├── API gemini.ipynb                        # Notebook for API Gemini fine-tuning
│   ├── AraBERT_.ipynb                          # Notebook for AraBERT fine-tuning
│   ├── t5smallarabe.ipynb                      # Notebook for fine-tuning T5 small Arabic model
│   └── out of memory(ambanovasystemsSambaLingo-Arabic-Chat)/  # Out-of-memory experiments
│
├── Media/                                      # Media assets for the project
│
├── Models_ollama/                              # Models and metric evaluation files
│   ├── Metriques/                              # Metrics evaluation
│   │   └── metriques.ipynb                     # Notebook for metrics evaluation
│   └── ModelFiles/                             # Model generation files
│       ├── generate_model_file.ipynb           # Notebook to generate model files
│       ├── Modelfile llama3.2/                 # Model files for LLaMA 3.2
│       │   └── Modelfile                       # Main model file
│       └── Modelfile Msirtral7b/               # Model files for Msirtral 7B
│           └── Modelfile                       # Main model file
│
├── Scraping/                                   # Scraping scripts and results
│   ├── greatlearning_ml_questions.csv          # Dataset scraped from Great Learning
│   ├── scrape1.ipynb                           # First scraping notebook
│   ├── scrape2.ipynb                           # Second scraping notebook
│   ├── turing_ml_questions_with_images.csv     # Turing ML questions with images
│   ├── httpswww.turing.cominterview-questionsmachine-learning/  # Turing source data
│   └── images/                                 # Images scraped from Turing
│
├── traduction/                                 # Translation datasets and configurations
│   ├── Helsinki-NLPopus-mt-en-ar/              # Helsinki NLP translation configurations
│   ├── marefa-nlpmarefa-mt-en-ar/              # Marefa translation configurations
│   ├── questions_translated.csv                # Translated questions dataset
│   └── t5-v1_1-base/                           # Base configuration for T5 translation
│
└── README.md                                   # Project documentation
```
## 👥 Contributions

Ce projet a été développé en collaboration par :

- **Mohamed Habib Kammoun** 👨‍💻
- **Ahmed Rami Belguith** 👨‍💻
- **Dhia Elhak Toukebri** 👨‍💻

<a href="https://github.com/habibkammoun/GenrativeIA_ML_questions_arabic/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=habibkammoun/GenrativeIA_ML_questions_arabic" />
</a>
