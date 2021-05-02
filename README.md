# Linear_Regression
{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "name": "linear-regression.ipynb",
      "provenance": [],
      "collapsed_sections": []
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "WSAvvETI052N",
        "colab_type": "text"
      },
      "source": [
        "# **Build Linear Regression Model in Python**\n",
        "\n",
        "Chanin Nantasenamat\n",
        "\n",
        "[*'Data Professor' YouTube channel*](http://youtube.com/dataprofessor)\n",
        "\n",
        "In this Jupyter notebook, I will be showing you how to build a linear regression model in Python using the scikit-learn package.\n",
        "\n",
        "Inspired by [scikit-learn's Linear Regression Example](https://scikit-learn.org/stable/auto_examples/linear_model/plot_ols.html)\n",
        "\n",
        "---"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "AdN_S7JylQDW",
        "colab_type": "text"
      },
      "source": [
        "## **Load the Diabetes dataset** (via scikit-learn)"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "f3Fi9yx3lfWn",
        "colab_type": "text"
      },
      "source": [
        "### **Import library**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "0m-6K7IJlc2H",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "from sklearn import datasets"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "DXvpHcyHlh9m",
        "colab_type": "text"
      },
      "source": [
        "### **Load dataset**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "fTNc6-A87v0-",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "diabetes = datasets.load_diabetes()"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Vtp3Gq2K89SW",
        "colab_type": "code",
        "outputId": "a02f258c-29d0-48ee-fac5-9eece299a2aa",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 1000
        }
      },
      "source": [
        "diabetes"
      ],
      "execution_count": 3,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "{'DESCR': '.. _diabetes_dataset:\\n\\nDiabetes dataset\\n----------------\\n\\nTen baseline variables, age, sex, body mass index, average blood\\npressure, and six blood serum measurements were obtained for each of n =\\n442 diabetes patients, as well as the response of interest, a\\nquantitative measure of disease progression one year after baseline.\\n\\n**Data Set Characteristics:**\\n\\n  :Number of Instances: 442\\n\\n  :Number of Attributes: First 10 columns are numeric predictive values\\n\\n  :Target: Column 11 is a quantitative measure of disease progression one year after baseline\\n\\n  :Attribute Information:\\n      - Age\\n      - Sex\\n      - Body mass index\\n      - Average blood pressure\\n      - S1\\n      - S2\\n      - S3\\n      - S4\\n      - S5\\n      - S6\\n\\nNote: Each of these 10 feature variables have been mean centered and scaled by the standard deviation times `n_samples` (i.e. the sum of squares of each column totals 1).\\n\\nSource URL:\\nhttps://www4.stat.ncsu.edu/~boos/var.select/diabetes.html\\n\\nFor more information see:\\nBradley Efron, Trevor Hastie, Iain Johnstone and Robert Tibshirani (2004) \"Least Angle Regression,\" Annals of Statistics (with discussion), 407-499.\\n(https://web.stanford.edu/~hastie/Papers/LARS/LeastAngle_2002.pdf)',\n",
              " 'data': array([[ 0.03807591,  0.05068012,  0.06169621, ..., -0.00259226,\n",
              "          0.01990842, -0.01764613],\n",
              "        [-0.00188202, -0.04464164, -0.05147406, ..., -0.03949338,\n",
              "         -0.06832974, -0.09220405],\n",
              "        [ 0.08529891,  0.05068012,  0.04445121, ..., -0.00259226,\n",
              "          0.00286377, -0.02593034],\n",
              "        ...,\n",
              "        [ 0.04170844,  0.05068012, -0.01590626, ..., -0.01107952,\n",
              "         -0.04687948,  0.01549073],\n",
              "        [-0.04547248, -0.04464164,  0.03906215, ...,  0.02655962,\n",
              "          0.04452837, -0.02593034],\n",
              "        [-0.04547248, -0.04464164, -0.0730303 , ..., -0.03949338,\n",
              "         -0.00421986,  0.00306441]]),\n",
              " 'data_filename': '/usr/local/lib/python3.6/dist-packages/sklearn/datasets/data/diabetes_data.csv.gz',\n",
              " 'feature_names': ['age',\n",
              "  'sex',\n",
              "  'bmi',\n",
              "  'bp',\n",
              "  's1',\n",
              "  's2',\n",
              "  's3',\n",
              "  's4',\n",
              "  's5',\n",
              "  's6'],\n",
              " 'target': array([151.,  75., 141., 206., 135.,  97., 138.,  63., 110., 310., 101.,\n",
              "         69., 179., 185., 118., 171., 166., 144.,  97., 168.,  68.,  49.,\n",
              "         68., 245., 184., 202., 137.,  85., 131., 283., 129.,  59., 341.,\n",
              "         87.,  65., 102., 265., 276., 252.,  90., 100.,  55.,  61.,  92.,\n",
              "        259.,  53., 190., 142.,  75., 142., 155., 225.,  59., 104., 182.,\n",
              "        128.,  52.,  37., 170., 170.,  61., 144.,  52., 128.,  71., 163.,\n",
              "        150.,  97., 160., 178.,  48., 270., 202., 111.,  85.,  42., 170.,\n",
              "        200., 252., 113., 143.,  51.,  52., 210.,  65., 141.,  55., 134.,\n",
              "         42., 111.,  98., 164.,  48.,  96.,  90., 162., 150., 279.,  92.,\n",
              "         83., 128., 102., 302., 198.,  95.,  53., 134., 144., 232.,  81.,\n",
              "        104.,  59., 246., 297., 258., 229., 275., 281., 179., 200., 200.,\n",
              "        173., 180.,  84., 121., 161.,  99., 109., 115., 268., 274., 158.,\n",
              "        107.,  83., 103., 272.,  85., 280., 336., 281., 118., 317., 235.,\n",
              "         60., 174., 259., 178., 128.,  96., 126., 288.,  88., 292.,  71.,\n",
              "        197., 186.,  25.,  84.,  96., 195.,  53., 217., 172., 131., 214.,\n",
              "         59.,  70., 220., 268., 152.,  47.,  74., 295., 101., 151., 127.,\n",
              "        237., 225.,  81., 151., 107.,  64., 138., 185., 265., 101., 137.,\n",
              "        143., 141.,  79., 292., 178.,  91., 116.,  86., 122.,  72., 129.,\n",
              "        142.,  90., 158.,  39., 196., 222., 277.,  99., 196., 202., 155.,\n",
              "         77., 191.,  70.,  73.,  49.,  65., 263., 248., 296., 214., 185.,\n",
              "         78.,  93., 252., 150.,  77., 208.,  77., 108., 160.,  53., 220.,\n",
              "        154., 259.,  90., 246., 124.,  67.,  72., 257., 262., 275., 177.,\n",
              "         71.,  47., 187., 125.,  78.,  51., 258., 215., 303., 243.,  91.,\n",
              "        150., 310., 153., 346.,  63.,  89.,  50.,  39., 103., 308., 116.,\n",
              "        145.,  74.,  45., 115., 264.,  87., 202., 127., 182., 241.,  66.,\n",
              "         94., 283.,  64., 102., 200., 265.,  94., 230., 181., 156., 233.,\n",
              "         60., 219.,  80.,  68., 332., 248.,  84., 200.,  55.,  85.,  89.,\n",
              "         31., 129.,  83., 275.,  65., 198., 236., 253., 124.,  44., 172.,\n",
              "        114., 142., 109., 180., 144., 163., 147.,  97., 220., 190., 109.,\n",
              "        191., 122., 230., 242., 248., 249., 192., 131., 237.,  78., 135.,\n",
              "        244., 199., 270., 164.,  72.,  96., 306.,  91., 214.,  95., 216.,\n",
              "        263., 178., 113., 200., 139., 139.,  88., 148.,  88., 243.,  71.,\n",
              "         77., 109., 272.,  60.,  54., 221.,  90., 311., 281., 182., 321.,\n",
              "         58., 262., 206., 233., 242., 123., 167.,  63., 197.,  71., 168.,\n",
              "        140., 217., 121., 235., 245.,  40.,  52., 104., 132.,  88.,  69.,\n",
              "        219.,  72., 201., 110.,  51., 277.,  63., 118.,  69., 273., 258.,\n",
              "         43., 198., 242., 232., 175.,  93., 168., 275., 293., 281.,  72.,\n",
              "        140., 189., 181., 209., 136., 261., 113., 131., 174., 257.,  55.,\n",
              "         84.,  42., 146., 212., 233.,  91., 111., 152., 120.,  67., 310.,\n",
              "         94., 183.,  66., 173.,  72.,  49.,  64.,  48., 178., 104., 132.,\n",
              "        220.,  57.]),\n",
              " 'target_filename': '/usr/local/lib/python3.6/dist-packages/sklearn/datasets/data/diabetes_target.csv.gz'}"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 3
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "7XNtaeRS8roJ",
        "colab_type": "text"
      },
      "source": [
        "### **Description of the Diabetes dataset**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "tkRC3-5m8aW2",
        "colab_type": "code",
        "outputId": "acf58987-ad54-488c-90f3-0fc1beb27bae",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 663
        }
      },
      "source": [
        "print(diabetes.DESCR)"
      ],
      "execution_count": 4,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            ".. _diabetes_dataset:\n",
            "\n",
            "Diabetes dataset\n",
            "----------------\n",
            "\n",
            "Ten baseline variables, age, sex, body mass index, average blood\n",
            "pressure, and six blood serum measurements were obtained for each of n =\n",
            "442 diabetes patients, as well as the response of interest, a\n",
            "quantitative measure of disease progression one year after baseline.\n",
            "\n",
            "**Data Set Characteristics:**\n",
            "\n",
            "  :Number of Instances: 442\n",
            "\n",
            "  :Number of Attributes: First 10 columns are numeric predictive values\n",
            "\n",
            "  :Target: Column 11 is a quantitative measure of disease progression one year after baseline\n",
            "\n",
            "  :Attribute Information:\n",
            "      - Age\n",
            "      - Sex\n",
            "      - Body mass index\n",
            "      - Average blood pressure\n",
            "      - S1\n",
            "      - S2\n",
            "      - S3\n",
            "      - S4\n",
            "      - S5\n",
            "      - S6\n",
            "\n",
            "Note: Each of these 10 feature variables have been mean centered and scaled by the standard deviation times `n_samples` (i.e. the sum of squares of each column totals 1).\n",
            "\n",
            "Source URL:\n",
            "https://www4.stat.ncsu.edu/~boos/var.select/diabetes.html\n",
            "\n",
            "For more information see:\n",
            "Bradley Efron, Trevor Hastie, Iain Johnstone and Robert Tibshirani (2004) \"Least Angle Regression,\" Annals of Statistics (with discussion), 407-499.\n",
            "(https://web.stanford.edu/~hastie/Papers/LARS/LeastAngle_2002.pdf)\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "HtlSG5M187YC",
        "colab_type": "text"
      },
      "source": [
        "### **Feature names**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "GMeRYgLK8xjS",
        "colab_type": "code",
        "outputId": "09f4212e-b9be-4458-a9ee-fb4dea5a77c4",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "print(diabetes.feature_names)"
      ],
      "execution_count": 5,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "['age', 'sex', 'bmi', 'bp', 's1', 's2', 's3', 's4', 's5', 's6']\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "v_EPpc7U9fjN",
        "colab_type": "text"
      },
      "source": [
        "### **Create X and Y data matrices**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "m66XE7uA9tEk",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "X = diabetes.data\n",
        "Y = diabetes.target"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "0ZHtE-if93Vw",
        "colab_type": "code",
        "outputId": "8a293299-cbab-47e3-880c-cd15108ac70f",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "X.shape, Y.shape"
      ],
      "execution_count": 7,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "((442, 10), (442,))"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 7
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "Ng_Jpsqh9tZK",
        "colab_type": "text"
      },
      "source": [
        "### **Load dataset + Create X and Y data matrices (in 1 step)**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "HHYgXzyvjY-V",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "X, Y = datasets.load_diabetes(return_X_y=True)"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "3pjWOP3E-ioq",
        "colab_type": "code",
        "outputId": "032a2a0e-6e25-45f4-a379-f191d663eb39",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "X.shape, Y.shape"
      ],
      "execution_count": 9,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "((442, 10), (442,))"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 9
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ebyXGC8S2kgV",
        "colab_type": "text"
      },
      "source": [
        "## **Load the Boston Housing dataset (via GitHub)**\n",
        "\n",
        "The Boston Housing dataset was obtained from the mlbench R package, which was loaded using the following commands:\n",
        "\n",
        "```\n",
        "library(mlbench)\n",
        "data(BostonHousing)\n",
        "```\n",
        "\n",
        "For your convenience, I have also shared the [Boston Housing dataset](https://github.com/dataprofessor/data/blob/master/BostonHousing.csv) on the Data Professor GitHub package."
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "TmsgVFU56LbU",
        "colab_type": "text"
      },
      "source": [
        "### **Import library**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "l-vSjx5O6G6M",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "import pandas as pd"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "eXQDM3856Rzy",
        "colab_type": "text"
      },
      "source": [
        "### **Download CSV from GitHub**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "nC8pBDOB2jI8",
        "colab_type": "code",
        "outputId": "60dfd2e4-f1b2-49fc-a360-6f7b1c1d82a3",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 289
        }
      },
      "source": [
        "! wget https://github.com/dataprofessor/data/raw/master/BostonHousing.csv"
      ],
      "execution_count": 11,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "--2020-03-30 07:43:30--  https://github.com/dataprofessor/data/raw/master/BostonHousing.csv\n",
            "Resolving github.com (github.com)... 140.82.112.3\n",
            "Connecting to github.com (github.com)|140.82.112.3|:443... connected.\n",
            "HTTP request sent, awaiting response... 302 Found\n",
            "Location: https://raw.githubusercontent.com/dataprofessor/data/master/BostonHousing.csv [following]\n",
            "--2020-03-30 07:43:36--  https://raw.githubusercontent.com/dataprofessor/data/master/BostonHousing.csv\n",
            "Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.0.133, 151.101.64.133, 151.101.128.133, ...\n",
            "Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|151.101.0.133|:443... connected.\n",
            "HTTP request sent, awaiting response... 200 OK\n",
            "Length: 36242 (35K) [text/plain]\n",
            "Saving to: ‘BostonHousing.csv’\n",
            "\n",
            "BostonHousing.csv   100%[===================>]  35.39K  --.-KB/s    in 0.03s   \n",
            "\n",
            "2020-03-30 07:43:37 (1.25 MB/s) - ‘BostonHousing.csv’ saved [36242/36242]\n",
            "\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "nwEA8kjK6Ypj",
        "colab_type": "text"
      },
      "source": [
        "### **Read in CSV file**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "TI8bfUX05_mp",
        "colab_type": "code",
        "outputId": "6254aadb-a19f-45dc-bb44-e5ab8aec2529",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 419
        }
      },
      "source": [
        "BostonHousing = pd.read_csv(\"BostonHousing.csv\")\n",
        "BostonHousing"
      ],
      "execution_count": 12,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>crim</th>\n",
              "      <th>zn</th>\n",
              "      <th>indus</th>\n",
              "      <th>chas</th>\n",
              "      <th>nox</th>\n",
              "      <th>rm</th>\n",
              "      <th>age</th>\n",
              "      <th>dis</th>\n",
              "      <th>rad</th>\n",
              "      <th>tax</th>\n",
              "      <th>ptratio</th>\n",
              "      <th>b</th>\n",
              "      <th>lstat</th>\n",
              "      <th>medv</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>0.00632</td>\n",
              "      <td>18.0</td>\n",
              "      <td>2.31</td>\n",
              "      <td>0</td>\n",
              "      <td>0.538</td>\n",
              "      <td>6.575</td>\n",
              "      <td>65.2</td>\n",
              "      <td>4.0900</td>\n",
              "      <td>1</td>\n",
              "      <td>296</td>\n",
              "      <td>15.3</td>\n",
              "      <td>396.90</td>\n",
              "      <td>4.98</td>\n",
              "      <td>24.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>0.02731</td>\n",
              "      <td>0.0</td>\n",
              "      <td>7.07</td>\n",
              "      <td>0</td>\n",
              "      <td>0.469</td>\n",
              "      <td>6.421</td>\n",
              "      <td>78.9</td>\n",
              "      <td>4.9671</td>\n",
              "      <td>2</td>\n",
              "      <td>242</td>\n",
              "      <td>17.8</td>\n",
              "      <td>396.90</td>\n",
              "      <td>9.14</td>\n",
              "      <td>21.6</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>0.02729</td>\n",
              "      <td>0.0</td>\n",
              "      <td>7.07</td>\n",
              "      <td>0</td>\n",
              "      <td>0.469</td>\n",
              "      <td>7.185</td>\n",
              "      <td>61.1</td>\n",
              "      <td>4.9671</td>\n",
              "      <td>2</td>\n",
              "      <td>242</td>\n",
              "      <td>17.8</td>\n",
              "      <td>392.83</td>\n",
              "      <td>4.03</td>\n",
              "      <td>34.7</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>0.03237</td>\n",
              "      <td>0.0</td>\n",
              "      <td>2.18</td>\n",
              "      <td>0</td>\n",
              "      <td>0.458</td>\n",
              "      <td>6.998</td>\n",
              "      <td>45.8</td>\n",
              "      <td>6.0622</td>\n",
              "      <td>3</td>\n",
              "      <td>222</td>\n",
              "      <td>18.7</td>\n",
              "      <td>394.63</td>\n",
              "      <td>2.94</td>\n",
              "      <td>33.4</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>0.06905</td>\n",
              "      <td>0.0</td>\n",
              "      <td>2.18</td>\n",
              "      <td>0</td>\n",
              "      <td>0.458</td>\n",
              "      <td>7.147</td>\n",
              "      <td>54.2</td>\n",
              "      <td>6.0622</td>\n",
              "      <td>3</td>\n",
              "      <td>222</td>\n",
              "      <td>18.7</td>\n",
              "      <td>396.90</td>\n",
              "      <td>5.33</td>\n",
              "      <td>36.2</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>501</th>\n",
              "      <td>0.06263</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.593</td>\n",
              "      <td>69.1</td>\n",
              "      <td>2.4786</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>391.99</td>\n",
              "      <td>9.67</td>\n",
              "      <td>22.4</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>502</th>\n",
              "      <td>0.04527</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.120</td>\n",
              "      <td>76.7</td>\n",
              "      <td>2.2875</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>396.90</td>\n",
              "      <td>9.08</td>\n",
              "      <td>20.6</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>503</th>\n",
              "      <td>0.06076</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.976</td>\n",
              "      <td>91.0</td>\n",
              "      <td>2.1675</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>396.90</td>\n",
              "      <td>5.64</td>\n",
              "      <td>23.9</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>504</th>\n",
              "      <td>0.10959</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.794</td>\n",
              "      <td>89.3</td>\n",
              "      <td>2.3889</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>393.45</td>\n",
              "      <td>6.48</td>\n",
              "      <td>22.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>505</th>\n",
              "      <td>0.04741</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.030</td>\n",
              "      <td>80.8</td>\n",
              "      <td>2.5050</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>396.90</td>\n",
              "      <td>7.88</td>\n",
              "      <td>11.9</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>506 rows × 14 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "        crim    zn  indus  chas    nox  ...  tax  ptratio       b  lstat  medv\n",
              "0    0.00632  18.0   2.31     0  0.538  ...  296     15.3  396.90   4.98  24.0\n",
              "1    0.02731   0.0   7.07     0  0.469  ...  242     17.8  396.90   9.14  21.6\n",
              "2    0.02729   0.0   7.07     0  0.469  ...  242     17.8  392.83   4.03  34.7\n",
              "3    0.03237   0.0   2.18     0  0.458  ...  222     18.7  394.63   2.94  33.4\n",
              "4    0.06905   0.0   2.18     0  0.458  ...  222     18.7  396.90   5.33  36.2\n",
              "..       ...   ...    ...   ...    ...  ...  ...      ...     ...    ...   ...\n",
              "501  0.06263   0.0  11.93     0  0.573  ...  273     21.0  391.99   9.67  22.4\n",
              "502  0.04527   0.0  11.93     0  0.573  ...  273     21.0  396.90   9.08  20.6\n",
              "503  0.06076   0.0  11.93     0  0.573  ...  273     21.0  396.90   5.64  23.9\n",
              "504  0.10959   0.0  11.93     0  0.573  ...  273     21.0  393.45   6.48  22.0\n",
              "505  0.04741   0.0  11.93     0  0.573  ...  273     21.0  396.90   7.88  11.9\n",
              "\n",
              "[506 rows x 14 columns]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 12
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "60JWEmpn6zQJ",
        "colab_type": "text"
      },
      "source": [
        "### **Split dataset to X and Y variables**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "nGYLRa3x64Q_",
        "colab_type": "code",
        "outputId": "a9b6c348-7230-4bee-ed13-21a3d5a060d8",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 221
        }
      },
      "source": [
        "Y = BostonHousing.medv\n",
        "Y"
      ],
      "execution_count": 13,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0      24.0\n",
              "1      21.6\n",
              "2      34.7\n",
              "3      33.4\n",
              "4      36.2\n",
              "       ... \n",
              "501    22.4\n",
              "502    20.6\n",
              "503    23.9\n",
              "504    22.0\n",
              "505    11.9\n",
              "Name: medv, Length: 506, dtype: float64"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 13
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "RnvhPzaQ933W",
        "colab_type": "code",
        "outputId": "f29df657-5abf-4049-e944-19465a96af6a",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 419
        }
      },
      "source": [
        "X = BostonHousing.drop(['medv'], axis=1)\n",
        "X"
      ],
      "execution_count": 14,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>crim</th>\n",
              "      <th>zn</th>\n",
              "      <th>indus</th>\n",
              "      <th>chas</th>\n",
              "      <th>nox</th>\n",
              "      <th>rm</th>\n",
              "      <th>age</th>\n",
              "      <th>dis</th>\n",
              "      <th>rad</th>\n",
              "      <th>tax</th>\n",
              "      <th>ptratio</th>\n",
              "      <th>b</th>\n",
              "      <th>lstat</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>0.00632</td>\n",
              "      <td>18.0</td>\n",
              "      <td>2.31</td>\n",
              "      <td>0</td>\n",
              "      <td>0.538</td>\n",
              "      <td>6.575</td>\n",
              "      <td>65.2</td>\n",
              "      <td>4.0900</td>\n",
              "      <td>1</td>\n",
              "      <td>296</td>\n",
              "      <td>15.3</td>\n",
              "      <td>396.90</td>\n",
              "      <td>4.98</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>0.02731</td>\n",
              "      <td>0.0</td>\n",
              "      <td>7.07</td>\n",
              "      <td>0</td>\n",
              "      <td>0.469</td>\n",
              "      <td>6.421</td>\n",
              "      <td>78.9</td>\n",
              "      <td>4.9671</td>\n",
              "      <td>2</td>\n",
              "      <td>242</td>\n",
              "      <td>17.8</td>\n",
              "      <td>396.90</td>\n",
              "      <td>9.14</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>0.02729</td>\n",
              "      <td>0.0</td>\n",
              "      <td>7.07</td>\n",
              "      <td>0</td>\n",
              "      <td>0.469</td>\n",
              "      <td>7.185</td>\n",
              "      <td>61.1</td>\n",
              "      <td>4.9671</td>\n",
              "      <td>2</td>\n",
              "      <td>242</td>\n",
              "      <td>17.8</td>\n",
              "      <td>392.83</td>\n",
              "      <td>4.03</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>0.03237</td>\n",
              "      <td>0.0</td>\n",
              "      <td>2.18</td>\n",
              "      <td>0</td>\n",
              "      <td>0.458</td>\n",
              "      <td>6.998</td>\n",
              "      <td>45.8</td>\n",
              "      <td>6.0622</td>\n",
              "      <td>3</td>\n",
              "      <td>222</td>\n",
              "      <td>18.7</td>\n",
              "      <td>394.63</td>\n",
              "      <td>2.94</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>0.06905</td>\n",
              "      <td>0.0</td>\n",
              "      <td>2.18</td>\n",
              "      <td>0</td>\n",
              "      <td>0.458</td>\n",
              "      <td>7.147</td>\n",
              "      <td>54.2</td>\n",
              "      <td>6.0622</td>\n",
              "      <td>3</td>\n",
              "      <td>222</td>\n",
              "      <td>18.7</td>\n",
              "      <td>396.90</td>\n",
              "      <td>5.33</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>501</th>\n",
              "      <td>0.06263</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.593</td>\n",
              "      <td>69.1</td>\n",
              "      <td>2.4786</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>391.99</td>\n",
              "      <td>9.67</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>502</th>\n",
              "      <td>0.04527</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.120</td>\n",
              "      <td>76.7</td>\n",
              "      <td>2.2875</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>396.90</td>\n",
              "      <td>9.08</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>503</th>\n",
              "      <td>0.06076</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.976</td>\n",
              "      <td>91.0</td>\n",
              "      <td>2.1675</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>396.90</td>\n",
              "      <td>5.64</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>504</th>\n",
              "      <td>0.10959</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.794</td>\n",
              "      <td>89.3</td>\n",
              "      <td>2.3889</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>393.45</td>\n",
              "      <td>6.48</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>505</th>\n",
              "      <td>0.04741</td>\n",
              "      <td>0.0</td>\n",
              "      <td>11.93</td>\n",
              "      <td>0</td>\n",
              "      <td>0.573</td>\n",
              "      <td>6.030</td>\n",
              "      <td>80.8</td>\n",
              "      <td>2.5050</td>\n",
              "      <td>1</td>\n",
              "      <td>273</td>\n",
              "      <td>21.0</td>\n",
              "      <td>396.90</td>\n",
              "      <td>7.88</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>506 rows × 13 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "        crim    zn  indus  chas    nox  ...  rad  tax  ptratio       b  lstat\n",
              "0    0.00632  18.0   2.31     0  0.538  ...    1  296     15.3  396.90   4.98\n",
              "1    0.02731   0.0   7.07     0  0.469  ...    2  242     17.8  396.90   9.14\n",
              "2    0.02729   0.0   7.07     0  0.469  ...    2  242     17.8  392.83   4.03\n",
              "3    0.03237   0.0   2.18     0  0.458  ...    3  222     18.7  394.63   2.94\n",
              "4    0.06905   0.0   2.18     0  0.458  ...    3  222     18.7  396.90   5.33\n",
              "..       ...   ...    ...   ...    ...  ...  ...  ...      ...     ...    ...\n",
              "501  0.06263   0.0  11.93     0  0.573  ...    1  273     21.0  391.99   9.67\n",
              "502  0.04527   0.0  11.93     0  0.573  ...    1  273     21.0  396.90   9.08\n",
              "503  0.06076   0.0  11.93     0  0.573  ...    1  273     21.0  396.90   5.64\n",
              "504  0.10959   0.0  11.93     0  0.573  ...    1  273     21.0  393.45   6.48\n",
              "505  0.04741   0.0  11.93     0  0.573  ...    1  273     21.0  396.90   7.88\n",
              "\n",
              "[506 rows x 13 columns]"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 14
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "y5wMVRtpkvo2",
        "colab_type": "text"
      },
      "source": [
        "## **Data split**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "a2FdlRkWlGhd",
        "colab_type": "text"
      },
      "source": [
        "### **Import library**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "-loRD7Chkx2u",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "from sklearn.model_selection import train_test_split"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "5u43h3GllJL5",
        "colab_type": "text"
      },
      "source": [
        "### **Perform 80/20 Data split**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "DCkW1c_fk0ZB",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.2)"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "3KraL05hlAlF",
        "colab_type": "text"
      },
      "source": [
        "### **Data dimension**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "wRle727Kk5zD",
        "colab_type": "code",
        "outputId": "e2290a0e-d184-4d1c-c54f-f0b22de0902e",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "X_train.shape, Y_train.shape"
      ],
      "execution_count": 17,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "((404, 13), (404,))"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 17
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "eYuH1K2Dk_2r",
        "colab_type": "code",
        "outputId": "5b2bc4a4-bd0d-4567-dcb4-dc52259e4b18",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "X_test.shape, Y_test.shape"
      ],
      "execution_count": 18,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "((102, 13), (102,))"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 18
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ftLHUDWWmAyC",
        "colab_type": "text"
      },
      "source": [
        "## **Linear Regression Model**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "u20GkslXmLm8",
        "colab_type": "text"
      },
      "source": [
        "### **Import library**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "7ZQh8TtjmDwi",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "from sklearn import linear_model\n",
        "from sklearn.metrics import mean_squared_error, r2_score"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "vCYTGIh1KSvo",
        "colab_type": "text"
      },
      "source": [
        "### **Build linear regression**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "S2DWBNumCnBY",
        "colab_type": "text"
      },
      "source": [
        "#### Defines the regression model"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "0mUdKcftmYKC",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "model = linear_model.LinearRegression()"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "6AVIFWcbCw6p",
        "colab_type": "text"
      },
      "source": [
        "#### Build training model"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Fv-a-toQmc0c",
        "colab_type": "code",
        "outputId": "3f3bca7e-fcb1-4891-fc68-2200783dfa68",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "model.fit(X_train, Y_train)"
      ],
      "execution_count": 21,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "LinearRegression(copy_X=True, fit_intercept=True, n_jobs=None, normalize=False)"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 21
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "OVfa9YhYC2lD",
        "colab_type": "text"
      },
      "source": [
        "#### Apply trained model to make prediction (on test set)"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Ceqli7YtmkM9",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "Y_pred = model.predict(X_test)"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "kOgx7y7wLiW-",
        "colab_type": "text"
      },
      "source": [
        "## **Prediction results**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "eNj5NwDnC91W",
        "colab_type": "text"
      },
      "source": [
        "### **Print model performance**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "hQPfL1nkmvxb",
        "colab_type": "code",
        "outputId": "bcc90329-bd73-4fd8-86f0-9b6e8fdbb5bf",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 136
        }
      },
      "source": [
        "print('Coefficients:', model.coef_)\n",
        "print('Intercept:', model.intercept_)\n",
        "print('Mean squared error (MSE): %.2f'\n",
        "      % mean_squared_error(Y_test, Y_pred))\n",
        "print('Coefficient of determination (R^2): %.2f'\n",
        "      % r2_score(Y_test, Y_pred))"
      ],
      "execution_count": 23,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Coefficients: [-1.00050462e-01  4.25597647e-02  4.88553708e-02  3.85303261e+00\n",
            " -1.71332360e+01  3.91262456e+00  5.06045646e-04 -1.30894438e+00\n",
            "  2.78526738e-01 -1.06247981e-02 -9.55659863e-01  9.59720319e-03\n",
            " -5.09207833e-01]\n",
            "Intercept: 33.890629034122\n",
            "Mean squared error (MSE): 26.54\n",
            "Coefficient of determination (R^2): 0.71\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ukQ1MFxzDNc2",
        "colab_type": "text"
      },
      "source": [
        "### **String formatting**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "MLeShbUDDTe7",
        "colab_type": "text"
      },
      "source": [
        "By default r2_score returns a floating number ([more details](https://docs.scipy.org/doc/numpy-1.13.0/user/basics.types.html))"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "vXc3Zh9rDZDr",
        "colab_type": "code",
        "outputId": "297d69ac-6dc8-4121-9cc0-42ba5a9a52ca",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "r2_score(Y_test, Y_pred)"
      ],
      "execution_count": 24,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.7072810305481783"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 24
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "p4dYm1msDa8y",
        "colab_type": "code",
        "outputId": "5b774a05-1aaf-470e-e2c9-4be8e494ee55",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "r2_score(Y_test, Y_pred).dtype"
      ],
      "execution_count": 25,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "dtype('float64')"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 25
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "HvlQcuhIEC13",
        "colab_type": "text"
      },
      "source": [
        "We will be using the modulo operator to format the numbers by rounding it off."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "cl_B_EBYFx4L",
        "colab_type": "code",
        "outputId": "12ab90fe-98c3-4871-ffe6-fadd23176295",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "'%f' % 0.523810833536016"
      ],
      "execution_count": 26,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "'0.523811'"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 26
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "coHGJ_CrG5mY",
        "colab_type": "text"
      },
      "source": [
        "We will now round it off to 3 digits"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "WXv_MDhVF0zN",
        "colab_type": "code",
        "outputId": "346671bf-872e-495e-862f-26203b7d12a8",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "'%.3f' % 0.523810833536016"
      ],
      "execution_count": 27,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "'0.524'"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 27
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "4tvESBrSHBcs",
        "colab_type": "text"
      },
      "source": [
        "We will now round it off to 2 digits"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "mmT1UMUaHHnw",
        "colab_type": "code",
        "outputId": "fb4aad67-5ee6-456c-a512-656b77741cf0",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 34
        }
      },
      "source": [
        "'%.2f' % 0.523810833536016"
      ],
      "execution_count": 28,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "'0.52'"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 28
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "bmL8ZSOTKYDw",
        "colab_type": "text"
      },
      "source": [
        "## **Scatter plots**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "_Mi1ipCJPczT",
        "colab_type": "text"
      },
      "source": [
        "### **Import library**"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "JDh3jorMKd8Q",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        "import seaborn as sns"
      ],
      "execution_count": 0,
      "outputs": []
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "pxD1MIXdPepK",
        "colab_type": "text"
      },
      "source": [
        "### **Make scatter plot**"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "0DbZGw8sI4jR",
        "colab_type": "text"
      },
      "source": [
        "#### The Data"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "8xBzmCpaJEBB",
        "colab_type": "code",
        "outputId": "cf9404ab-c1bb-446b-e49a-73b28be2b653",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 221
        }
      },
      "source": [
        "Y_test"
      ],
      "execution_count": 30,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "152    15.3\n",
              "159    23.3\n",
              "376    13.9\n",
              "222    27.5\n",
              "101    26.5\n",
              "       ... \n",
              "383    12.3\n",
              "87     22.2\n",
              "22     15.2\n",
              "127    16.2\n",
              "504    22.0\n",
              "Name: medv, Length: 102, dtype: float64"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 30
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "UPwtR8XsKYoE",
        "colab_type": "code",
        "outputId": "ab82eaf9-2cd1-4189-8fd6-bbf0ee45030a",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 187
        }
      },
      "source": [
        "import numpy as np\n",
        "np.array(Y_test)"
      ],
      "execution_count": 31,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([15.3, 23.3, 13.9, 27.5, 26.5, 19.3, 36.2, 42.3, 23.8, 16.7, 11.3,\n",
              "       24.4, 20.6, 23.9, 10.9, 37.6, 19. , 22.8, 29.1, 19.9, 18.5, 19.4,\n",
              "       16.1,  8.4, 12.1, 31.5, 24.7, 26.4, 22.3, 25.2, 15.6, 17.8,  7.2,\n",
              "       18.5, 18.9, 19.4, 15.6, 18.9, 50. , 13.9, 16.4, 37.9, 10.2, 24.1,\n",
              "       50. , 20.6, 18.4, 23. , 21.2, 27.9, 44.8, 20.7,  8.3, 11.8, 15. ,\n",
              "       23.1, 21.9, 24.8, 20.9,  8.1, 18.2, 20.5, 15.6, 21.4, 20. , 22. ,\n",
              "       22.4, 12.7, 13.5, 22.8, 13.4,  8.4, 50. , 16.5, 22.3, 34.9, 22.5,\n",
              "       23.1, 21.6, 46.7, 19.5, 11.7, 22.2, 29.9, 50. , 21.2, 30.3,  7. ,\n",
              "       23.3, 14.5, 19.5, 13.4, 29. , 30.1, 21.9, 11. , 24.3, 12.3, 22.2,\n",
              "       15.2, 16.2, 22. ])"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 31
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "U8UAehGlJIeS",
        "colab_type": "code",
        "outputId": "0c321930-3e91-4a66-812e-a2d368810109",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 374
        }
      },
      "source": [
        "Y_pred"
      ],
      "execution_count": 32,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([21.3969995 , 25.78787156, 18.00497747, 32.99703165, 25.4474803 ,\n",
              "       20.73540261, 27.08440187, 36.98678114, 26.53684192, 20.76173404,\n",
              "       13.60074088, 28.14853668, 19.73530644, 24.62028308, 18.73922314,\n",
              "       37.27411339, 14.52963986, 28.46143692, 29.94181835, 19.14147404,\n",
              "       19.18307551, 23.06505316, 18.8400145 ,  5.25333402, 18.47500581,\n",
              "       30.81620649, 22.63410539, 28.77546229, 27.22815761, 26.88595528,\n",
              "       13.59371314, 21.08056431,  8.35412851, 19.35533031, 23.43521384,\n",
              "       23.47412116, 12.5295889 , 21.83429104, 40.41962859, 13.39426264,\n",
              "       19.33401488, 33.24955401, 16.34851367, 21.23884298, 35.39992502,\n",
              "       22.13608838, 18.94239498, 23.68601818, 23.33635488, 19.91338453,\n",
              "       38.04480377, 21.57963707, 13.21478382, 12.25281136, 25.52578575,\n",
              "       25.50153569, 38.89350142, 30.88847137, 20.95560997,  4.67574832,\n",
              "       19.26663744, 20.1968555 , 15.73055629, 22.48979365, 23.10502457,\n",
              "       27.3630545 , 23.38348282, 12.864994  , 13.69752447, 24.61248362,\n",
              "       13.29402643, 14.87143328, 24.84679762, 22.45894991, 26.83771245,\n",
              "       30.18353822, 21.95780828, 22.49700709, 25.3671763 , 35.15662905,\n",
              "       17.00385344, 14.59914182, 19.42262377, 31.02130551, 42.82843704,\n",
              "       21.58990262, 32.73793049,  9.17568096, 27.66447805, 13.85290565,\n",
              "       19.98379052, 16.12035875, 32.0257592 , 25.82073566, 15.48260265,\n",
              "       14.41555638, 20.33727524, 13.23072672, 25.50869879, 15.87972124,\n",
              "       15.44633029, 25.93124132])"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 32
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "XEa9vmBjI8Bd",
        "colab_type": "text"
      },
      "source": [
        "#### Making the scatter plot"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Wuig81bSKgGN",
        "colab_type": "code",
        "outputId": "4f3eed58-526f-40cf-cdcf-7737c9f53148",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 296
        }
      },
      "source": [
        "sns.scatterplot(Y_test, Y_pred)"
      ],
      "execution_count": 33,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<matplotlib.axes._subplots.AxesSubplot at 0x7f664f026748>"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 33
        },
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": []
          }
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "34PEHdfwPv8X",
        "colab_type": "code",
        "outputId": "9e902fe0-93cc-4668-e911-1abc9c193bdf",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 296
        }
      },
      "source": [
        "sns.scatterplot(Y_test, Y_pred, marker=\"+\")"
      ],
      "execution_count": 34,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<matplotlib.axes._subplots.AxesSubplot at 0x7f664f00cac8>"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 34
        },
        {
          "output_type": "display_data",
          "data": {
            "image/png": "iVBORw0KGgoAAAANSUhEUgAAAXAAAAEGCAYAAAB8Ys7jAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAADh0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uMy4yLjEsIGh0\ndHA6Ly9tYXRwbG90bGliLm9yZy+j8jraAAAY2UlEQVR4nO3dfYxcV33G8e+TxNgpcZW3bWTFMQ4v\nKkIEnGYbsEAouIDSEgVQk5iXotBG2FSlAkEKIX9QA0ICNRCoQK5Nk8a0ARwb3KAIGqIkVoBaCbt5\ncV6cNi8ktSMTbwpRHFCsOvn1j7njjMczO3dm7p25Z+7zkayduTsvZ6+8z5z9nXPPUURgZmbpOWrc\nDTAzs8E4wM3MEuUANzNLlAPczCxRDnAzs0QdM8o3O/nkk2P58uWjfEszs+TNzs4+FRFT7cdHGuDL\nly9nZmZmlG9pZpY8SY93Ou4SiplZohzgZmaJcoCbmSXKAW5mligHuJlZohzgZmYjsGVmd+Gv6QA3\nMxuBrbN7Cn9NB7iZWaJGeiGPmVmdbJnZfajnffsvf83qDTsAuOCspVw4fdrQr+8ANzMryYXTpx0K\n6tUbdrB57cpCX98lFDOzRDnAzcxG4IKzlhb+mg5wM7MRKKLm3c4BbmaWKAe4mVmiHOBmZolygJuZ\nJcoBbmaWKAe4mdkIeDErM7NEjXUxK0lHS7pL0g3Z/dMl3S7pYUmbJb2k8NaZmVlX/ayF8jFgF/D7\n2f0vA1dGxPck/RNwCbC+4PaZmSWrEotZSVoKvBP4IvAJSQJWAe/PHrIJWIcD3MzskKosZvU14FPA\nC9n9k4CnI+Jgdn8PcGqnJ0paI2lG0szc3NxQjTUzsxf1DHBJ5wH7ImJ2kDeIiI0RMR0R01NTU4O8\nhJlZ8spYzCpPCeVNwPmS/gxYRKMG/nXgeEnHZL3wpcAThbfOzGxCjGUxq4j4TEQsjYjlwHuBWyLi\nA8CtwAXZwy4Gri+8dZacMua6mllnw8wD/zSNAc2HadTEryqmSZayMua6mllnfW2pFhHbge3Z7UeB\ns4tvkpmZ5eE9MW1oZc91NbPOHOA2tLLnupr1a8vM7lp0HrwWiplNnLqMxTjArVBlzHU1s85cQrFC\n1eHPVqumOo7FOMDNDEi/blzHsRiXUMwMqE/deJI4wM2sMoq6krcuYzEuoZjVWNXqxltn9xTyvimX\ngvrhADersTrWjSeJA9zMxqpqfwWkxAFuZsD46sb+K2BwHsQ0M6A+deNJ4gA3s8qoy+yRojjAzawy\n/FdAfxzgZmYjUMZuVQ5wMzPK3w6wjCtd8+xKv0jSHZLukXS/pM9lx6+R9EtJd2f/VhTeOjOzEUlx\nKYE80wgPAKsi4llJC4CfSfpx9r2/i4it5TXPzCxdZc9x7xngERHAs9ndBdm/GPqdzczGrOyALXuO\ne64LeSQdDcwCrwS+GRG3S/pr4IuSPgvcDFwWEQc6PHcNsAZg2bJlhTXczGxYqV9ElGsQMyKej4gV\nwFLgbEmvBT4DvBr4Y+BE4NNdnrsxIqYjYnpqaqqgZpuZpaWMOe59zUKJiKeBW4FzI2JvNBwA/gU4\nu/DWmZmNSNkXEZUxxz3PLJQpScdnt48F3g48KGlJdkzAu4H7Cm+dmdmIpHgRUZ4a+BJgU1YHPwq4\nLiJukHSLpClAwN3AR0psp5mZtckzC2UncGaH46tKaZGZmeXiKzHN7DBlX5FoxXGAW204mPJJ8YrE\nunKAW204mGzSeEceswFtmdmd5MyFTrytWZoc4DbRygymonZQr4LUr0isKwe4TTQHk00yB7hZB93K\nI3UoNXhbs3Q4wK02+gmmbuWROvToJ+WDqA48C8Vqw8Fkk8Y9cLNMv+URlxps3NTYr2E0pqenY2Zm\nZmTvZzaoSS2PWJokzUbEdPtxl1DM+uCrOa1KHOBWaeMKzG7lkX6v5nTgW5kc4FZp47r8vagBT1++\nb2XyIKZZD3WY+21p8iCmVU57YL7h9BOBagRmnsHNKrff0tRtENM9cKuc1C+WGWX7J2lBLetfnj0x\nF0m6Q9I9ku6X9Lns+OmSbpf0sKTNkl5SfnPNRqfTAGTV5n67xl5veQYxDwCrIuL1wArgXElvBL4M\nXBkRrwR+A1xSXjOtrsYZmJ3Csd/ebtUC3yZLnj0xA3g2u7sg+xfAKuD92fFNwDpgffFNtDpLvTxQ\nRvs9qGpNuWrg2Y70s8ArgW8CjwBPR8TB7CF7gFO7PHcNsAZg2bJlw7bXrFQphGPqYwRWnFwBHhHP\nAyskHQ9sA16d9w0iYiOwERqzUAZppNmoOBwtJX1dyBMRTwO3AiuB4yU1PwCWAk8U3DYz68E19nrL\nMwtlKut5I+lY4O3ALhpBfkH2sIuB68tqpFkeRV+2nkI4VqWsY+ORpwe+BLhV0k7gF8BNEXED8Gng\nE5IeBk4CriqvmWa9FT2lzuFoVZdnFspO4MwOxx8Fzi6jUTZ5fMGJWfF8JaaNRD87uPcT9inMGjEr\niwPcKqefsPesEaszB7iVxr1js3I5wK008/WO28skRYR9CrNGzIrkALdC5a1ft5dJiiiFuFdvdeMd\neaxQzV50+5xs947NiuceuJWiUw87b5nEYV8sT+GcXA5wG1qnYL5n99NHBEfeMkm3sHEQDaafWT2W\nFpdQbGgXTp/G5rUrueCspSxe1OgTPHfwBbbO7mH1hh2FXeLuzQvMDuceuBXmwunT2Dq7h81rV3LG\nuhvnHYhsLZO4Z108T+GsB29qbIXZMrOb9dsfYWrxwr42852vnOINgofnC5zS502NrXStNe5VV2wv\nJDR8paVZdw5wK1SzHDK1eGHPx6X8J35KZR/P6plcDnArVHPGQ57QaPam8/asqxREKc3sSKWd1j/P\nQqmQojckqKLmzzjIjJI8QVSHc2jW5B54haTUq2vVPni5esMOHtj7DHBk6Hb6GYvsWZd5DlMv+9jk\n6Rngkk4Dvg2cAgSwMSK+Lmkd8GFgLnvo5RHxo7IaatXVOn2wWQ5ZvWHHEaG2ZWY3D+x9htUbdhwR\ngCnwgKpVTZ4e+EHgkxFxp6TFwKykm7LvXRkRV5TXvMk3Sb26bgH9spN+j8f/93cA7H/uIACLFx1T\n2M84SefQJlcZA995tlTbC+zNbu+XtAs4tdBW1FjKvbr24ASYOm7hoR51p59lvh76oMZxDlP5q8Gq\no4zyXl+DmJKW09gf8/bs0Ecl7ZR0taQTCm2ZVV7zEvrNa1fyhtNPZPPaldxy6Tkd/5P2Wp0wtcFH\n9+ytCnIHuKTjgO8DH4+IZ4D1wCuAFTR66F/p8rw1kmYkzczNzXV6iGUmqVfX/rM0e+rN450GN8t4\nX7Nx2jKzm9UbdhxWVixyfaBcs1AkLaAR3tdGxA8AIuLJlu9/C7ih03MjYiOwERqX0g/b4EmWcq+u\nPTi7/Sxl/4wpn0ObPGWX9/LMQhFwFbArIr7acnxJVh8HeA9wX6Ets6R0K5vMN7jowUez4fRczErS\nm4GfAvcCL2SHLwfeR6N8EsBjwNqWQO/Ii1nV1+oNO+YN5tQGcM36NcwslIEXs4qInwHq8C3P+ba+\npHqhklkRyvi/70vpa6p9EGWQQZVez2n9fq/BRQ8+mvXPAV5T7bM+2u/nCfReM0e2zu45NAq/dXbP\nvKPw7pmb9c9roRgAc/sPHHa/qHJHyhcqmVWdA7xG2md9rLpiO3PPHmDquIU8+tRvc61NMszMEjMr\nlrdUq6n23vAZ627ks+e9pq/ty3r1qNu/3+8ofEqbJpiVyVuqTZCigq21t7z/uYNHXC2Zp9zRT1ua\nPfS8j/esFbP5eRAzQUVcdt7sVTfXMnn5yS89dDvPWibN15ivLZ3KJkVdMm9mDvDaag/p9j0su61l\nMt9rdPp+v9MTy147wmySuISSiKIvO28vZeRdy6TftjQfl/fxnrVilp8DPBFFB1t7fTnPWiarrtjO\n1OLGet+b16481Cvu1RaHslk5HOAVVJXZF+3BC4eHdbd6dlFTCT310Gx+DvAK6jX7YtBgK2P1v05t\nGbTH3f7BVYUPMbMqc4AnKG+wdQrEfoO1Gfpz+w/w6FO/PeLiH2h84OT9EJjvMZ42aNYfB3hFlNE7\nLiIQO4V+84Mhz4eAyyBm5XGAV8SgveMiSh/9vk4/Hwy9HudNHcwG5wBPWKcgzRuIrbfzBnJ7b7qI\n3rVnqJgNzgFeQcMEY1mB2PxgaF0WtvU9i1SVWThmVZdnT8zTgG8Dp9DYPm1jRHxd0onAZmA5jS3V\nLoqI35TX1Poo6iKa+QzyOs0Pg7J6ys0PLg9mmuWTpwd+EPhkRNwpaTEwK+km4EPAzRHxJUmXAZcB\nny6vqQb99bDn68nPNzjZyShCdZSh7V6+TYI8e2LuBfZmt/dL2gWcCrwLOCd72CZgOw7wSuk3oOYL\n6dYNH8qYWTLqwUz38m0S9FUDl7QcOBO4HTilZRf6X9EosdgIFRWk3V6nNVTzbvgwKA9mmvUvd4BL\nOg74PvDxiHhGenGj+ogISR13hpC0BlgDsGzZsuFaa8CLf/4PckFPe+mg2+Bks+fbfOwZ627sK1Sr\nWKLwlEWbNLkCXNICGuF9bUT8IDv8pKQlEbFX0hJgX6fnRsRGYCM0duQpoM211++f/62PX7/9kZ5X\nZzbDt33Dh34Cb5gSRVkX/7iXb5MmzywUAVcBuyLiqy3f+iFwMfCl7Ov1pbTQCrNlZjdzzx7o+bhm\n+LYG3qorto8s8NwbNssnTw/8TcAHgXsl3Z0du5xGcF8n6RLgceCicpo4HlUrAWyZ2c367Y8wtXhh\nrj//28sFZ6y7kd8dOMjzQdfnztfzbd/woVsbUylR+BJ/mwTe1LiLXn9ijyPgm23q98//5jreD+x9\nhv3PHey4WXF7+LY/pt+f1yUKs+J4U+OCpTINrVk2mVq8kP3PHeTobOy506X189WHU/hZzerGAd6i\niiWATm2a238gd4+4+Zjm6oFz+w+MpGfsEoVZ+VxC6aJTL7RXmaGXYcsuw5YlVm/YkautVav/m9Wd\nSygFGHYa2rjLLkVsumBm1XHUuBtQVVUsAQzbJgez2WRxD7yLXmGXN0yLrKs7gM2slWvgI+SpdWY2\niG41cJdQ7JAtM7vH3QQz64MDfISqWFdv1Sz1mFkaHOAj5Bq2mRXJg5jUe95zFS9eMrN8HOCMf372\nOHmJVbN0uYRSIg8KmlmZatsDH0XpYJCe/TjLOVUfZDWzw9U2wKtaOmgN/VGHeV3LSGapcgmlYFtm\ndrN6ww5Wb9hxqGe/esOOgcop7dP6UijJpNBGs0lR2x54qyJLB4P07LuVc+b2H779WQqDrSm00WxS\n5NkT82rgPGBfRLw2O7YO+DAwlz3s8oj4UVmNLNu4A6d978mmR5/67WG1eTOzVnl64NcA3wC+3Xb8\nyoi4ovAWDalKc7oHCd2pxQsP9dqb63dvnd3D1tk9lZ2n7bnkZuPRM8Aj4jZJy8tvSjGq9Cf8IO1o\nD/2qDra2SqGNZpNomEHMj0raKelqSSd0e5CkNZJmJM3Mzc11e1jldBqMG8UAXd5d4ovgAUeztA0a\n4OuBVwArgL3AV7o9MCI2RsR0RExPTU0N+HbzK3LmR1OnhZ1GvdhTew++6EAv4+dxrd5sdAaahRIR\nTzZvS/oWcENhLRpAXf6Er0ppaD4ptNFsUgwU4JKWRMTe7O57gPuKa9L4dNsBHhqDi0UP0I1jwNUD\njmYTJCLm/Qd8l0aZ5P+APcAlwL8C9wI7gR8CS3q9TkRw1llnRdmu+8X/FPI6F/3Tf+Y61st87Rnk\n9Yo07vc3s3yAmeiQqT1r4BHxvohYEhELImJpRFwVER+MiDMi4nURcX682BsfuzJ6kUXX0kfxvmY2\n+XwlZhetg3HNqYn9DtC1B3Dzft4SRtlTIj3gaJa2iQrwImvKnV6n07FO79msMz+w9xn2P3fwsEvj\nb7n0nMoMuLrmbZa2iQrwInuseQf7Oq0e2PzXfE7rlZVFva+Z2UQFeJEGmZrYDN7WAF50zFGcse5G\npo5beMTaJp1KGHWZEmlmw0s+wMfRY51v9cD2AG5tR7+B3L4aoZlZq+QDfBQ91vnWJ+m1eqDLHmZW\nluQDfBRaQ7h90LJ99cD5PkD6nfUxtXhhny01szqZqAAfxbS49oHS+d6zvfedpzfuQUwzy2uiAnwc\nAVf06oEexDSzvCYqwMuSt1fsHrKZjZIDPIdx9Yp9paSZzce70leYe/RmNh8HeJ/cKzazqnCA98m9\nYjOrCge4mVmiHOBmZolygJuZJapngEu6WtI+Sfe1HDtR0k2SHsq+nlBuM83MrF2eHvg1wLltxy4D\nbo6IVwE3Z/fNzGyE8uyJeRvw67bD7wI2Zbc3Ae8uuF1mZtbDoDXwU1o2Mv4VcEq3B0paI2lG0szc\n3NyAb2dmZu2GHsTMtryPeb6/MSKmI2J6ampq2LczM7PMoAH+pKQlANnXfcU1qbP2Hd7NzOpu0AD/\nIXBxdvti4PpimtNdczVAMzNryDON8LvADuAPJe2RdAnwJeDtkh4C3pbdNzOzEeq5nGxEvK/Lt/6k\n4LYcwbvTmJl1V+n1wDutw92+J6WZWV0ldym9a+FmZg3JBLjX4TYzO1ylSyhNzVr41tk9roWbmWWS\nCHDv1G5mdqRkSihmZna45ALctXAzs4bkAtw1bzOzhuQC3MzMGhzgZmaJcoCbmSXKAW5mligHuJlZ\nohzgZmaJcoCbmSXKAW5mlqiJC3DvnWlmdTFUgEt6TNK9ku6WNFNUo4bh9cLNrC6KWI3wrRHxVAGv\nY2ZmfUhiOdletszsZv32R5havNDrhZtZbQwb4AH8RFIAGyJiY/sDJK0B1gAsW7ZsyLfr7MLp09g6\nu4fNa1d6vXAzq41hBzHfHBF/BPwp8DeS3tL+gIjYGBHTETE9NTU15NuZmVnTUD3wiHgi+7pP0jbg\nbOC2IhqWR3OrNeBQ6WRu/wHvXG9mtTBwgEt6KXBUROzPbr8D+HxhLcvBW62ZWZ0N0wM/Bdgmqfk6\n34mI/yikVWZm1tPAAR4RjwKvL7AtQ/FWa2ZWNxNzJaZr3mZWNxMT4GZmdeMANzNLlAPczCxRDnAz\ns0Q5wM3MEqWIGN2bSXPA4yN7w95OBrySYmc+N9353HTnc9PdMOfmZRFxxFokIw3wqpE0ExHT425H\nFfncdOdz053PTXdlnBuXUMzMEuUANzNLVN0D/Ij1y+0Qn5vufG6687nprvBzU+sauJlZyureAzcz\nS5YD3MwsUbUJcElXS9on6b6WYydKuknSQ9nXE8bZxnGRdJqkWyU9IOl+SR/Ljtf6/EhaJOkOSfdk\n5+Vz2fHTJd0u6WFJmyW9ZNxtHRdJR0u6S9IN2X2fG0DSY5LulXS3pJnsWOG/T7UJcOAa4Ny2Y5cB\nN0fEq4Cbs/t1dBD4ZES8Bngjjf1NX4PPzwFgVUS8HlgBnCvpjcCXgSsj4pXAb4BLxtjGcfsYsKvl\nvs/Ni94aESta5n4X/vtUmwCPiNuAX7cdfhewKbu9CXj3SBtVERGxNyLuzG7vp/ELeSo1Pz/R8Gx2\nd0H2L4BVwNbseO3OS5OkpcA7gX/O7gufm/kU/vtUmwDv4pSI2Jvd/hWNbeJqTdJy4Ezgdnx+miWC\nu4F9wE3AI8DTEXEwe8geGh92dfQ14FPAC9n9k/C5aQrgJ5JmJa3JjhX++zTUrvSTJCJCUq3nVEo6\nDvg+8PGIeCbb7xSo7/mJiOeBFZKOB7YBrx5zkypB0nnAvoiYlXTOuNtTQW+OiCck/QFwk6QHW79Z\n1O9T3XvgT0paApB93Tfm9oyNpAU0wvvaiPhBdtjnJxMRTwO3AiuB4yU1Oz9LgSfG1rDxeRNwvqTH\ngO/RKJ18HZ8bACLiiezrPhof/GdTwu9T3QP8h8DF2e2LgevH2JaxyWqXVwG7IuKrLd+q9fmRNJX1\nvJF0LPB2GuMDtwIXZA+r3XkBiIjPRMTSiFgOvBe4JSI+gM8Nkl4qaXHzNvAO4D5K+H2qzZWYkr4L\nnENjSccngb8H/h24DlhGY5nbiyKifaBz4kl6M/BT4F5erGdeTqMOXtvzI+l1NAabjqbR2bkuIj4v\n6eU0ep0nAncBfxERB8bX0vHKSiiXRsR5PjeQnYNt2d1jgO9ExBclnUTBv0+1CXAzs0lT9xKKmVmy\nHOBmZolygJuZJcoBbmaWKAe4mVmiHOBm85C0XZI36bVKcoCbmSXKAW4TR9JySQ9KukbSf0u6VtLb\nJP08W4v57Oxquauz9b7vkvSu7LnHSvqepF2StgHHZsc/IukfWt7jQ5K+MaYf0QzwhTw2gbIVFR+m\nsari/cAvgHtorE19PvCXwAPAAxHxb9nl8ndkj18LvDYi/iq7EvNOGmukPw7syNa5RtKPgS9GxM9G\n+KOZHcarEdqk+mVE3Asg6X4aC+mHpHuB5TQWWjpf0qXZ4xfRuMT5LcA/AkTETkk7s9tzkh7NNnR4\niMaqhD8f5Q9k1s4BbpOqdf2NF1ruv0Dj//3zwJ9HxH+1Pql1Cd0OvgdcBDwIbAv/+Wpj5hq41dWN\nwN9mKzEi6czs+G3A+7NjrwVe1/KcbTR2VXkfjTA3GysHuNXVF2hskbYzK7F8ITu+HjhO0i7g88Bs\n8wkR8Rsay8m+LCLuGHF7zY7gQUwzs0S5B25mligHuJlZohzgZmaJcoCbmSXKAW5mligHuJlZohzg\nZmaJ+n8BKf/W/OPiogAAAABJRU5ErkJggg==\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": []
          }
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "kPgBVuuOQ4IQ",
        "colab_type": "code",
        "outputId": "3bb04892-d4d0-4666-b241-903c43b76420",
        "colab": {
          "base_uri": "https://localhost:8080/",
          "height": 296
        }
      },
      "source": [
        "sns.scatterplot(Y_test, Y_pred, alpha=0.5)"
      ],
      "execution_count": 35,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "<matplotlib.axes._subplots.AxesSubplot at 0x7f664c2adcc0>"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 35
        },
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": []
          }
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "5VLUdcQSIebl",
        "colab_type": "code",
        "colab": {}
      },
      "source": [
        ""
      ],
      "execution_count": 0,
      "outputs": []
    }
  ]
}
