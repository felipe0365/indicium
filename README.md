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
-   **Serialização:** Pickle

## 📁 Estrutura do Repositório

```
.
├── imdb_analysis_and_prediction.ipynb   # Notebook Jupyter com todo o código e análise.
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
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3. **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
    _(Para criar o arquivo `requirements.txt`, execute `pip freeze > requirements.txt` no seu ambiente virtual após instalar as bibliotecas)._

## 🚀 Como Utilizar

### Para Análise e Treinamento

Abra e execute o notebook `imdb_analysis_and_prediction.ipynb` em um ambiente Jupyter. Ele contém todos os passos da análise, visualizações e o treinamento do modelo.

### Para Fazer uma Nova Previsão

Você pode usar o modelo salvo (`imdb_rating_predictor.pkl`) para fazer previsões em novos dados sem precisar treinar tudo novamente. Utilize o script abaixo como exemplo:

```python
import pickle
import pandas as pd

# Carrega o modelo salvo
with open('imdb_rating_predictor.pkl', 'rb') as file:
    loaded_model = pickle.load(file)

# Dados de um novo filme (exemplo)
new_movie_data = {
    'Released_Year': '2021',
    'Runtime': '155 min',
    'Genre': 'Sci-Fi, Adventure',
    'Meta_score': 84.0,
    'Director': 'Denis Villeneuve',
    'No_of_Votes': 650000,
    'Gross': '108,327,830'
}
new_movie_df = pd.DataFrame([new_movie_data])

# Aplica as mesmas transformações dos dados de treino
new_movie_df['Runtime'] = new_movie_df['Runtime'].str.replace(' min', '').astype(int)
new_movie_df['Gross'] = new_movie_df['Gross'].str.replace(',', '').astype(float)
new_movie_df['Released_Year'] = new_movie_df['Released_Year'].astype(int)
new_movie_df['Movie_Age'] = 2023 - new_movie_df['Released_Year']
new_movie_df['Main_Genre'] = new_movie_df['Genre'].apply(lambda x: x.split(',')[0])

# Faz a previsão
predicted_rating = loaded_model.predict(new_movie_df)
print(f"A nota IMDB prevista para o novo filme é: {predicted_rating[0]:.2f}")
```
