# Data Processor README

## Overview

The DataProcessor class is a comprehensive tool for preprocessing
datasets for machine learning. It streamlines the cleaning,
transformation, encoding, and scaling of data, ensuring it is ready for
analysis or model training. The class includes methods for handling
missing values, outliers, categorical encoding, and scaling, and
integrates Google Gemini AI for intelligent column processing.

## Features

### 1. Handling Missing Values

-   Automatically detects and fills missing values based on column type:

    -   Drops columns with more than 40% missing values.

    -   Fills missing categorical values with the mode.

    -   Fills missing numerical values with the mean.

### 2. Data Cleaning

-   Converts all string data in the dataset to lowercase.

-   Removes duplicate rows.

### 3. Data Type Conversion

-   Automatically identifies and converts data types:

    -   Converts strings to integers or floats if applicable.

    -   Detects and converts date columns based on various formats.

### 4. Handling Outliers

-   Removes rows with outliers in numerical columns based on Z-scores
    > (configurable threshold).

### 5. Grouping Infrequent Categories

-   Groups infrequent categories in categorical columns under the label
    > \"Other,\" based on a configurable frequency threshold.

### 6. Data Splitting

-   Splits the dataset into training and testing sets using
    > train_test_split.

### 7. Encoding Categorical Variables

-   Uses Google Gemini AI to classify columns as ordinal or nominal and
    > applies the appropriate encoding:

    -   Label encoding for ordinal columns.

    -   One-hot encoding for nominal columns with fewer than 10
        > categories.

    -   Frequency encoding or target encoding for nominal columns with a
        > higher number of categories.

### 8. Scaling Numerical Features

-   Applies scaling based on the skewness of the data:

    -   StandardScaler for highly skewed data.

    -   MinMaxScaler for less skewed data.

### 9. Integrated Google Gemini API

-   Utilizes the Google Gemini AI model to assist in determining the
    > type of categorical variables (ordinal or nominal).

-   Handles API response retries with exponential backoff.

## Dependencies

-   pandas

-   numpy

-   scikit-learn

-   category_encoders

-   scipy

-   datetime

-   google.generativeai

-   time

Install the required libraries using pip:

pip install pandas numpy scikit-learn category-encoders scipy
google-generativeai

## Usage

### Initialization

from data_processor import DataProcessor

\# Example Usage

dataframe = pd.read_csv(\'your_dataset.csv\')

processor = DataProcessor(dataframe, target_column=\'target\',
api_key=\'your_api_key\')

### Processing the Data

processor.process(test_size=0.2, z_threshold=3, category_threshold=0.05)

After processing, the cleaned and preprocessed data will be available
as:

-   processor.X_train: Training features.

-   processor.X_test: Testing features.

-   processor.y_train: Training labels.

-   processor.y_test: Testing labels.

## Methods

### handle_missing_values()

Fills or drops missing values based on predefined rules.

### lowercase_columns()

Converts all string data in the dataset to lowercase.

### remove_duplicates()

Removes duplicate rows from the dataset.

### convert_data_types()

Automatically detects and converts column data types to appropriate
formats (e.g., int, float, datetime).

### handle_outliers(z_threshold=3)

Removes rows with Z-scores above the specified threshold.

### group_infrequent_categories(threshold=0.05)

Groups infrequent categories in categorical columns under the label
\"Other.\"

### split_data(test_size=0.2, random_state=42)

Splits the dataset into training and testing sets.

### apply_encoding()

Encodes categorical variables based on their type (ordinal/nominal) and
cardinality.

### apply_scaling()

Scales numerical features using StandardScaler or MinMaxScaler based on
skewness.

### process(test_size=0.2, z_threshold=3, category_threshold=0.05)

Runs all preprocessing steps sequentially.

## 

## 

## Notes

-   Ensure your API key for Google Gemini AI is valid before using the
    > DataProcessor class.

-   Modify hyperparameters (e.g., z_threshold, category_threshold) to
    > customize the preprocessing pipeline based on your dataset.
