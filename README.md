# Análise Preditiva de Notas de Filmes do IMDB

## 📋 Tabela de Conteúdos

1. [Tecnologias Utilizadas](#-tecnologias-utilizadas)
2. [Estrutura do Repositório](#-estrutura-do-repositório)
3. [Instalação e Setup](#-instalação-e-setup)
4. [Como Utilizar](#-como-utilizar)

## 🛠️ Tecnologias Utilizadas

-   **Linguagem:** Python 3.x
-   **Bibliotecas de Análise de Dados:** Pandas, NumPy
-   **Bibliotecas de Visualização:** Matplotlib, Seaborn, WordCloud
-   **Bibliotecas de Machine Learning:** Scikit-learn, XGBoost
-   **Interpretabilidade de Modelo:** SHAP
-   **Serialização:** Pickle

## 📁 Estrutura do Repositório

```
.
├── indicium_imdb.ipynb   # Notebook Jupyter com todo o código e análise.
├── imdb_rating_predictor.pkl            # Modelo treinado e serializado.
├── requirements.txt                     # Dependências do projeto para fácil instalação.
└── README.md                            # Este arquivo.
```

## ⚙️ Instalação e Setup

Para executar este projeto localmente, siga os passos abaixo:

1. **Clone o repositório:**

    ```bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    cd seu-repositorio
    ```

2. **Crie e ative um ambiente virtual (recomendado):**

    ```bash
    python -m venv venv
    source venv/bin/activate
    ```

3. **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```

## 🚀 Como Utilizar

### Para Análise e Treinamento

Você pode usar o modelo salvo (`imdb_rating_predictor.pkl`) para fazer previsões em novos dados sem precisar treinar tudo novamente. Utilize o script abaixo como exemplo:

```python
import pickle
import pandas as pd

# Carrega o pipeline completo (pré-processador + modelo)
with open('imdb_rating_predictor.pkl', 'rb') as file:
    loaded_model = pickle.load(file)

# Dados de um novo filme (exemplo)
# O modelo precisa dessas colunas.
new_movie_data = {
    'Series_Title': '',
    'Released_Year': '',
    'Certificate': '',
    'Runtime': '',
    'Genre': '',
    'Overview': '',
    'Meta_score': 0,
    'Director': '',
    'Star1': '',
    'Star2': '',
    'Star3': '',
    'Star4': '',
    'No_of_Votes': 0,
    'Gross': ''
}
new_movie_df = pd.DataFrame([new_movie_data])

# Faça esses tratamentos nos dados
top_directors = df['Director'].value_counts().nlargest(15).index
new_movie_df['Director_simplified'] = new_movie_df['Director'].apply(lambda x: x if x in top_directors else 'Other')
new_movie_df['Runtime'] = new_movie_df['Runtime'].str.replace(' min', '').astype(int)
new_movie_df['Gross'] = new_movie_df['Gross'].str.replace(',', '').astype(float)
new_movie_df['Released_Year'] = new_movie_df['Released_Year'].astype(int)
new_movie_df['Movie_Age'] = current_year - new_movie_df['Released_Year']
new_movie_df['Main_Genre'] = new_movie_df['Genre'].apply(lambda x: x.split(',')[0])

# Faz a previsão
predicted_rating = loaded_model.predict(new_movie_df)
print(f"A nota IMDB prevista para o novo filme é: {predicted_rating[0]:.2f}")

# Utilize para ver a nota
print(f" >> {final_prediction:.2f} << ")
```
