{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "\n",
    "\n",
    "<h1 align=center><font size=5>Data Analysis with Python</font></h1>\n",
    "<h1 align=center><font size=5>By BAHBAH Ibrahim</font></h1>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1>Data Wrangling</h1>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3>Welcome!</h3>\n",
    "\n",
    "By the end of this notebook, you will have learned the basics of Data Wrangling! "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Table of content</h2>\n",
    "\n",
    "<div class=\"alert alert-block alert-info\" style=\"margin-top: 20px\">\n",
    "<ul>\n",
    "    <li><a href=\"#identify_handle_missing_values\">Identify and handle missing values</a>\n",
    "        <ul>\n",
    "            <li><a href=\"#identify_missing_values\">Identify missing values</a></li>\n",
    "            <li><a href=\"#deal_missing_values\">Deal with missing values</a></li>\n",
    "            <li><a href=\"#correct_data_format\">Correct data format</a></li>\n",
    "        </ul>\n",
    "    </li>\n",
    "    <li><a href=\"#data_standardization\">Data standardization</a></li>\n",
    "    <li><a href=\"#data_normalization\">Data Normalization (centering/scaling)</a></li>\n",
    "    <li><a href=\"#binning\">Binning</a></li>\n",
    "    <li><a href=\"#indicator\">Indicator variable</a></li>\n",
    "</ul>\n",
    "    \n",
    "Estimated Time Needed: <strong>30 min</strong>\n",
    "</div>\n",
    " \n",
    "<hr>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>What is the purpose of Data Wrangling?</h2>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Data Wrangling is the process of converting data from the initial format to a format that may be better for analysis."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3>What is the fuel consumption (L/100k) rate for the diesel car?</h3>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3>Import data</h3>\n",
    "<p>\n",
    "You can find the \"Automobile Data Set\" from the following link: <a href=\"https://archive.ics.uci.edu/ml/machine-learning-databases/autos/imports-85.data\">https://archive.ics.uci.edu/ml/machine-learning-databases/autos/imports-85.data</a>. \n",
    "We will be using this data set throughout this course.\n",
    "</p>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Import pandas</h4> "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import matplotlib.pylab as plt"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Reading the data set from the URL and adding the related headers.</h2>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "URL of the dataset"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "This dataset was hosted on IBM Cloud object click <a href=\"https://cocl.us/corsera_da0101en_notebook_bottom\">HERE</a> for free storage "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "filename = \"https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/DA0101EN/auto.csv\""
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " Python list <b>headers</b> containing name of headers "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "headers = [\"symboling\",\"normalized-losses\",\"make\",\"fuel-type\",\"aspiration\", \"num-of-doors\",\"body-style\",\n",
    "         \"drive-wheels\",\"engine-location\",\"wheel-base\", \"length\",\"width\",\"height\",\"curb-weight\",\"engine-type\",\n",
    "         \"num-of-cylinders\", \"engine-size\",\"fuel-system\",\"bore\",\"stroke\",\"compression-ratio\",\"horsepower\",\n",
    "         \"peak-rpm\",\"city-mpg\",\"highway-mpg\",\"price\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Use the Pandas method <b>read_csv()</b> to load the data from the web address. Set the parameter  \"names\" equal to the Python list \"headers\"."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df = pd.read_csv(filename, names = headers)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " Use the method <b>head()</b> to display the first five rows of the dataframe. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# To see what the data set looks like, we'll use the head() method.\n",
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "As we can see, several question marks appeared in the dataframe; those are missing values which may hinder our further analysis. \n",
    "<div>So, how do we identify all those missing values and deal with them?</div> \n",
    "\n",
    "\n",
    "<b>How to work with missing data?</b>\n",
    "\n",
    "Steps for working with missing data:\n",
    "<ol>\n",
    "    <li>dentify missing data</li>\n",
    "    <li>deal with missing data</li>\n",
    "    <li>correct data format</li>\n",
    "</ol>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 id=\"identify_handle_missing_values\">Identify and handle missing values</h2>\n",
    "\n",
    "\n",
    "<h3 id=\"identify_missing_values\">Identify missing values</h3>\n",
    "<h4>Convert \"?\" to NaN</h4>\n",
    "In the car dataset, missing data comes with the question mark \"?\".\n",
    "We replace \"?\" with NaN (Not a Number), which is Python's default missing value marker, for reasons of computational speed and convenience. Here we use the function: \n",
    " <pre>.replace(A, B, inplace = True) </pre>\n",
    "to replace A by B"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "\n",
    "# replace \"?\" to NaN\n",
    "df.replace(\"?\", np.nan, inplace = True)\n",
    "df.head(5)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "dentify_missing_values\n",
    "\n",
    "<h4>Evaluating for Missing Data</h4>\n",
    "\n",
    "The missing values are converted to Python's default. We use Python's built-in functions to identify these missing values. There are two methods to detect missing data:\n",
    "<ol>\n",
    "    <li><b>.isnull()</b></li>\n",
    "    <li><b>.notnull()</b></li>\n",
    "</ol>\n",
    "The output is a boolean value indicating whether the value that is passed into the argument is in fact missing data."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "missing_data = df.isnull()\n",
    "missing_data.head(5)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "\"True\" stands for missing value, while \"False\" stands for not missing value."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Count missing values in each column</h4>\n",
    "<p>\n",
    "Using a for loop in Python, we can quickly figure out the number of missing values in each column. As mentioned above, \"True\" represents a missing value, \"False\"  means the value is present in the dataset.  In the body of the for loop the method  \".value_counts()\"  counts the number of \"True\" values. \n",
    "</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "for column in missing_data.columns.values.tolist():\n",
    "    print(column)\n",
    "    print (missing_data[column].value_counts())\n",
    "    print(\"\")    "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Based on the summary above, each column has 205 rows of data, seven columns containing missing data:\n",
    "<ol>\n",
    "    <li>\"normalized-losses\": 41 missing data</li>\n",
    "    <li>\"num-of-doors\": 2 missing data</li>\n",
    "    <li>\"bore\": 4 missing data</li>\n",
    "    <li>\"stroke\" : 4 missing data</li>\n",
    "    <li>\"horsepower\": 2 missing data</li>\n",
    "    <li>\"peak-rpm\": 2 missing data</li>\n",
    "    <li>\"price\": 4 missing data</li>\n",
    "</ol>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3 id=\"deal_missing_values\">Deal with missing data</h3>\n",
    "<b>How to deal with missing data?</b>\n",
    "\n",
    "<ol>\n",
    "    <li>drop data<br>\n",
    "        a. drop the whole row<br>\n",
    "        b. drop the whole column\n",
    "    </li>\n",
    "    <li>replace data<br>\n",
    "        a. replace it by mean<br>\n",
    "        b. replace it by frequency<br>\n",
    "        c. replace it based on other functions\n",
    "    </li>\n",
    "</ol>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Whole columns should be dropped only if most entries in the column are empty. In our dataset, none of the columns are empty enough to drop entirely.\n",
    "We have some freedom in choosing which method to replace data; however, some methods may seem more reasonable than others. We will apply each method to many different columns:\n",
    "\n",
    "<b>Replace by mean:</b>\n",
    "<ul>\n",
    "    <li>\"normalized-losses\": 41 missing data, replace them with mean</li>\n",
    "    <li>\"stroke\": 4 missing data, replace them with mean</li>\n",
    "    <li>\"bore\": 4 missing data, replace them with mean</li>\n",
    "    <li>\"horsepower\": 2 missing data, replace them with mean</li>\n",
    "    <li>\"peak-rpm\": 2 missing data, replace them with mean</li>\n",
    "</ul>\n",
    "\n",
    "<b>Replace by frequency:</b>\n",
    "<ul>\n",
    "    <li>\"num-of-doors\": 2 missing data, replace them with \"four\". \n",
    "        <ul>\n",
    "            <li>Reason: 84% sedans is four doors. Since four doors is most frequent, it is most likely to occur</li>\n",
    "        </ul>\n",
    "    </li>\n",
    "</ul>\n",
    "\n",
    "<b>Drop the whole row:</b>\n",
    "<ul>\n",
    "    <li>\"price\": 4 missing data, simply delete the whole row\n",
    "        <ul>\n",
    "            <li>Reason: price is what we want to predict. Any data entry without price data cannot be used for prediction; therefore any row now without price data is not useful to us</li>\n",
    "        </ul>\n",
    "    </li>\n",
    "</ul>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Calculate the average of the column </h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "avg_norm_loss = df[\"normalized-losses\"].astype(\"float\").mean(axis=0)\n",
    "print(\"Average of normalized-losses:\", avg_norm_loss)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Replace \"NaN\" by mean value in \"normalized-losses\" column</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "df[\"normalized-losses\"].replace(np.nan, avg_norm_loss, inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Calculate the mean value for 'bore' column</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "avg_bore=df['bore'].astype('float').mean(axis=0)\n",
    "print(\"Average of bore:\", avg_bore)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Replace NaN by mean value</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "df[\"bore\"].replace(np.nan, avg_bore, inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-danger alertdanger\" style=\"margin-top: 20px\">\n",
    "<h1> Question  #1: </h1>\n",
    "\n",
    "<b>According to the example above, replace NaN in \"stroke\" column by mean.</b>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# Write your code below and press Shift+Enter to execute \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click <b>here</b> for the solution.\n",
    "\n",
    "<!-- The answer is below:\n",
    "\n",
    "# calculate the mean vaule for \"stroke\" column\n",
    "avg_stroke = df[\"stroke\"].astype(\"float\").mean(axis = 0)\n",
    "print(\"Average of stroke:\", avg_stroke)\n",
    "\n",
    "# replace NaN by mean value in \"stroke\" column\n",
    "df[\"stroke\"].replace(np.nan, avg_stroke, inplace = True)\n",
    "\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Calculate the mean value for the  'horsepower' column:</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "avg_horsepower = df['horsepower'].astype('float').mean(axis=0)\n",
    "print(\"Average horsepower:\", avg_horsepower)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Replace \"NaN\" by mean value:</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "df['horsepower'].replace(np.nan, avg_horsepower, inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Calculate the mean value for 'peak-rpm' column:</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "avg_peakrpm=df['peak-rpm'].astype('float').mean(axis=0)\n",
    "print(\"Average peak rpm:\", avg_peakrpm)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Replace NaN by mean value:</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "df['peak-rpm'].replace(np.nan, avg_peakrpm, inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "To see which values are present in a particular column, we can use the \".value_counts()\" method:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df['num-of-doors'].value_counts()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can see that four doors are the most common type. We can also use the \".idxmax()\" method to calculate for us the most common type automatically:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df['num-of-doors'].value_counts().idxmax()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The replacement procedure is very similar to what we have seen previously"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "#replace the missing 'num-of-doors' values by the most frequent \n",
    "df[\"num-of-doors\"].replace(np.nan, \"four\", inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Finally, let's drop all rows that do not have price data:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "# simply drop whole row with NaN in \"price\" column\n",
    "df.dropna(subset=[\"price\"], axis=0, inplace=True)\n",
    "\n",
    "# reset index, because we droped two rows\n",
    "df.reset_index(drop=True, inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Good!</b> Now, we obtain the dataset with no missing values."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3 id=\"correct_data_format\">Correct data format</h3>\n",
    "<b>We are almost there!</b>\n",
    "<p>The last step in data cleaning is checking and making sure that all data is in the correct format (int, float, text or other).</p>\n",
    "\n",
    "In Pandas, we use \n",
    "<p><b>.dtype()</b> to check the data type</p>\n",
    "<p><b>.astype()</b> to change the data type</p>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Lets list the data types for each column</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df.dtypes"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p>As we can see above, some columns are not of the correct data type. Numerical variables should have type 'float' or 'int', and variables with strings such as categories should have type 'object'. For example, 'bore' and 'stroke' variables are numerical values that describe the engines, so we should expect them to be of the type 'float' or 'int'; however, they are shown as type 'object'. We have to convert data types into a proper format for each column using the \"astype()\" method.</p> "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Convert data types to proper format</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df[[\"bore\", \"stroke\"]] = df[[\"bore\", \"stroke\"]].astype(\"float\")\n",
    "df[[\"normalized-losses\"]] = df[[\"normalized-losses\"]].astype(\"int\")\n",
    "df[[\"price\"]] = df[[\"price\"]].astype(\"float\")\n",
    "df[[\"peak-rpm\"]] = df[[\"peak-rpm\"]].astype(\"float\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h4>Let us list the columns after the conversion</h4>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df.dtypes"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Wonderful!</b>\n",
    "\n",
    "Now, we finally obtain the cleaned dataset with no missing values and all data in its proper format."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 id=\"data_standardization\">Data Standardization</h2>\n",
    "<p>\n",
    "Data is usually collected from different agencies with different formats.\n",
    "(Data Standardization is also a term for a particular type of data normalization, where we subtract the mean and divide by the standard deviation)\n",
    "</p>\n",
    "    \n",
    "<b>What is Standardization?</b>\n",
    "<p>Standardization is the process of transforming data into a common format which allows the researcher to make the meaningful comparison.\n",
    "</p>\n",
    "\n",
    "<b>Example</b>\n",
    "<p>Transform mpg to L/100km:</p>\n",
    "<p>In our dataset, the fuel consumption columns \"city-mpg\" and \"highway-mpg\" are represented by mpg (miles per gallon) unit. Assume we are developing an application in a country that accept the fuel consumption with L/100km standard</p>\n",
    "<p>We will need to apply <b>data transformation</b> to transform mpg into L/100km?</p>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p>The formula for unit conversion is<p>\n",
    "L/100km = 235 / mpg\n",
    "<p>We can do many mathematical operations directly in Pandas.</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# Convert mpg to L/100km by mathematical operation (235 divided by mpg)\n",
    "df['city-L/100km'] = 235/df[\"city-mpg\"]\n",
    "\n",
    "# check your transformed data \n",
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-danger alertdanger\" style=\"margin-top: 20px\">\n",
    "<h1> Question  #2: </h1>\n",
    "\n",
    "<b>According to the example above, transform mpg to L/100km in the column of \"highway-mpg\", and change the name of column to \"highway-L/100km\".</b>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# Write your code below and press Shift+Enter to execute \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click <b>here</b> for the solution.\n",
    "\n",
    "<!-- The answer is below:\n",
    "\n",
    "# transform mpg to L/100km by mathematical operation (235 divided by mpg)\n",
    "df[\"highway-mpg\"] = 235/df[\"highway-mpg\"]\n",
    "\n",
    "# rename column name from \"highway-mpg\" to \"highway-L/100km\"\n",
    "df.rename(columns={'\"highway-mpg\"':'highway-L/100km'}, inplace=True)\n",
    "\n",
    "# check your transformed data \n",
    "df.head()\n",
    "\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 id=\"data_normalization\">Data Normalization</h2>\n",
    "\n",
    "<b>Why normalization?</b>\n",
    "<p>Normalization is the process of transforming values of several variables into a similar range. Typical normalizations include scaling the variable so the variable average is 0, scaling the variable so the variance is 1, or scaling variable so the variable values range from 0 to 1\n",
    "</p>\n",
    "\n",
    "<b>Example</b>\n",
    "<p>To demonstrate normalization, let's say we want to scale the columns \"length\", \"width\" and \"height\" </p>\n",
    "<p><b>Target:</b>would like to Normalize those variables so their value ranges from 0 to 1.</p>\n",
    "<p><b>Approach:</b> replace original value by (original value)/(maximum value)</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# replace (original value) by (original value)/(maximum value)\n",
    "df['length'] = df['length']/df['length'].max()\n",
    "df['width'] = df['width']/df['width'].max()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-danger alertdanger\" style=\"margin-top: 20px\">\n",
    "<h1> Questiont #3: </h1>\n",
    "\n",
    "<b>According to the example above, normalize the column \"height\".</b>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# Write your code below and press Shift+Enter to execute \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click <b>here</b> for the solution.\n",
    "\n",
    "<!-- The answer is below:\n",
    "\n",
    "df['height'] = df['height']/df['height'].max() \n",
    "# show the scaled columns\n",
    "df[[\"length\",\"width\",\"height\"]].head()\n",
    "\n",
    "-->"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Here we can see, we've normalized \"length\", \"width\" and \"height\" in the range of [0,1]."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 id=\"binning\">Binning</h2>\n",
    "<b>Why binning?</b>\n",
    "<p>\n",
    "    Binning is a process of transforming continuous numerical variables into discrete categorical 'bins', for grouped analysis.\n",
    "</p>\n",
    "\n",
    "<b>Example: </b>\n",
    "<p>In our dataset, \"horsepower\" is a real valued variable ranging from 48 to 288, it has 57 unique values. What if we only care about the price difference between cars with high horsepower, medium horsepower, and little horsepower (3 types)? Can we rearrange them into three ‘bins' to simplify analysis? </p>\n",
    "\n",
    "<p>We will use the Pandas method 'cut' to segment the 'horsepower' column into 3 bins </p>\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3>Example of Binning Data In Pandas</h3>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " Convert data to correct format "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df[\"horsepower\"]=df[\"horsepower\"].astype(int, copy=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Lets plot the histogram of horspower, to see what the distribution of horsepower looks like."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "%matplotlib inline\n",
    "import matplotlib as plt\n",
    "from matplotlib import pyplot\n",
    "plt.pyplot.hist(df[\"horsepower\"])\n",
    "\n",
    "# set x/y labels and plot title\n",
    "plt.pyplot.xlabel(\"horsepower\")\n",
    "plt.pyplot.ylabel(\"count\")\n",
    "plt.pyplot.title(\"horsepower bins\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p>We would like 3 bins of equal size bandwidth so we use numpy's <code>linspace(start_value, end_value, numbers_generated</code> function.</p>\n",
    "<p>Since we want to include the minimum value of horsepower we want to set start_value=min(df[\"horsepower\"]).</p>\n",
    "<p>Since we want to include the maximum value of horsepower we want to set end_value=max(df[\"horsepower\"]).</p>\n",
    "<p>Since we are building 3 bins of equal length, there should be 4 dividers, so numbers_generated=4.</p>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We build a bin array, with a minimum value to a maximum value, with bandwidth calculated above. The bins will be values used to determine when one bin ends and another begins."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "bins = np.linspace(min(df[\"horsepower\"]), max(df[\"horsepower\"]), 4)\n",
    "bins"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " We set group  names:"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "group_names = ['Low', 'Medium', 'High']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " We apply the function \"cut\" the determine what each value of \"df['horsepower']\" belongs to. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df['horsepower-binned'] = pd.cut(df['horsepower'], bins, labels=group_names, include_lowest=True )\n",
    "df[['horsepower','horsepower-binned']].head(20)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Lets see the number of vehicles in each bin."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "df[\"horsepower-binned\"].value_counts()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Lets plot the distribution of each bin."
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {},
   "outputs": [],
   "source": [
    "%matplotlib inline\n",
    "import matplotlib as plt\n",
    "from matplotlib import pyplot\n",
    "pyplot.bar(group_names, df[\"horsepower-binned\"].value_counts())\n",
    "\n",
    "# set x/y labels and plot title\n",
    "plt.pyplot.xlabel(\"horsepower\")\n",
    "plt.pyplot.ylabel(\"count\")\n",
    "plt.pyplot.title(\"horsepower bins\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<p>\n",
    "    Check the dataframe above carefully, you will find the last column provides the bins for \"horsepower\" with 3 categories (\"Low\",\"Medium\" and \"High\"). \n",
    "</p>\n",
    "<p>\n",
    "    We successfully narrow the intervals from 57 to 3!\n",
    "</p>"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h3>Bins visualization</h3>\n",
    "Normally, a histogram is used to visualize the distribution of bins we created above. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "%matplotlib inline\n",
    "import matplotlib as plt\n",
    "from matplotlib import pyplot\n",
    "\n",
    "a = (0,1,2)\n",
    "\n",
    "# draw historgram of attribute \"horsepower\" with bins = 3\n",
    "plt.pyplot.hist(df[\"horsepower\"], bins = 3)\n",
    "\n",
    "# set x/y labels and plot title\n",
    "plt.pyplot.xlabel(\"horsepower\")\n",
    "plt.pyplot.ylabel(\"count\")\n",
    "plt.pyplot.title(\"horsepower bins\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The plot above shows the binning result for attribute \"horsepower\". "
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2 id=\"indicator\">Indicator variable (or dummy variable)</h2>\n",
    "<b>What is an indicator variable?</b>\n",
    "<p>\n",
    "    An indicator variable (or dummy variable) is a numerical variable used to label categories. They are called 'dummies' because the numbers themselves don't have inherent meaning. \n",
    "</p>\n",
    "\n",
    "<b>Why we use indicator variables?</b>\n",
    "<p>\n",
    "    So we can use categorical variables for regression analysis in the later modules.\n",
    "</p>\n",
    "<b>Example</b>\n",
    "<p>\n",
    "    We see the column \"fuel-type\" has two unique values, \"gas\" or \"diesel\". Regression doesn't understand words, only numbers. To use this attribute in regression analysis, we convert \"fuel-type\" into indicator variables.\n",
    "</p>\n",
    "\n",
    "<p>\n",
    "    We will use the panda's method 'get_dummies' to assign numerical values to different categories of fuel type. \n",
    "</p>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df.columns"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "get indicator variables and assign it to data frame \"dummy_variable_1\" "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "dummy_variable_1 = pd.get_dummies(df[\"fuel-type\"])\n",
    "dummy_variable_1.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "change column names for clarity "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "dummy_variable_1.rename(columns={'fuel-type-diesel':'gas', 'fuel-type-diesel':'diesel'}, inplace=True)\n",
    "dummy_variable_1.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We now have the value 0 to represent \"gas\" and 1 to represent \"diesel\" in the column \"fuel-type\". We will now insert this column back into our original dataset. "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "# merge data frame \"df\" and \"dummy_variable_1\" \n",
    "df = pd.concat([df, dummy_variable_1], axis=1)\n",
    "\n",
    "# drop original column \"fuel-type\" from \"df\"\n",
    "df.drop(\"fuel-type\", axis = 1, inplace=True)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The last two columns are now the indicator variable representation of the fuel-type variable. It's all 0s and 1s now."
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div class=\"alert alert-danger alertdanger\" style=\"margin-top: 20px\">\n",
    "<h1> Question  #4: </h1>\n",
    "\n",
    "<b>As above, create indicator variable to the column of \"aspiration\": \"std\" to 0, while \"turbo\" to 1.</b>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# Write your code below and press Shift+Enter to execute \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click <b>here</b> for the solution.\n",
    "\n",
    "<!-- The answer is below:\n",
    "\n",
    "# get indicator variables of aspiration and assign it to data frame \"dummy_variable_2\"\n",
    "dummy_variable_2 = pd.get_dummies(df['aspiration'])\n",
    "\n",
    "# change column names for clarity\n",
    "dummy_variable_2.rename(columns={'std':'aspiration-std', 'turbo': 'aspiration-turbo'}, inplace=True)\n",
    "\n",
    "# show first 5 instances of data frame \"dummy_variable_1\"\n",
    "dummy_variable_2.head()\n",
    "\n",
    "-->"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    " <div class=\"alert alert-danger alertdanger\" style=\"margin-top: 20px\">\n",
    "<h1> Question  #5: </h1>\n",
    "\n",
    "<b>Merge the new dataframe to the original dataframe then drop the column 'aspiration'</b>\n",
    "</div>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": false,
    "jupyter": {
     "outputs_hidden": false
    }
   },
   "outputs": [],
   "source": [
    "# Write your code below and press Shift+Enter to execute \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click <b>here</b> for the solution.\n",
    "\n",
    "<!-- The answer is below:\n",
    "\n",
    "#merge the new dataframe to the original datafram\n",
    "df = pd.concat([df, dummy_variable_2], axis=1)\n",
    "\n",
    "# drop original column \"aspiration\" from \"df\"\n",
    "df.drop('aspiration', axis = 1, inplace=True)\n",
    "\n",
    "-->"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "save the new csv "
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true,
    "jupyter": {
     "outputs_hidden": true
    }
   },
   "outputs": [],
   "source": [
    "df.to_csv('clean_df.csv')"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1>Thank you for completing this notebook</h1>"
   ]
  }
 ],
 "metadata": {
  "anaconda-cloud": {},
  "kernelspec": {
   "display_name": "Python",
   "language": "python",
   "name": "conda-env-python-py"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.7"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
