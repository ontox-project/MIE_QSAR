# IN SILICO MODELING OF BIOACTIVITY TOWARD PROTEINS ASSOCIATED TO MOLECULAR INITIATING EVENTS OF ORGAN-SPECIFIC TOXICITY USING QUANTITATIVE STRUCTURE-ACTIVITY RELATIONSHIPS

Implementation of Quantitative-Strucure activity relationship (QSAR) models predicting chemicals bioactivity towards proteins associated to molecular initiating events (MIE) of hepatic steatosis, cholestasis, cognitive functional defects, neural tube closure and kidney failure. 

## TECHNICAL DETAILS

### DATA SOURCE
1. Bioactivity data from ChEMBL 34 were curated following a protocol adapted from Bosc et al. (2019) (doi: 10.1186/s13321-018-0325-4).
2. Only records representing measures of half-maximal responses (molar IC50, XC50, EC50, AC50, Ki, Kd, potency and ED50) expressed on a negative logarithmic scale were aggregated.
3. Records with no potential duplicates, flagged with no 'Data Validity Comment', and not classified as 'inconclusive,' 'undetermined,' or 'not determined' were considered.
4. Records were classified into active and inactives based on information reported in the ‘Standard Relation’ and a ‘Standard Value’ fields and based on a threshold of 10,000 nM.
5. The following protein targets associated to relevant MIEs were modeled:

- **Liver steatosis (STE)**: aryl hydrocarbon receptor (AHR), pregnane X receptor (PXR), peroxisome proliferator activated receptor alpha (PPARα) and gamma (PPARγ).
- **Cholestasis (CHO)**: bile salt export pump (BSEP), multidrug resistance-associated protein isoform 4 (MRP4)
- **Kidney failure (KF)**: cycloxigenase 1 (COX1), angiotensin converting enzyme (ACE) and angiotensin II receptor type 1 (AT1R).
- **Neural tube closure (NTD)**: histone deacetylase (HDeac), cytochrome P450 26A1 (CYP26) fibroblast growth factors (FGF), bone morphogenetic proteins (BMP) fibroblast growth factor receptor isoform 1 (FGFR1), isoform 2 (FGFR2), isoform 3 (FGFR3), isoform 4 (FGFR4).
- **Cognitive function defects (CFD)**: acetylcholinesterase (ACHE) N-methyl-d-aspartic acid receptor (NMDA), transthyretin (TTR), thyroid hormone receptors alpha (THRα) and beta (THRß), voltage gate sodium channels (VGSC).

### QSAR DETAILS
Various independent variables, machine learning methods, and associated parameters were compared to develop QSARs from the collected data.

1. **Independent variables**: extended structural fingerprints, DRAGON descriptors, CDDD descriptors (https://github.com/jrwnter/cddd)
2. **Machine Learning Methods**: Randome Forests, k-nearest neighbors, multi.layer perceptron, support vector machine, gradient boosting, extreme graxient boosting.
3. **Adressing Imbalance**: Synthetic Minority Oversampling Technique (SMOTE) (doi.org/10.1613/jair.953), balanced random forests.
3. **Variable selection**: VSURF (10.1016/j.patrec.2010.03.014)

## HOW TO USE THE MODELS

### PYTHON ENVIRONMENTS INSTALLATION
1. Python 3 should be installed.
2. CDDD should be installed following the instruction in https://github.com/jrwnter/cddd
3. To run the model, a Python environment should be created with the following packages. A default environment (mie_knime_env) including the required dependencies is available in this GitHub repository

```
pypmml==0.9.17
scikit-learn==1-5-1
xgboost==2.1.0
```

### DRAGON LICENCE
1. *The user has a Dragon licence:* download the Dragon node provided in this GitHub repository. The node can be installed by copy-pasting the downloaded file in the "dropins" folder in the installation directory of KNIME.
2. *The user does not have a Dragon licence*: Load the spreadsheet with SMILES including additional columns with descriptors calculated previously in the input metanode.

### SETTING PREFERENCES
1. **Load input data**
a. Load the data to predict in .txt, .smi or .csv format in the metanode "Select data to predict". The file should include columns with the SMILES list ('SMILES') and the identifiers ('ID'). The coulmns should include headers.
b. Specify the ID and SMILES columns from the metanode "Select columns" metanode.

3. **Calculate descriptors**
c. Dragon descriptors: Specify if a Dragon licence is available in the corresponding metanode. If yes, specify the location of the DRAGON executable (usually C:\Program Files (x86)\Dragon 7\dragon7shell.exe).
d. CDDD: Specify the column including the smiles from the drop-down menu and the location of the cddd python environment previously created as explained in in https://github.com/jrwnter/cddd

5. **Run models**
a. Specify the python environments previously creates (by default is mie_knime_env 
b. Specify if DRAGON models should be used. If the user does not have neither a DRAGON licence or precalculated descriptors, this option should be not active.

## REFERENCE
Further details on the algorithms and on the statistical performance of models can be found in the reference pubblication:

*Gadaleta D, Garcia de Lomana M, Serrano Candelas E, Ortega Vallbona R, Gozalbes R, Roncaglioni A, Benfenati E. In silico Modeling of Bioactivity toward Proteins associated to Molecular Initiating Events of Organ-Specific Toxicity Using Quantitative Structure-Activity Relationships. Submitted manuscript.*

## CONTACT
Domenico Gadaleta, PhD
Laboratory of Environmental Chemistry and Toxicology
Department of Environmental Health Sciences
Istituto di Ricerche Farmacologiche Mario Negri IRCCS 
Via Mario Negri 2, 20156 Milano, Italy 
e-mail: domenico.gadaleta@marionegri.it
