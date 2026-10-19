# Seeing the Clouds Coming: Short-Term Solar Power Forecasting from Sky-Image Sequences

APS360 (Applied Fundamentals of Deep Learning, University of Toronto) course project by Daksh Khanna.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DakshK26/aps360-solar-nowcasting/blob/main/notebooks/solar_nowcasting.ipynb)

## Goal

Predict the power output of a 30 kW rooftop photovoltaic (PV) array **15 minutes ahead** from the
previous 15 minutes of ground-based fisheye sky images and the array's recent power history.
Passing clouds cause abrupt ramps in solar output that grid operators must cover with reserves;
a camera that "sees the clouds coming" can anticipate these ramps.

## Approach

| Component | Description |
| --- | --- |
| Data | SKIPP'D benchmark (Stanford, 2017-2019): 64x64 sky images + 1-min PV output |
| Target | Clear-sky index at t+15 min, k = P / P_clear (P_clear from a calibrated `pvlib` model) |
| Model | Shared CNN frame encoder -> LSTM over 8 frames -> fusion with PV history and sun geometry -> MLP head |
| Baselines | Smart persistence (no learning); ridge regression on PV history only |
| Metrics | RMSE, MAE (kW), forecast skill vs. smart persistence, on sunny and cloudy test days |

## Repository layout

```
notebooks/solar_nowcasting.ipynb   Colab notebook: data loading, clear-sky model, sample construction,
                                   smart-persistence baseline, model definition (training: in progress)
requirements.txt                   Python dependencies for running outside Colab
```

## Running

Open the notebook in Colab with the badge above (a GPU runtime is recommended for training), or locally:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/solar_nowcasting.ipynb
```

The dataset is downloaded automatically from Hugging Face (`solarbench/SKIPPD`).

## Data and license

SKIPP'D is released under the [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license.

> Nie, Y., Li, X., Scott, A., Sun, Y., Venugopal, V., & Brandt, A. (2023). SKIPP'D: A SKy Images and
> Photovoltaic Power Generation Dataset for short-term solar forecasting. *Solar Energy*, 255, 171-179.
> https://doi.org/10.1016/j.solener.2023.03.043
