<p align="center">
  <img src="assets/gpyucatan200_logo.png" width="350" alt="Gran Premio Yucatán 200 Logo">
</p>

# 🏎️🏁 NASCAR Mexico Series Predictor

A Python-based Machine Learning pipeline developed to predict the finishing order of the full grid (20 cars) in the **Gran Premio Yucatán 200** of the NASCAR Mexico Series, held at the Autódromo Emerson Fittipaldi (Mérida, Yucatán).

## 📸 On-Track Action (October 17, 2026)
*Direct visual documentation from the Autódromo Emerson Fittipaldi during the race weekend.*

<p align="center">
  <img src="assets/carrera.jpeg" width="750" alt="Cars on track - Autódromo Emerson Fittipaldi">
</p>

## 🚀 Project Architecture

This model does not use simulated data; it is fed by real, verifiable championship information:

- **Live Data Ingestion (Race.mx):** Connection to the official open data API to extract real-time Chase *Standings* and the starting grid.
- **Dynamic Weather (OpenWeatherMap):** Integration of meteorological telemetry (temperature and rain probability) from Mérida to calculate a custom `HeatTrafficStress` index.
- **Feature Engineering:** 
  - `ChaseMomentum`: Tracks a driver's performance trajectory by comparing their initial Playoff seed with their current ranking.
  - `TargetDominanceScore`: A composite target variable that weighs regular season vs. Playoff performance.
- **Predictive Model:** Implementation of `XGBRegressor` with **Monotonic Constraints** (to enforce sports logic in the decision tree) and **Leave-One-Out Cross-Validation (LOOCV)** with *Out-Of-Fold* predictions to completely eliminate grid *overfitting*.

## 🛠️ Technologies Used

- **Language:** Python 3.12
- **Machine Learning:** XGBoost, Scikit-Learn
- **Data Wrangling:** Pandas, NumPy
- **APIs:** Requests, JSON

## ⚙️ Installation and Usage

1. Clone the repository and install the dependencies:
```bash
git clone [https://github.com/YOUR_USERNAME/nascar-mexico-predictions2026.git](https://github.com/YOUR_USERNAME/nascar-mexico-predictions2026.git)
cd nascar-mexico-predictions2026
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

2. Configure your API keys by creating a `.env` file in the project root:
```env
OPENWEATHERMAP_API_KEY=your_api_key_here
```

3. Run the complete pipeline from the Jupyter Notebook:
```bash
jupyter notebook notebook/main.ipynb
```

## 📝 Licenses

- **Code:** This project is distributed under the [MIT License](LICENSE). You are free to use and modify the predictive model's architecture.
- **Data:** The standings, drivers, and venue information is extracted from the [Race.mx](https://race.mx) open API and used under the [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license.