# Airbnb Price Prediction

Projekt dotyczy analizy oraz przewidywania cen ofert Airbnb w Nowym Jorku na podstawie danych pochodzących z Kaggle.

Celem projektu było przejście przez pełny proces tworzenia modelu machine learningowego: od czyszczenia i eksploracji danych, przez przygotowanie cech, aż po porównanie kilku modeli regresyjnych i wybór najlepszego rozwiązania.

## Project Goal

Celem projektu jest stworzenie modelu pozwalającego przewidywać cenę oferty Airbnb na podstawie dostępnych informacji o nieruchomości.

## Data

Dane wykorzystane w projekcie pochodzą z platformy Kaggle.

Przed modelowaniem dane zostały:
- oczyszczone,
- sprawdzone pod kątem brakujących wartości,
- przeanalizowane pod kątem wartości odstających,
- poddane eksploracyjnej analizie danych (EDA).

## Models

W projekcie przetestowano kilka modeli regresyjnych:

- Linear Regression
- Random Forest Regressor
- Gradient Boosting Regressor

Dodatkowo zastosowano logarytmiczną transformację zmiennej docelowej `price` oraz strojenie hiperparametrów za pomocą `RandomizedSearchCV`.

## Final Model

Najlepszym modelem został Gradient Boosting Regressor z logarytmiczną transformacją zmiennej docelowej.

Wyniki na zbiorze testowym:

- MAE: ~77.25 USD
- RMSE: ~325.49 USD
- R²: ~0.092

## Limitations

Największym ograniczeniem projektu jest niewielka liczba dostępnych cech opisujących ofertę.

Model nie posiada m.in. informacji o:
- dokładnej lokalizacji,
- powierzchni apartamentu,
- standardzie obiektu,
- udogodnieniach,
- jakości wyposażenia.

Dodatkowym problemem są bardzo wysokie, nietypowe ceny, które powodują duże błędy predykcji i mają szczególnie duży wpływ na RMSE.

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- scikit-learn
- Jupyter Notebook
- joblib

## Project Structure

### `DANE_AIR_BNB.ipynb`
Zawiera proces przygotowania danych:
- wczytanie surowego zbioru danych,
- sprawdzenie typów danych i brakujących wartości,
- czyszczenie danych,
- przygotowanie danych do dalszej analizy,
- zapis oczyszczonego zbioru.

### `AIR_BNB_EDA.ipynb`
Zawiera eksploracyjną analizę danych (EDA):
- analizę rozkładów zmiennych,
- porównanie cen między dzielnicami i typami ofert,
- analizę korelacji,
- wizualizacje danych,
- analizę wartości odstających.

### `MODEL.ipynb`
Zawiera proces budowy i oceny modeli machine learning:
- przygotowanie cech i zmiennej docelowej,
- podział danych na zbiór treningowy i testowy,
- preprocessing danych,
- Linear Regression,
- Random Forest,
- Gradient Boosting,
- cross-validation,
- transformację logarytmiczną ceny,
- eksperyment z cenami do 1000 USD,
- strojenie hiperparametrów za pomocą RandomizedSearchCV,
- finalną ocenę modelu na zbiorze testowym.

### `models/`
Zawiera zapisany finalny model:
`airbnb_price_model.pkl`

### `data/`
Zawiera dane wykorzystywane w projekcie.

## How to Run

1. Sklonuj repozytorium lub pobierz projekt na swój komputer.

2. Przejdź do głównego folderu projektu.

3. Zainstaluj wymagane biblioteki:

```bash
pip install -r requirements.txt
```

4. Uruchom Jupyter Notebook:

```bash
jupyter notebook
```

5. Otwieraj notebooki w następującej kolejności:

   1. `DANE_AIR_BNB.ipynb`  
      Wczytanie, czyszczenie oraz przygotowanie danych.

   2. `AIR_BNB_EDA.ipynb`  
      Eksploracyjna analiza danych, wizualizacje oraz analiza zależności pomiędzy zmiennymi.

   3. `model.ipynb`  
      Przygotowanie cech, trenowanie modeli, cross-validation, transformacja zmiennej docelowej, strojenie hiperparametrów oraz finalna ocena modelu.

## Using the Trained Model

Gotowy model znajduje się w folderze:

```text
models/airbnb_price_model.pkl
```

Model zawiera cały pipeline potrzebny do wykonania predykcji, w tym preprocessing danych oraz finalny model Gradient Boosting.

Można go wczytać za pomocą biblioteki `joblib` bez konieczności ponownego trenowania modelu.

Przykładowy schemat użycia:

```python
import joblib

model = joblib.load("models/airbnb_price_model.pkl")

predictions = model.predict(X_new)
```

Dane przekazane do modelu powinny zawierać takie same cechy jak dane używane podczas trenowania:

- `neighbourhood_group`
- `room_type`
- `bedrooms`
- `beds`
- `baths`

