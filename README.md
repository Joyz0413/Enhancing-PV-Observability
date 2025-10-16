## Data Access

This project uses external datasets that are not included in the repository due to licensing restrictions.  
Users must obtain the data from the official sources below before running the code.  

### 1. Pecan Street Dataport (PV power + metadata）
- Website: [https://dataport.pecanstreet.org/](https://dataport.pecanstreet.org/)  
- Access: University researchers can apply using an institutional email.  
- Steps: Register → Apply for academic license → Download PV generation and consumption data.  
- Note: Subject to Pecan Street Inc. licensing terms.  

### 2. NREL NSRDB (GHI)
- Website: [https://nsrdb.nrel.gov/data-sets/how-to-access-data](https://nsrdb.nrel.gov/data-sets/how-to-access-data)  
- Access: Requires NREL developer account and API key.  
- Steps: Register → Request API key → Use NSRDB API to download GHI and meteorological data.  
- Docs: API usage instructions are available on the NSRDB website.  

ShrPVProfile.ipynb
输入
Y_list.csv 
c_ratio_pecan.csv
Outputs:
  - D_orth.csv : learned dictionary (orthonormal columns)
  - X_orth.csv : concatenated sparse codes [South | West | East]

Capacity_estimation.ipynb
  Y_test_1.csv   —— PV power measurement :  Y^mea_n
  Y_s_ave.csv    —— Normalized PV profile for unique-azimuth systems Y_d (south)
  Y_w_ave.csv    —— Normalized PV profile for unique-azimuth systems Y_d (west)
  Y_e_ave.csv    —— Normalized PV profile for unique-azimuth systems Y_d (east)
  - D_orth.csv : learned dictionary (orthonormal columns)
  - X_orth.csv : concatenated sparse codes [South | West | East]
输出


PV_forecast.ipynb
CNN_LSTM节
    csv_path: str = r"D:\15minute_data_austin\PV_power_GHI.csv"  # must contain solar_radiation, pv_power
    out_dir:  str = r"D:\15minute_data_austin\sample\cnn_lstm_5d"

XGboost节
输入
split_days_csv_path: str = r"D:\15minute_data_austin\sample\cnn_lstm_5d\split_days.csv"
csv_path: str = r"D:\15minute_data_austin\PV_power_GHI.csv"  # must contain solar_radiation, pv_power
out_dir: str = r"D:\15minute_data_austin\sample\single_r2p"

Procrustes节
输入
CSV_DATA_PATH = r"D:\15minute_data_austin\PV_power_GHI.csv"            # PV_power_GHI dataset columns: solar_radiation, pv_power
D_ORTH_CSV    = r"D:\15minute_data_austin\sample\D_orth.csv"           # Orthogonal Dictionaty D
X_ORTH_CSV    = r"D:\15minute_data_austin\sample\X_orth.csv"           # Sparse Coding X^sep
SPLIT_CSV     = r"D:\15minute_data_austin\sample\cnn_lstm_5d\split_days.csv" # Split Index
capacity_csv_path = r"D:\15minute_data_austin\sample\Capacity_Data.csv" #通过registered PV metadata和Capacity_estimation.ipynb的结果整合得到
输出
OUTPUT_DIR  = Path(r"./outputs_procrustes") 
