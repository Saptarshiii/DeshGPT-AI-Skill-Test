# Government Clinic Dataset Preprocessing for AI Chatbot

This project demonstrates the preprocessing of a **government healthcare dataset** (e.g., Indian city-wise government clinic data) to prepare it for **training an AI chatbot**.  
The chatbot can later be used to answer queries such as the **nearest clinic**, **doctor availability**, and **clinic details**.

---

##  Dataset
The dataset contains information about **government clinics** in various cities, including:
- Clinic codes & numbers
- City names & codes
- Latitude & longitude
- Doctor availability
- Contact information
- Category/type of clinic

**Example columns:**
```
ClinicCenterCode | ClinicNumber | ClinicCenterAddress | CityName | CityCode | Latitude | Longitude | DoctorCount | Category
```

---

##  Preprocessing Steps

### 1️ Load Data
- Read the dataset using **pandas**.
- Convert it into a DataFrame for easier manipulation.

```python
df = pd.read_csv("city-wise-govt-clinic.csv")
```

---

### 2️ Handle Missing Values
- Replace placeholders (`'*'`, `NA`, `null`, `NULL`, `NaN`) with `NaN`.
- Drop irrelevant or empty columns (`ClinicName` in this case).
- Remove rows missing **ClinicCenterCode** (treated as a primary key).
- Drop rows where **both** `ClinicNumber` and `ClinicCenterAddress` are missing.
- Remove clinics with `DoctorCount = 0`.

---

### 3️ Data Type Conversion
- Convert numerical columns (`CityCode`, `DoctorCount`, `Latitude`, `Longitude`) to numeric data types for consistency.
- Handle conversion errors gracefully (`errors='coerce'`).

---

### 4️ Text Standardization
- Strip whitespace and standardize case for:
  - `Category` → Title Case
  - `CityName` → Title Case
  - `ClinicCenterAddress` → Clean formatting

---

### 5️ Encode Categorical Values
- Encode `Category` using **LabelEncoder** for chatbot-friendly numeric representation.
- Save the mapping for interpretability.

---

### 6️ Save Cleaned Data
- Export the processed dataset to `cleandata.csv` for downstream AI chatbot training.

---

##  Ethical Considerations
When working with government health data:
- **Privacy**: Ensure that no personally identifiable information (PII) is stored or exposed.
- **Consent**: Use publicly available datasets or datasets with explicit usage rights.
- **Security**: Store datasets securely to prevent misuse.

---

##  Bias Mitigation
- Avoid regional or language bias by **standardizing city and category names**.
- Ensure small cities with fewer clinics are not deprioritized in chatbot recommendations.
- Regularly update the dataset to avoid outdated or skewed responses.

---

##  Potential Chatbot Capabilities
- Find the nearest government clinic using latitude & longitude.
- Display doctor availability for each clinic.
- Filter clinics by category (e.g., general, specialty).
- Provide clinic addresses and contact details.

---

##  How to Run
1. Place `city-wise-govt-clinic.csv` in the working directory.
2. Install dependencies:
   ```bash
   pip install pandas numpy scikit-learn geopy
   ```
3. Run the preprocessing script:
   ```bash
   python preprocessing.py
   ```
4. Use `cleandata.csv` as the input for AI chatbot training.

---

##  License
This code is intended for **educational and research purposes** only. Ensure compliance with government data usage policies before deploying in production.
