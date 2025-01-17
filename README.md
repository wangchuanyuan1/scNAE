# scNAE: Network activity evaluation reveals significant gene regulatory architectures during SARS-CoV-2 viral infec-tion from dynamic scRNA-seq data #


**scNAE will be detailed if the manuscript is accepted!**

**Please write to [zpliu@sdu.edu.cn](mailto:zpliu@sdu.edu.cn) if you have any questions.**

**Please cite our paper if it helps you.**

![workfolw](https://github.com/zpliulab/scNAE/blob/main/Supplementary/single%20cell.jpg)

Computer Environment [![MATLAB](https://img.shields.io/badge/MATLAB-R2022a-green.svg "MATLAB")](https://ww2.mathworks.cn/products/matlab.html "MATLAB"):
-
- MATLAB R2022a (requires Parallel Computing Toolbox installed)
- If your working environment cannot enable parallel pooling, please replace *parfor* with *for*


## Files:
- **code: subfunction used in the scNAE process.**
- **data: All processed SARS-CoV-2 data are divided according to pathways, including original values, differential values and networks.Please unzip before use it.**
- **result: save results.**
- **simu_data: simulation datasets.** (Note that "simu_data_302.mat" in the simulated data is assumed to have 30 genes and 2 cell clusters. Other data are named similarly.)
- **Supplementary**
- **demo.m: run the simulation example**
- **demo_SARS.m: run the SARS-CoV-2 example**
  
## Run the code
Run the following code in the Matlab environment
- demo.m 
- demo_SARS.m
  
## Use scNAE on a new dataset

The core interface function of scNAE is code\refer_scNAE.m

```[newgra,obj,opt] = refer_scNAE(data,network,Lp,parameter);```

	Input:
	  data : A structure variable containing the original value and the differential value, 
   		 *data.orig* represents the gene expression profile of the time series; 
      		 *data.fit* represents the corresponding differential value;
	  network:   An (m*m) adjacency matrix
	  Lp:   the Lp-norm type used, p can be selected {0, 0~1, 2}
      parameter： *parameter* is a structure, where 'parameter.i' is the regularization parameter that must be set., e.g: parameter.i=1e-6 ~ 1e2
      
	Output:
	 newgra: Reconstructed adjacency matrix.
     obj: The loss value generated by each iteration (used to calculate p-value)
     opt: optimal parameters
     
## Data preprocessing tips
Given a single-cell gene expression profile, we recommend using the standard workflows of Seurat (in R) or Scanpy (in Python) algorithms for data preprocessing. Utilize the FindClusters function (in Seurat) or leiden (in Scanpy) to cluster cell types. Additionally, exporting marker genes can provide specific information about each cell type. These steps constitute a common procedure for single-cell data analysis, and we adhere to this practice, suggesting readers do the same. 

For pre-processed single-cell data, there may be some inherent errors in cell type that are unavoidable. To minimize the impact of cells misclassified on the overall workflow, we recommend retaining only cells within 10% of the distance from the centroid. We achieve this using the kmeans algorithm based on Euclidean distance.
