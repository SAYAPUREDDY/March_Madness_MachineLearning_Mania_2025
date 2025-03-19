# Aspect Term Extraction and Polarity Classification

## Overview
This project implements **Aspect Term Extraction** and **Polarity Classification** using sentiment analysis techniques. The system processes customer reviews to extract aspect terms and classify their sentiment as Positive, Negative, or Neutral.

It also features a **Streamlit GUI Dashboard** to visualize sentiment trends across various aspects and locations.

---

## Problem Statement
Businesses receive a large volume of customer reviews daily. However, understanding and analyzing these reviews effectively presents challenges:

- What aspects of a store or service do customers praise or criticize?
- Why do customers leave positive, negative, or neutral feedback?
- Which specific areas or locations require immediate attention?

Without a structured approach to extract and analyze aspects, businesses may overlook valuable insights that could improve customer experience.

---

## Solution
Our tool leverages **natural language processing (NLP)** to analyze reviews by:

1. **Extracting Key Aspects**: Identifying elements like service quality, pricing, staff behavior, etc.
2. **Sentiment Classification**: Determining the sentiment associated with each aspect (Positive, Negative, Neutral).
3. **Aspect Analysis by Location**: Highlighting store-specific issues to enable targeted improvements.

---

## Features
- **Aspect Term Extraction**: Identifies key aspects from customer reviews.
- **Polarity Classification**: Categorizes sentiments into Positive, Negative, or Neutral.
- **Interactive Dashboard**: Visualizes insights using **Streamlit**.
- **Data Filtering**: Allows querying results for a specific store/place ID.
- **Charts and Graphs**: Displays sentiment trends using bar charts and heatmaps.
- **Comprehensive Insights**: Analyzes sentiment trends across multiple locations.

---

## Dataset Preparation
### Pre-word Segmentation (For Non-English Data)
- Use the Raw data with only reviews in it
Use the script:
```
https://github.com/yangheng95/ABSADatasets/blob/v1.2/DPT/pre_word_segment_for_non_english_data.py
```
Save the segmented files in the `data/segmented_data` directory.

### Split the data
The segmented data is automatically annotated and split into training, validation, and test datasets:

| File | Content |
|------|---------|
| train.csv | 70% of original data |
| valid.csv | 15% of original data |
| test.csv | 15% of original data |

### Auto-Annotation and ATEPC Data preparation
### make_ATC_dataset.py
This script processes raw review datasets which are segmented and prepares them for aspect-term extraction.
#### Usage:
```bash
python make_ATC_dataset.py
```
The APC dataset is then converted to ATEPC format using the `convert_atc_to_atepc.py` script.
### convert_atc_to_atepc.py
This script converts **APC format** datasets to **ATEPC format** for training.
#### Usage:
```bash
python convert_atc_to_atepc.py
```
### Preparing Custom Dataset
Your custom dataset should be merged into `integrated_datasets/atepc_datasets/<dataset_id>` following the naming conventions outlined [here](https://github.com/yangheng95/ABSADatasets?tab=readme-ov-file#auto-annoate-your-datasets-via-pyabsa).

### Training
This script trains an Aspect Term Extraction model using the PyABSA framework. 
It configures the FAST_LCF_ATEPC model, sets training parameters, and loads the 
specified dataset for training. 
The training process is flexible, supporting checkpointing, auto device selection, and augmentation options.

Note: Please replace the number of Epochs in the pyabsa library
Note: Please change the custom dataset based on your dataset

if the training is successful u will get the checkpoints saved to your local filesystem.
which can later be used while testing the model.

#### Usage:
```bash
python training_the_atepc.py
```

### Inference
This script performs aspect term extraction and polarity classification on reviews using a pre-trained model.
- The checkpoint files from training exist in the `checkpoints/` folder.
- If missing, create the `checkpoints/` directory and store the obtained checkpoints.
#### Usage:
```bash
python inference.py
```

### Overall_analysis.py
This script provides an overall analysis of extracted aspects and sentiments from multiple stores.
#### Usage:
```bash
python overall_analysis.py
```

---

## Sample Analysis

### Sample Review 1:
**Review:**
> "Really great stuff, you can always find something. The employees are always very nice, they also have small talk with the customers. Very helpful, always happy to go."

**Extracted Aspects:**
- **Stuff**: Positive (Confidence: **99.91%**)
- **Employees**: Positive (Confidence: **99.94%**)

### Sample Review 2:
**Review:**
> "Great store. The prices have also risen here and the quality has become inferior. The material has become thinner, and the 3-pack became a 2-pack at the same price."

**Extracted Aspects:**
- **Prices**: Negative
- **Quality**: Negative

---

## Streamlit GUI Dashboard

### Features:
- Enter a **placeId** to retrieve sentiment insights.
- Toggle various checkboxes to generate visualizations.
- View sentiment trends for specific locations.

### Run the Dashboard:
```bash
streamlit run gui.py
```

### Install Dependencies
```bash
pip install requirements.txt
```

### Dataset Structure
1. **store_aspect_sentiment_analysis.csv** - Aggregated sentiment counts per store.
2. **reviews_with_aspects_utf8_2024.csv** - Reviews with extracted aspects and sentiments.

Ensure these files are in the working directory before running the application.
---

## Contributors
- **Sayapureddy Sai Surya Teja** - Developer

---

## License
This project is licensed under the **MIT License**.

---

Turn customer reviews into actionable insights. Enhance your business strategy with data-driven sentiment analysis! 🚀

