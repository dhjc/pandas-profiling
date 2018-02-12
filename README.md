# pandas-profiling offline
Forked from original to work offline in a linux environment.  The following files need to stored in /var/cdn_local/ for this to work.

[JQuery](https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js)

[Bootstrap CSS](https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css)

[Bootstrap-theme](https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap-theme.min.css)

[Bootstrap JS](https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js)



# pandas-profiling 

Generates profile reports from a pandas `DataFrame`. The pandas `df.describe()` function is great but a little basic for serious exploratory data analysis.

For each column the following statistics - if relevant for the column type - are presented in an interactive HTML report:

* **Essentials**:  type, unique values, missing values
* **Quantile statistics** like minimum value, Q1, median, Q3, maximum, range, interquartile range
* **Descriptive statistics** like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness
* **Most frequent values**
* **Histogram**
* **Correlations** highlighting of highly correlated variables, Spearman and Pearson matrixes

## Demo

[Click here](http://nbviewer.ipython.org/github/JosPolfliet/pandas-profiling/blob/master/examples/meteorites.ipynb) to see a live demo.

## Installation

Unlike the orginal version from which this was forked, this can only be installed from source.

### From source

Download the source code by cloning the repo or by pressing 'Download ZIP' on this page. Install by navigating to the proper directory and running

    python setup.py install

## Usage

The profile report is written in HTML5 and CSS3, which means pandas-profiling requires a modern browser. 

### Jupyter Notebook (formerly IPython)

We recommend generating reports interactively by using the Jupyter notebook. 

Start by loading in your pandas DataFrame, e.g. by using
```python
import pandas as pd
import pandas_profiling

df=pd.read_csv("/myfilepath/myfile.csv", parse_dates=True, encoding='UTF-8')
```
To display the report in a Jupyter notebook, run:
```python
pandas_profiling.ProfileReport(df)
```
To retrieve the list of variables which are rejected due to high correlation:
```python
profile = pandas_profiling.ProfileReport(df)
rejected_variables = profile.get_rejected_variables(threshold=0.9)
```
If you want to generate a HTML report file, save the `ProfileReport` to an object and use the `to_file()` function:
```python
profile = pandas_profiling.ProfileReport(df)
profile.to_file(outputfile="/tmp/myoutputfile.html")
```
### Python

For standard formatted CSV files that can be read immediately by pandas, you can use the `profile_csv.py` script. Run

	python profile_csv.py -h

for information about options and arguments.

### Advanced usage

A set of options are available in order to adapt the report generated.

* `bins` (`int`): Number of bins in histogram (10 by default).
* Correlation settings:
    * `check_correlation` (`boolean`): Whether or not to check correlation (`True` by default)
    * `correlation_threshold` (`float`): Threshold to determine if the variable pair is correlated (0.9 by default).
    * `correlation_overrides` (`list`): Variable names not to be rejected because they are correlated (`None` by default).
    * `check_recoded` (`boolean`): Whether or not to check recoded correlation (`False` by default). Since it's an expensive computation it can be activated for small datasets.
* `pool_size` (`int`): Number of workers in thread pool. The default is equal to the number of CPU.

## Dependencies

* python (>= 2.7)
* pandas (>=0.19)
* matplotlib  (>=1.4)
* six (>=1.9)
