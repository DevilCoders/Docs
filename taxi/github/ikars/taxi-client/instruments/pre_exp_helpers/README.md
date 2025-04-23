# Pre-exp Helper
---

Pre-exp Helper is a Jupyter Notebook are designed in order to help analysts to perform a data analysis before the start of the experiment:
- distrubution of main features
- sample size and it's influence on detected effect
- test/control groups ratio

Also the project contains small library contains some useful classes and functions for analysis.

## Who may be interested in this project?
---

Mainly, data analysts who are going to perform an AB experiment. And it's necessary for them to pre-analyze data to estimate minimum detected effects, etc.

## Installation
---

It's not a published package. So just open Notebook Templates and use data_wrapper library. 

## Usage
----

There're some work scenarios depend on what you already know about your experiment and what you want to get.

1. Load data with features.
2. Handle it.
3. Set up features calculation rules.
4. Bucketing. If you want, compare results: bootstrapped and binned.
5. **Two scenarios:**
    1. You know total sample size you want to perform experiment on.
    2. You know desirable test size in % from total.
    
There're 4 charts help you to understand data and choose total sample size and test/control ratio properly.
1. SE (feature) - total sample size
2. SE (feature_test - feature_control) - test_size
3. SE (feature_test - feature_control) - total sample size
4. Min. Detected Effect (feature_test - feature_control) with alpha=0.05 - total sample size

## Contributing
---
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
---
[MIT](https://choosealicense.com/licenses/mit/)