```python
!pip3 install pyarrow
```

    Defaulting to user installation because normal site-packages is not writeable
    Collecting pyarrow
      Downloading pyarrow-17.0.0-cp310-cp310-manylinux_2_28_x86_64.whl.metadata (3.3 kB)
    Requirement already satisfied: numpy>=1.16.6 in /nexus/posix0/MAGE-flaski/service/posit/home/wangy/.jupyter/python/3.10/lib/python3.10/site-packages (from pyarrow) (1.24.3)
    Downloading pyarrow-17.0.0-cp310-cp310-manylinux_2_28_x86_64.whl (39.9 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m39.9/39.9 MB[0m [31m48.7 MB/s[0m eta [36m0:00:00[0m:00:01[0m00:01[0m
    [?25hInstalling collected packages: pyarrow
    Successfully installed pyarrow-17.0.0
    
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m A new release of pip is available: [0m[31;49m24.1.1[0m[39;49m -> [0m[32;49m24.2[0m
    [1m[[0m[34;49mnotice[0m[1;39;49m][0m[39;49m To update, run: [0m[32;49mpip install --upgrade pip[0m



```python
import wget
import pandas as pd
import numpy as np
import gzip
import shutil
import os
from pyarrow.parquet import ParquetFile
import pyarrow as pa
```


```python
# url = 'https://storage.googleapis.com/adult-gtex/bulk-gex/v8/rna-seq/GTEx_Analysis_2017-06-05_v8_STARv2.5.3a_junctions.gct.gz'

# output_directory = "/nexus/posix0/MAGE-flaski/service/projects/data/Adam_Antebi/AA_spliceosomics"
# filename = wget.download(url, out=output_directory)

# filename
# filenameunzip = filename.replace('.gz', '')

# with gzip.open(filename, 'rb') as f_in:
#     with open(filenameunzip, 'wb') as f_out:
#         shutil.copyfileobj(f_in, f_out)
```


```python
output_directory = "/nexus/posix0/MAGE-flaski/service/projects/data/Adam_Antebi/AA_spliceosomics/"
filenameunzip = output_directory + "GTEx_Analysis_2017-06-05_v8_STARv2.5.3a_junctions.gct"

df=pd.read_csv(filenameunzip, skiprows=2, nrows=10, sep="\t")
```


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Description</th>
      <th>GTEX-1117F-0226-SM-5GZZ7</th>
      <th>GTEX-1117F-0426-SM-5EGHI</th>
      <th>GTEX-1117F-0526-SM-5EGHJ</th>
      <th>GTEX-1117F-0626-SM-5N9CS</th>
      <th>GTEX-1117F-0726-SM-5GIEN</th>
      <th>GTEX-1117F-1326-SM-5EGHH</th>
      <th>GTEX-1117F-2426-SM-5EGGH</th>
      <th>GTEX-1117F-2526-SM-5GZY6</th>
      <th>...</th>
      <th>GTEX-ZZPU-1126-SM-5N9CW</th>
      <th>GTEX-ZZPU-1226-SM-5N9CK</th>
      <th>GTEX-ZZPU-1326-SM-5GZWS</th>
      <th>GTEX-ZZPU-1426-SM-5GZZ6</th>
      <th>GTEX-ZZPU-1826-SM-5E43L</th>
      <th>GTEX-ZZPU-2126-SM-5EGIU</th>
      <th>GTEX-ZZPU-2226-SM-5EGIV</th>
      <th>GTEX-ZZPU-2426-SM-5E44I</th>
      <th>GTEX-ZZPU-2626-SM-5E45Y</th>
      <th>GTEX-ZZPU-2726-SM-5NQ8O</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>chr1_12058_12178</td>
      <td>ENSG00000223972.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>chr1_12228_12612</td>
      <td>ENSG00000223972.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>chr1_12698_12974</td>
      <td>ENSG00000223972.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>chr1_12722_13220</td>
      <td>ENSG00000223972.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>chr1_13053_13220</td>
      <td>ENSG00000223972.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>chr1_13375_13452</td>
      <td>ENSG00000223972.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>chr1_14502_15004</td>
      <td>ENSG00000227232.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>chr1_15039_15795</td>
      <td>ENSG00000227232.5</td>
      <td>10</td>
      <td>8</td>
      <td>8</td>
      <td>9</td>
      <td>3</td>
      <td>8</td>
      <td>7</td>
      <td>23</td>
      <td>...</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>chr1_15948_16606</td>
      <td>ENSG00000227232.5</td>
      <td>20</td>
      <td>7</td>
      <td>14</td>
      <td>17</td>
      <td>8</td>
      <td>18</td>
      <td>14</td>
      <td>34</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>chr1_16766_16857</td>
      <td>ENSG00000227232.5</td>
      <td>2</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>10</td>
      <td>3</td>
      <td>4</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>7</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 17384 columns</p>
</div>




```python
# url = 'https://storage.googleapis.com/adult-gtex/bulk-gex/v8/rna-seq/GTEx_Analysis_2017-06-05_v8_RNASeQCv1.1.9_exon_reads.parquet'

# output_directory = "/nexus/posix0/MAGE-flaski/service/projects/data/Adam_Antebi/AA_spliceosomics"
# filename = wget.download(url, out=output_directory)

```


```python
filename = output_directory + "GTEx_Analysis_2017-06-05_v8_RNASeQCv1.1.9_exon_reads.parquet"
pf = ParquetFile(filename) 
first_ten_rows = next(pf.iter_batches(batch_size = 10)) 
df2 = pa.Table.from_batches([first_ten_rows]).to_pandas() 
```


```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Description</th>
      <th>GTEX-1117F-0226-SM-5GZZ7</th>
      <th>GTEX-1117F-0426-SM-5EGHI</th>
      <th>GTEX-1117F-0526-SM-5EGHJ</th>
      <th>GTEX-1117F-0626-SM-5N9CS</th>
      <th>GTEX-1117F-0726-SM-5GIEN</th>
      <th>GTEX-1117F-1326-SM-5EGHH</th>
      <th>GTEX-1117F-2426-SM-5EGGH</th>
      <th>GTEX-1117F-2526-SM-5GZY6</th>
      <th>GTEX-1117F-2826-SM-5GZXL</th>
      <th>...</th>
      <th>GTEX-ZZPU-1126-SM-5N9CW</th>
      <th>GTEX-ZZPU-1226-SM-5N9CK</th>
      <th>GTEX-ZZPU-1326-SM-5GZWS</th>
      <th>GTEX-ZZPU-1426-SM-5GZZ6</th>
      <th>GTEX-ZZPU-1826-SM-5E43L</th>
      <th>GTEX-ZZPU-2126-SM-5EGIU</th>
      <th>GTEX-ZZPU-2226-SM-5EGIV</th>
      <th>GTEX-ZZPU-2426-SM-5E44I</th>
      <th>GTEX-ZZPU-2626-SM-5E45Y</th>
      <th>GTEX-ZZPU-2726-SM-5NQ8O</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ENSG00000223972.5_1</th>
      <td>DDX11L1</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>ENSG00000223972.5_2</th>
      <td>DDX11L1</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.855263</td>
    </tr>
    <tr>
      <th>ENSG00000223972.5_3</th>
      <td>DDX11L1</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>ENSG00000223972.5_4</th>
      <td>DDX11L1</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.144737</td>
    </tr>
    <tr>
      <th>ENSG00000227232.5_1</th>
      <td>WASH7P</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>ENSG00000227232.5_2</th>
      <td>WASH7P</td>
      <td>1.000000</td>
      <td>18.460526</td>
      <td>8.394737</td>
      <td>23.868422</td>
      <td>0.000000</td>
      <td>9.078947</td>
      <td>5.894737</td>
      <td>5.605263</td>
      <td>13.447369</td>
      <td>...</td>
      <td>7.381579</td>
      <td>12.276316</td>
      <td>9.644737</td>
      <td>6.368421</td>
      <td>8.828947</td>
      <td>11.592105</td>
      <td>7.171053</td>
      <td>19.131578</td>
      <td>5.960526</td>
      <td>6.671053</td>
    </tr>
    <tr>
      <th>ENSG00000227232.5_3</th>
      <td>WASH7P</td>
      <td>1.197368</td>
      <td>8.460526</td>
      <td>6.960526</td>
      <td>11.684211</td>
      <td>1.539474</td>
      <td>4.907895</td>
      <td>1.868421</td>
      <td>32.184212</td>
      <td>18.539474</td>
      <td>...</td>
      <td>5.144737</td>
      <td>4.697368</td>
      <td>3.118421</td>
      <td>4.513158</td>
      <td>5.868421</td>
      <td>5.947368</td>
      <td>4.368421</td>
      <td>7.763158</td>
      <td>2.789474</td>
      <td>5.171053</td>
    </tr>
    <tr>
      <th>ENSG00000227232.5_4</th>
      <td>WASH7P</td>
      <td>13.710526</td>
      <td>8.828947</td>
      <td>9.960526</td>
      <td>25.052631</td>
      <td>4.815789</td>
      <td>6.184211</td>
      <td>14.947368</td>
      <td>40.921055</td>
      <td>21.565788</td>
      <td>...</td>
      <td>5.421053</td>
      <td>6.026316</td>
      <td>12.144737</td>
      <td>7.697368</td>
      <td>7.526316</td>
      <td>8.921053</td>
      <td>4.842105</td>
      <td>10.184211</td>
      <td>3.486842</td>
      <td>8.236842</td>
    </tr>
    <tr>
      <th>ENSG00000227232.5_5</th>
      <td>WASH7P</td>
      <td>23.328947</td>
      <td>4.526316</td>
      <td>15.078947</td>
      <td>33.473682</td>
      <td>17.052631</td>
      <td>12.500000</td>
      <td>34.407894</td>
      <td>48.473682</td>
      <td>34.250000</td>
      <td>...</td>
      <td>5.013158</td>
      <td>19.934212</td>
      <td>29.223684</td>
      <td>11.328947</td>
      <td>11.815789</td>
      <td>10.894737</td>
      <td>4.065789</td>
      <td>13.500000</td>
      <td>5.355263</td>
      <td>7.078947</td>
    </tr>
    <tr>
      <th>ENSG00000227232.5_6</th>
      <td>WASH7P</td>
      <td>20.763159</td>
      <td>5.723684</td>
      <td>17.144737</td>
      <td>23.986841</td>
      <td>13.105263</td>
      <td>16.026316</td>
      <td>22.578947</td>
      <td>54.618420</td>
      <td>33.039474</td>
      <td>...</td>
      <td>12.881579</td>
      <td>13.855263</td>
      <td>21.578947</td>
      <td>15.657895</td>
      <td>14.118421</td>
      <td>12.552632</td>
      <td>5.907895</td>
      <td>11.092105</td>
      <td>2.460526</td>
      <td>11.960526</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 17383 columns</p>
</div>




```python
# histo=pd.read_csv(output_directory + "GTEx Portal.csv")

# histo

# df2_columns=df2.columns.str.replace(r'-SM.*', '', regex=True)

# sum(df2_columns.isin(histo['Tissue Sample ID']))

# df2_columns

# not_matching = df2_columns[~df2_columns.isin(histo['Tissue Sample ID'])]
# not_matching
```


```python
meta=pd.read_csv(output_directory + "GTEx_Analysis_v8_Annotations_SampleAttributesDS.txt",sep='\t')
meta
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SAMPID</th>
      <th>SMATSSCR</th>
      <th>SMCENTER</th>
      <th>SMPTHNTS</th>
      <th>SMRIN</th>
      <th>SMTS</th>
      <th>SMTSD</th>
      <th>SMUBRID</th>
      <th>SMTSISCH</th>
      <th>SMTSPAX</th>
      <th>...</th>
      <th>SME1ANTI</th>
      <th>SMSPLTRD</th>
      <th>SMBSMMRT</th>
      <th>SME1SNSE</th>
      <th>SME1PCTS</th>
      <th>SMRRNART</th>
      <th>SME1MPRT</th>
      <th>SMNUM5CD</th>
      <th>SMDPMPRT</th>
      <th>SME2PCTS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GTEX-1117F-0003-SM-58Q7G</td>
      <td>NaN</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Blood</td>
      <td>Whole Blood</td>
      <td>0013756</td>
      <td>1188.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GTEX-1117F-0003-SM-5DWSB</td>
      <td>NaN</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Blood</td>
      <td>Whole Blood</td>
      <td>0013756</td>
      <td>1188.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GTEX-1117F-0003-SM-6WBT7</td>
      <td>NaN</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Blood</td>
      <td>Whole Blood</td>
      <td>0013756</td>
      <td>1188.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GTEX-1117F-0011-R10a-SM-AHZ7F</td>
      <td>NaN</td>
      <td>B1, A1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Brain</td>
      <td>Brain - Frontal Cortex (BA9)</td>
      <td>0009834</td>
      <td>1193.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GTEX-1117F-0011-R10b-SM-CYKQ8</td>
      <td>NaN</td>
      <td>B1, A1</td>
      <td>NaN</td>
      <td>7.2</td>
      <td>Brain</td>
      <td>Brain - Frontal Cortex (BA9)</td>
      <td>0009834</td>
      <td>1193.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>22946</th>
      <td>K-562-SM-E9EZC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>26289400.0</td>
      <td>27814300.0</td>
      <td>0.002441</td>
      <td>26121600.0</td>
      <td>49.8400</td>
      <td>0.006370</td>
      <td>0.995167</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2621</td>
    </tr>
    <tr>
      <th>22947</th>
      <td>K-562-SM-E9EZI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>26653800.0</td>
      <td>28341700.0</td>
      <td>0.002336</td>
      <td>26553400.0</td>
      <td>49.9056</td>
      <td>0.006806</td>
      <td>0.994802</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2046</td>
    </tr>
    <tr>
      <th>22948</th>
      <td>K-562-SM-E9EZO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>14317500.0</td>
      <td>15168000.0</td>
      <td>0.001731</td>
      <td>14163500.0</td>
      <td>49.7298</td>
      <td>0.006662</td>
      <td>0.994935</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2412</td>
    </tr>
    <tr>
      <th>22949</th>
      <td>K-562-SM-E9EZT</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>25459900.0</td>
      <td>26906500.0</td>
      <td>0.002130</td>
      <td>25259100.0</td>
      <td>49.8020</td>
      <td>0.007145</td>
      <td>0.994828</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2529</td>
    </tr>
    <tr>
      <th>22950</th>
      <td>K-562-SM-E9EZZ</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>22341200.0</td>
      <td>23740600.0</td>
      <td>0.001867</td>
      <td>22232600.0</td>
      <td>49.8781</td>
      <td>0.006861</td>
      <td>0.993576</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2929</td>
    </tr>
  </tbody>
</table>
<p>22951 rows × 63 columns</p>
</div>




```python
sum(df2.columns.isin(meta['SAMPID'])) 
```




    17382




```python
age=pd.read_csv(output_directory + "GTEx_Analysis_v8_Annotations_SubjectPhenotypesDS.txt",sep='\t')
age
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SUBJID</th>
      <th>SEX</th>
      <th>AGE</th>
      <th>DTHHRDY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GTEX-1117F</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GTEX-111CU</td>
      <td>1</td>
      <td>50-59</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GTEX-111FC</td>
      <td>1</td>
      <td>60-69</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GTEX-111VG</td>
      <td>1</td>
      <td>60-69</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GTEX-111YS</td>
      <td>1</td>
      <td>60-69</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>975</th>
      <td>GTEX-ZYY3</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>976</th>
      <td>GTEX-ZZ64</td>
      <td>1</td>
      <td>20-29</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>977</th>
      <td>GTEX-ZZPT</td>
      <td>1</td>
      <td>50-59</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>978</th>
      <td>GTEX-ZZPU</td>
      <td>2</td>
      <td>50-59</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>979</th>
      <td>K-562</td>
      <td>2</td>
      <td>50-59</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>980 rows × 4 columns</p>
</div>




```python
meta['g1'] = meta['SAMPID'].str.split('-', n=2, expand=True)[0]
meta['g2'] = meta['SAMPID'].str.split('-', n=2, expand=True)[1]
meta['SAMP_Group'] =  meta[['g1', 'g2']].agg('-'.join, axis=1)
```


```python
meta=pd.merge(meta,age,left_on=["SAMP_Group"],right_on="SUBJID", how="left")
meta
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SAMPID</th>
      <th>SMATSSCR</th>
      <th>SMCENTER</th>
      <th>SMPTHNTS</th>
      <th>SMRIN</th>
      <th>SMTS</th>
      <th>SMTSD</th>
      <th>SMUBRID</th>
      <th>SMTSISCH</th>
      <th>SMTSPAX</th>
      <th>...</th>
      <th>SMNUM5CD</th>
      <th>SMDPMPRT</th>
      <th>SME2PCTS</th>
      <th>SAMP_Group</th>
      <th>g1</th>
      <th>g2</th>
      <th>SUBJID</th>
      <th>SEX</th>
      <th>AGE</th>
      <th>DTHHRDY</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>GTEX-1117F-0003-SM-58Q7G</td>
      <td>NaN</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Blood</td>
      <td>Whole Blood</td>
      <td>0013756</td>
      <td>1188.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>GTEX-1117F</td>
      <td>GTEX</td>
      <td>1117F</td>
      <td>GTEX-1117F</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>GTEX-1117F-0003-SM-5DWSB</td>
      <td>NaN</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Blood</td>
      <td>Whole Blood</td>
      <td>0013756</td>
      <td>1188.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>GTEX-1117F</td>
      <td>GTEX</td>
      <td>1117F</td>
      <td>GTEX-1117F</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>GTEX-1117F-0003-SM-6WBT7</td>
      <td>NaN</td>
      <td>B1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Blood</td>
      <td>Whole Blood</td>
      <td>0013756</td>
      <td>1188.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>GTEX-1117F</td>
      <td>GTEX</td>
      <td>1117F</td>
      <td>GTEX-1117F</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>GTEX-1117F-0011-R10a-SM-AHZ7F</td>
      <td>NaN</td>
      <td>B1, A1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Brain</td>
      <td>Brain - Frontal Cortex (BA9)</td>
      <td>0009834</td>
      <td>1193.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>GTEX-1117F</td>
      <td>GTEX</td>
      <td>1117F</td>
      <td>GTEX-1117F</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>GTEX-1117F-0011-R10b-SM-CYKQ8</td>
      <td>NaN</td>
      <td>B1, A1</td>
      <td>NaN</td>
      <td>7.2</td>
      <td>Brain</td>
      <td>Brain - Frontal Cortex (BA9)</td>
      <td>0009834</td>
      <td>1193.0</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>GTEX-1117F</td>
      <td>GTEX</td>
      <td>1117F</td>
      <td>GTEX-1117F</td>
      <td>2</td>
      <td>60-69</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>22946</th>
      <td>K-562-SM-E9EZC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2621</td>
      <td>K-562</td>
      <td>K</td>
      <td>562</td>
      <td>K-562</td>
      <td>2</td>
      <td>50-59</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22947</th>
      <td>K-562-SM-E9EZI</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2046</td>
      <td>K-562</td>
      <td>K</td>
      <td>562</td>
      <td>K-562</td>
      <td>2</td>
      <td>50-59</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22948</th>
      <td>K-562-SM-E9EZO</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2412</td>
      <td>K-562</td>
      <td>K</td>
      <td>562</td>
      <td>K-562</td>
      <td>2</td>
      <td>50-59</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22949</th>
      <td>K-562-SM-E9EZT</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2529</td>
      <td>K-562</td>
      <td>K</td>
      <td>562</td>
      <td>K-562</td>
      <td>2</td>
      <td>50-59</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>22950</th>
      <td>K-562-SM-E9EZZ</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Bone Marrow</td>
      <td>Cells - Leukemia cell line (CML)</td>
      <td>EFO_0002067</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>50.2929</td>
      <td>K-562</td>
      <td>K</td>
      <td>562</td>
      <td>K-562</td>
      <td>2</td>
      <td>50-59</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>22951 rows × 70 columns</p>
</div>




```python

```
