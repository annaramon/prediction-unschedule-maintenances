# Prediction of Unscheduled Aircraft Maintenances

A predictive analytics system that forecasts unscheduled aircraft maintenance events within a 7-day window, using big data techniques and decision tree classification.

## Problem

Unscheduled aircraft maintenance causes costly delays and operational disruptions. This project aims to predict these events **7 days in advance** by analyzing historical flight data and sensor readings, enabling proactive maintenance scheduling.

## Approach

The system uses an **ELT (Extract-Load-Transform)** architecture to handle large volumes of semi-structured data from a data warehouse and CSV sensor files.

### Pipeline Architecture

The project consists of three sequential data processing pipelines:

| Pipeline | File | Purpose |
|----------|------|---------|
| **Data Management** | `management.py` | Builds a feature matrix from historical KPIs (flight hours, flight cycles, sensor 3453 averages) and labels each instance as `Maintenance` or `NonMaintenance` |
| **Model Training** | `analysis.py` | Trains a Decision Tree classifier with a 70/30 train-test split |
| **Prediction** | `classifier.py` | Takes an aircraft ID and date as input, retrieves KPIs, and predicts whether maintenance will occur within 7 days |

### Key Features (KPIs)
- **FH** — Flight Hours
- **FC** — Flight Cycles
- **DY** — Operational Days
- **Sensor 3453 Average** — Mean sensor readings aggregated per aircraft per day

## Results

| Metric | Value |
|--------|-------|
| **Accuracy** | 88–93% (varies per random split) |

Additional evaluation metrics (precision, recall, F1) are computed in `analysis.py`.

## How to Run

```bash
python main.py
```

`main.py` orchestrates all three pipelines sequentially:
1. Generates the feature matrix (cached to avoid re-computation)
2. Trains and saves the decision tree model
3. Runs the prediction classifier

## Tech Stack

- Python
- PySpark (big data processing)
- Decision Tree Classifier
- ELT Architecture

