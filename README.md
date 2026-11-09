# Jet Engine RUL Monitoring Dashboard ✈️🔧

An interactive web dashboard for predicting the Remaining Useful Life (RUL) of turbofan jet engines in real-time. Built with Streamlit, TensorFlow/Keras, and Grad-CAM interpretability.

# 📌 Overview

Predicting when a mechanical component will fail is critical for preventative maintenance. This project utilizes a Bidirectional LSTM (Long Short-Term Memory) neural network to predict the RUL of jet engines based on multivariate sensor data.

To make the model's decisions transparent, the dashboard features Grad-CAM (Gradient-weighted Class Activation Mapping), which visualizes exactly which historical sensor cycles the model focused on to make its prediction.

# ✨ Features

Real-Time Prediction: Select an engine ID to instantly view its predicted Remaining Useful Life.

Dynamic Health Status: Visual alerts based on engine health (e.g., CRITICAL status if RUL drops below a certain threshold).

Grad-CAM Interpretability: A visual heatmap (bar chart) showing the most influential timesteps in the engine's recent 50-cycle history.

Cloud-Ready: Configured to run entirely within Google Colab and broadcast to the web via ngrok.

# 📊 Dataset

This project uses the NASA C-MAPSS (Commercial Modular Aero-Propulsion System Simulation) dataset, specifically the FD001 subset.

train_FD001.txt: Training data containing run-to-failure engine simulations.

test_FD001.txt: Testing data containing engine data ending prior to failure.

RUL_FD001.txt: Ground truth RUL values for the test engines.

# 🚀 Running the Project in Google Colab

Since this project relies on a Streamlit dashboard, it requires a secure tunnel to view it from a Colab runtime.

### 1. Setup the Environment

Upload the following files to your Colab workspace (/content):
  
- dashboard.py
  
- train_FD001.txt
  
- test_FD001.txt
  
- RUL_FD001.txt

### 2. Install Dependencies
   
  Run the following in a Colab cell to install the required web and tunneling libraries:
  
```bash
  !pip install pyngrok streamlit
```


### 3. Authenticate Ngrok

Get a free auth token from ngrok.com and run this cell to set up the secure tunnel:
```bash
from pyngrok import ngrok
# Kill any existing tunnels
ngrok.kill()

# Set your token
ngrok.set_auth_token("YOUR_NGROK_AUTH_TOKEN")

# Create a tunnel on port 8501 (Streamlit's default port)
public_url = ngrok.connect(8501)
print(f"Dashboard URL: {public_url}")
```


### 4. Launch the Dashboard

Run the Streamlit app in the background:

```bash
!streamlit run dashboard.py --server.port 8501 --server.address 0.0.0.0
```



Click the Dashboard URL generated in Step 3 to view the live app!

# 🛠️ Built With

- Python

- TensorFlow & Keras (Bidirectional LSTM)

- Streamlit (Frontend UI)

- pyngrok (Localhost tunneling)

- Scikit-Learn (Data preprocessing)

- Matplotlib/Seaborn (Grad-CAM visualization)
