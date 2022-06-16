# Related paper:
Tzu-Hsien Yang*, Yu-Huai Yu+, Shang-Hang Wu+, Fang-Yuan Zhang+, "CFA: an explainable deep learning model for cis-regulatory module transcriptional role annotation based on epigenetic codes". (Submitting)

+: These authors contributed equally.

# Prepare the Environment

Suggested running environments: Linux Ubuntu 16.04.6, Python 3.8.13

We recommend that you can use the conda package to create a new environment. This will automatically install the required python packages. 

Here is an example: 

1. Install the Conda package for you system. The installation of the package can be found <a href="https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html">here</a>. 

2. Create the CFA Conda environment. This may take a while, depending on the network status.

```
conda create -n "CFA" python=3.8.13
```

4. Activate your CFA Conda environment. 

```
conda activate CFA
```

## **Steps to Use CFA**

1. Download the codes from the following link and unzip the file. Please skip it if you have done this step.

```
wget https://cobishss0.im.nuk.edu.tw/CFA/CFA_Model.tar.gz
```

2. Unzip the file.

```
tar -zxvf CFA_Model.tar.gz
```

3. Change the working directory.

```
cd CFA_Model
```

4. Download the processed epigenetic datasets from the following link.

```
wget https://cobishss0.im.nuk.edu.tw/CFA/CFA_Dataset.tar.gz
```

5. Unzip the file.

```
tar -zxvf CFA_Dataset.tar.gz
```

6. If this is the first time you use CFA, run the following command to install necessary packages. 

```
pip install -r requirements.txt
```

7. Prepare the input Drosophila CRM chromosomal regions (ver. DM6).
   Multiple chromosomal regions can be provided in the same input file.
   
   The input format **SHOULD** followed the following formats:
   chromosome,start,end
   
   For example: (as the input file named input_Test.csv) 
   
   ![](https://i.imgur.com/hG5yhr3.png)
   
   Note: The input chromosomal regions start from the 5' end.

8. Predict the identification probability of CRM transcriptional roles (promoter, enhancer, and insulator).

```
python main.py -i <input_csv_file> -o <output_directory>
```
>**Required arguments:**
>
>* -i: The input file of the CFA Model.
>
>* -o: The output directory of the predicted results and SHAP bar plots.

   The probability results will be saved to the file named "predicted_result.csv" in the specified output directory.
   
   CFA also provides the top five determining epigenetic profiling types for every CRM. The SHAP value plots and the standardized ChIP-seq socres are stored in the specified output directory.

## Output Results
If we use the following as our inputs with the example command:

![](https://i.imgur.com/37L3zry.png)

```
python main.py -i input_Test.csv -o output/
```

>** output/predicted_result.csv :**

![](https://i.imgur.com/8Hv0RmR.png)

Output format explanation:
>* CRM_location,0,0,0 --> Contains nothing.
>* CRM_location,1,0,0 --> Contains promoter.
>* CRM_location,0,1,0 --> Contains enhancer.
>* CRM_location,0,0,1 --> Contains insulator.
>* CRM_location,1,1,0 --> Contains promoter and enhancer.
>* CRM_location,1,0,1 --> Contains promoter and insulator.
>* CRM_location,0,1,1 --> Contains enhancer and insulator.
>* CRM_location,1,1,1 --> Contains promoter, enhancer and insulator.

Output Plots :

Take X\_8305146_8307354 from the above input as an example.

The CRM is identified to have promoter and insulator functions. And the output plots for this CRM is in the subdirectory output/X\_8305146_8307354.

![](https://i.imgur.com/alaAbB8.png)

>* The SHAP value plots
>
![](https://i.imgur.com/pSYD7Un.png)
>* The standardized ChIP-seq score plots
>
![](https://i.imgur.com/FEazuim.png)
