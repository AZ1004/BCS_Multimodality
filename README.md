# Optimizing Performance and Interpretability in Multimodal Breast Cancer Screening using Late Fusion

This repository contains the implementation of a breast cancer screening model using late fusion techniques to integrate mammographic images and clinical patient data. The study employs deep learning for image analysis and classical classifiers for clinical data integration.

## Abstract

Early diagnosis and treatment of breast cancer have become essential to improve the cure rate and thus impact the incidence of attributable deaths. Therefore, establishing reliable screening methods is essential for the early diagnosis of breast cancer. This study proposes and evaluates late fusion architectures that integrate both mammographic images and clinical patient data for breast cancer screening. Nine deep learning models were employed for image analysis, and five classifiers were used for clinical data. Performance was assessed using classification metrics, statistical tests, and fivefold cross-validation.  Performance was assessed using classification metrics, statistical tests, and fivefold cross-validation. Interpretability of the best-performing late fusion model was explored using LIME and SHAP techniques. Results demonstrated the potential of combining deep learning on image data with classical classifiers on clinical data, with the DenseNet201 model paired with the KNN classifier emerging as the most effective combination. The interpretability highlighted the relevant clinical features known to be highly impactful on the model’s behaviour. This study not only enhances screening accuracy but also offers clinical insights, paving the way for potential generalization in computer-aided detection systems.
Keywords: Machine learning, Deep Learning, Late fusion, Interpretability, Performance, Breast cancer screening.

## Dataset

The main source of the data collection phase of this study was the Karolinska University Hospital, a renowned medical institution in Stockholm, Sweden. The dataset is available upon request from the Swedish National Data Service and is a result of leveraging medical records, patient histories, and diagnostic data available within the hospital's extensive database made through the Regional Cancer Center Stockholm-Gotland. Specifically, the focus was directed towards 1,103 cases of breast cancer that represented first-time diagnoses, occurring within the geographical catchment area of the Karolinska University Hospital. This catchment area was defined from late 2008, allowing us to include data from as far back as then, up to December 31, 2015.
In parallel with these cases, a control group was also included for comparison. 7,850 healthy controls were randomly selected from the general population in the Stockholm region, ensuring a balanced representation of the broader community. The examination of these healthy cases was conducted within a specific timeframe, commencing from May 6, 2008, and concluding on December 23, 2016. This selection process and time frame were meticulously chosen to provide a reliable basis for comparing the breast cancer cases with a healthy reference group.

### Dataset Reference:

K. Dembrower, P. Lindholm, and F. Strand, “A Multi-million Mammography Image Dataset and Population-Based Screening Cohort for the Training and Evaluation of Deep Neural Networks—the Cohort of Screen-Aged Women (CSAW),” J Digit Imaging, vol. 33, no. 2, pp. 408–413, Apr. 2020, doi: 10.1007/S10278-019-00278-0/FIGURES/2.

## Methods

1.	Metric Estimation: Using various metrics including accuracy, precision, recall, F1 Score and AUC, which are computed for all the models built on individual data modalities. These modalities encompass clinical patient data (utilizing KNN, DT, SVC, RF, ANN) and mammography data (with VGG16, VGG19, INCEPV3, DNET201, XCEP, INRENV2, MBNET, RNET50, NANET). Then, fusion models resulting from the combination of different single methods using aggregation modes (average, sum, max) for both data modalities are explored. In total we trained 135 fusion models, 9 deep learning image classification models and 5 clinical data classifiers. Moreover, a 5-fold cross-validation approach was applied.
2.	 Clustering Analysis: Clustering is performed on models constructed for each data modality and fusion models obtained through aggregation methods. Scott Knott's test of accuracy was utilized to identify the most suitable SK clusters for each data modality and fusion.
3.	Classification Selection: The best SK cluster models from each group of models, estimated on each data modality (clinical and image) and fusion variant (max, sum and average), were ranked by the Borda count method based on the five performance metrics. In total, we ranked 45 fusion models for each group of each of the three fusion aggregators (9 DL on image data * 5 ML on clinical data * 3 fusion aggregators). The two best models are selected for each data modality and aggregation method fusion.
4.	SK Test: The SK test is applied based on the accuracy of the best models obtained in step 3.  First for the DL models and the ML models each, where RF and DNET201 ranked on top. Then, for each aggregator, a separate SK test showed that the cluster containing DNET201 fused with KNN, DT, MLP and RF always ranked on top regardless of the aggregator. Lastly, another SK test of only the best clusters of the previous ones showed that DNET201 fused with KNN using the average aggregator was the best performing model overall.
5.	Final Classification: The best models from each aggregator are ranked using the Borda count method, based on the five chosen performance criteria: Accuracy, Precision, Recall, F1-score, and AUC.
6.	Interpretability: Once the evaluation of the classification performance was completed, the best late fusion model across all the aggregation methods is interpreted both locally and globally using LIME and SHAP techniques by breaking the model down to a DL model and a ML classifier. The results of LIME interpretation for the clinical data are evaluated using faithfulness and monotonicity as metrics.


## Results

The DenseNet201 model paired with the KNN classifier achieved:  
- Accuracy: 82.15%  
- AUC: 0.90  


## Citation

(Will be updated asap)

