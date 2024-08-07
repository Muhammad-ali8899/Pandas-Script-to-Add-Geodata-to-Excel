# Pandas-Script-to-Add-Geodata-to-Excel
#A Python script using pandas to add latitude and longitude to an Excel file with district wise. 

import pandas as pd

# Define the district data
district_data = {
"BADIN": (24.3030, 68.8210),
"DADU": (26.7300, 67.8400),
"Ghotki": (28.0678, 69.3310),
"HYDERABAD": (25.3960, 68.3578),
"IKAR PUR": (25.5115, 68.1731),  
"JACUBABAD": (28.2933, 68.4344),
"JAMSHORO": (25.4167, 68.2833),
"KARACHI": (24.8607, 67.0011),
"KASHMORE": (27.0000, 69.5700),
"KHAIRPUR": (27.5544, 69.0775),
"LARKANA": (27.5560, 68.2145),
"MATIARI": (25.4900, 68.2283),
"MBAR SHAHDADKOT": (27.5667, 68.1360),  
"MIRPURKHAS": (25.5275, 69.0151),
"MITTHI": (25.4361, 69.8551),
"NAUSHERO FEROZ": (27.2062, 68.1212),
"NAWAB SHAH": (26.2600, 68.4000),
"Qambar Shahdadkot": (27.5906, 68.1140),
"SAJAWAL": (24.7050, 67.8667),
"SANGHAR": (25.5322, 68.9290),
"SHIKAR PUR": (27.9750, 69.0486),
"SUKKAR": (27.7120, 69.0188),
"TANDO MUHAMMAD KHAN": (25.7216, 68.8516),
"TANDOALLAHYAR": (25.4364, 68.7677),
"Tando Muhammad Khan": (25.7216, 68.8516),   
"UMERKOT": (25.3769, 69.0872),
}
# Load the Excel file
file_path = 'Country_level_Education_Sindh.xlsx'
df = pd.read_excel(file_path)

# Normalize district names for matching
df['District'] = df['District'].str.strip().str.lower()
district_data_normalized = {key.strip().lower(): value for key, value in district_data.items()}

# Add latitude and longitude columns
df['Latitude'] = None
df['Longitude'] = None

# Match and add latitude and longitude
for idx, row in df.iterrows():
    district_name = row['District'].strip().lower()
    if district_name in district_data_normalized:
        lat, lon = district_data_normalized[district_name]
        df.at[idx, 'Latitude'] = lat
        df.at[idx, 'Longitude'] = lon

# Save the updated DataFrame back to Excel
output_file_path = 'Country_level_Education_Sindh_lat.xlsx'
df.to_excel(output_file_path, index=False)

print(f"Updated Excel file saved at: {output_file_path}")
