# 📱 Smartphone Product Price Scraping & Analysis Using R

A data science project that collects smartphone product data from the **Pickaboo e-commerce platform**, preprocesses and analyzes the data, visualizes pricing patterns, performs statistical analysis, and segments smartphones using **K-Means clustering**.

## 📌 Project Overview

This project analyzes the smartphone market in Bangladesh using real-world e-commerce data. Smartphone information was collected through an API-based web scraping approach and transformed into a structured dataset for further analysis.

The project focuses on:

- Smartphone brands and models
- Price distribution
- RAM and storage specifications
- Customer ratings
- Brand-wise pricing behavior
- Out-of-stock products
- Relationships between price and specifications
- Smartphone market segmentation

The overall workflow demonstrates a practical data science pipeline from **data collection to clustering analysis**.

---

## 🎯 Objectives

The main objectives of this project are:

1. Collect real-world smartphone product data from an e-commerce platform.
2. Extract important product information such as brand, model, RAM, storage, price, and rating.
3. Clean and preprocess the collected dataset.
4. Explore smartphone pricing and brand-wise market patterns.
5. Analyze the relationship between smartphone specifications and price.
6. Perform statistical analysis to investigate relationships between brand and stock availability.
7. Segment smartphones into different market groups using K-Means clustering.

---

## 🛠️ Technologies & Libraries

### Programming Language
- **R**

### Libraries

| Library | Purpose |
|---|---|
| `httr` | HTTP requests and API communication |
| `jsonlite` | Parsing JSON API responses |
| `stringr` | Regular expressions and specification extraction |
| `dplyr` | Data manipulation and preprocessing |
| `ggplot2` | Data visualization |
| `tidyr` | Data transformation |
| R Base | Statistical analysis and data processing |

The report specifically identifies `httr`, `jsonlite`, `stringr`, and `dplyr` as core libraries used during data collection and preprocessing.

---

## 🔄 Project Workflow

```text
Pickaboo E-commerce Website
          ↓
     API Data Collection
          ↓
       JSON Parsing
          ↓
   Data Transformation
          ↓
   Feature Extraction
    (RAM / Storage)
          ↓
     Data Cleaning
          ↓
 Exploratory Data Analysis
          ↓
 Statistical Analysis
          ↓
   Feature Engineering
          ↓
    Data Standardization
          ↓
    K-Means Clustering
          ↓
 Market Segmentation
```

---

## 🌐 Data Collection

The project uses an API-based scraping approach instead of traditional HTML scraping.

The API returns product information in JSON format. The R `httr` package is used to send HTTP requests, while `jsonlite` is used to parse the JSON response.

The scraper processes multiple pages and removes duplicate products using product IDs. Product names are further processed using regular expressions to extract RAM and storage information.

### Extracted Attributes

The resulting dataset contains:

- **Brand**
- **Model**
- **RAM**
- **Storage**
- **Price**
- **Rating**

The scraper saves the collected data into:

```text
pickaboo_api_data.csv
```

---

## 🧹 Data Preprocessing

Several preprocessing techniques were applied before analysis.

### Missing Values

Missing model names were replaced with:

```text
Unknown
```

Missing ratings were replaced using the mean rating of the available observations.

### Feature Extraction

RAM and storage values were extracted from product names using regular expressions and converted into numerical features for analysis.

### Outlier Detection

The **Interquartile Range (IQR)** method was used to identify price outliers.

```text
Q1 = 25th percentile
Q3 = 75th percentile
IQR = Q3 - Q1

Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

Outliers were subsequently examined by brand.

### Scaling

Price, RAM, and Storage were standardized before applying clustering algorithms.

---

## 📊 Exploratory Data Analysis

Several visualizations were created to understand the dataset.

### 1. Price Distribution

Smartphones were grouped into **25,000 Tk price intervals** to analyze the distribution of products across different price ranges.

### 2. Number of Phones by Brand

A bar chart was used to compare the number of products available from different brands.

### 3. Out-of-Stock Products

Products with a price of zero were treated as out-of-stock products and analyzed by model.

### 4. Button Phones vs Smartphones

The dataset was divided into feature phones and smartphones based on the availability of RAM and storage information.

### 5. Average Price by Brand

Average smartphone prices were calculated for each brand to compare brand-level pricing behavior.

### 6. Price Distribution by Brand

Boxplots were used to compare price distributions across different brands.

### 7. Price vs RAM

Boxplots were used to investigate how smartphone prices vary with different RAM configurations.

### 8. Price vs Storage

The relationship between storage capacity and smartphone price was also visualized.

### 9. Brand-wise Ratings

Average customer ratings were calculated and visualized for different brands.

### 10. Price vs Rating

A scatter plot was created to investigate whether smartphone price is associated with customer ratings.

---

## 📐 Statistical Analysis

A **Chi-Square test of independence** was performed to investigate the relationship between smartphone brand and stock availability.

The report found a very small p-value and interpreted this as evidence that **brand and stock availability are related**, with some brands having more sold-out products than others.

---

## 🤖 Machine Learning: K-Means Clustering

K-Means clustering was selected for unsupervised market segmentation.

The clustering process used:

- Price
- RAM
- Storage

The features were standardized before clustering.

Based on the elbow method, **K = 3** clusters were selected.

### Cluster Interpretation

The three clusters were interpreted as:

| Cluster | Description |
|---|---|
| 🟢 Budget | Lower-priced phones with lower RAM and storage |
| 🟡 Mid-Range | Moderately priced phones with decent RAM and storage |
| 🔵 Premium | Higher-priced phones with higher RAM and storage |

These clusters provide a simple market segmentation based on smartphone price and hardware specifications.

---

## 🔍 Key Findings

### Brand & Pricing

The analysis found that **Apple and Samsung** generally have higher prices and wider price ranges compared with budget-oriented brands such as **Symphony and Walton**.

### Hardware & Price

Smartphones with higher RAM and storage generally tend to have higher prices.

### Rating & Price

Higher price does not necessarily guarantee a higher customer rating. Some lower-priced phones can have good ratings, while expensive phones may not always have the highest ratings.

### Market Segmentation

K-Means clustering identified three broad smartphone market segments:

- Budget
- Mid-range
- Premium

---

## 📁 Suggested Repository Structure

```text
smartphone-price-analysis-r/
│
├── README.md
│
├── R/
│   ├── scraping.R
│   ├── preprocessing.R
│   ├── analysis.R
│   └── clustering.R
│
├── data/
│   └── pickaboo_api_data.csv
│
├── visualizations/
│   ├── price_distribution.png
│   ├── brand_analysis.png
│   ├── price_vs_ram.png
│   ├── price_vs_storage.png
│   ├── price_vs_rating.png
│   └── clustering.png
│
└── report/
    └── Final_Project_Report.pdf
```

> **Note:** The structure above is a recommended GitHub organization based on the components described in the report; the report itself does not specify that this exact repository structure already exists.

---

## 🚀 How to Run

### 1. Install R

Install R and an R development environment such as RStudio.

### 2. Install Required Packages

```r
install.packages(c(
  "httr",
  "jsonlite",
  "stringr",
  "dplyr",
  "ggplot2",
  "tidyr"
))
```

### 3. Run Data Collection

Execute the scraping script to collect smartphone data and generate:

```text
pickaboo_api_data.csv
```

### 4. Run Preprocessing & Analysis

Load the generated dataset and execute the preprocessing and exploratory analysis scripts.

### 5. Run Clustering

Standardize the numerical features and apply K-Means clustering using:

```text
Price
RAM
Storage
```

---

## ⚠️ Limitations

The project has several limitations:

- Data was collected from only one e-commerce website.
- The dataset does not include some potentially important smartphone specifications such as camera, battery, and processor.
- The analysis represents the collected dataset rather than the entire smartphone market.

---

## 🔮 Future Improvements

Possible improvements include:

- Add battery capacity.
- Add camera specifications.
- Add processor information.
- Compare data from multiple e-commerce platforms.
- Apply DBSCAN clustering.
- Apply hierarchical clustering.
- Build a machine learning model to estimate smartphone prices based on product specifications.

---

## 👨‍💻 Contributors

- **Ehtesham Ferdous**
- **Ayon Roy**
- **Rubiat Tahsin**

### Academic Information

**Course:** Introduction to Data Science  
**Institution:** American International University-Bangladesh (AIUB)  
**Department:** Computer Science  
**Section:** K  
**Group:** H  

---

## 📄 Project Report

The complete academic project report is included in the repository.

**Project:** Smartphone Product Price Scraping and Analysis Using R

---

## ⭐ Skills Demonstrated

```text
R Programming
Web/API Scraping
JSON Data Processing
Data Cleaning
Feature Engineering
Exploratory Data Analysis
Data Visualization
Statistical Analysis
K-Means Clustering
Unsupervised Machine Learning
```