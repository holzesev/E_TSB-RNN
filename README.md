# Detecting Errors in Databases with Bidirectional Recurrent Neural Networks
Code for SDS2021 accepted [paper](https://arxiv.org/pdf/1905.08205.pdf).

## Abstract
In recent years we have seen an exponential growth of data. However, not only does the volume of data grow but often also the numbers of erroneous data values. Detecting and cleaning these errors is an important data management problem to enable high quality data science pipelines. To reduce the human effort and to achieve good results in detecting errors, it is important to label the tuples which give the best impact for the error detection system.
In this paper we introduce an architecture based on bidirectional recurrent neural networks to detect errors in databases. The experimental results with 6 different datasets demonstrate that our approach shows similar performance to state-of-the-art error detection system per dataset. When considering the average of the F1-scores over all datasets, our approach called Enriched Two-Stacked Bidirectional (ETSB-RNN) outperforms state-of-the-art systems. Moreover, our approach achieves a lower standard deviation than existing work, which shows that our system is more robust.
In addition, our approach uses simpler machine learning algorithms that are faster to train. Depending on the dataset, our approach needs between less than one minute until 5 minutes for training for the benchmark datasets. Finally, our approach does not require additional data augmentation techniques to achieve high F1-scores. The system does not need any configuration or previous analysis of the data.

## Data Preparation
First we have to prepare the data so that we can produce a trainand testset, which in turn can be fed into a neural network to detect errors in the dataset and measure the results.
<p align='center'>
  <img src='https://github.com/holzesev/E_TSB-RNN/blob/main/images/datapreparation.PNG' width="100%"/>
</p>

## Algorithms for Trainset Selection (DiverSet)
The intuition is to select tuples with values that have not been seen previously. In other words, the newly select tuples increase the information content of our trainset
the most. In case two candidate tuples contain the same number of unseen attribute values, the tuple with the highest number of empty attribute values is chosen. Our hypothesis is that empty values give us more information for the system to learn – because if there are empty values in other attributes, we can learn if they should be empty or not. In case all candidate tuples have the same number of unseen attributes and empty attribute values, the tuples are choosing randomly.
<p align='center'>
  <img src='https://github.com/holzesev/E_TSB-RNN/blob/main/images/Algo3vis.PNG' width="30%"/>
</p>

## Neural Network Architectures
The main difference between the two architecture models is that the first model Two-Stacked Bidirectional RNN (TSB-RNN) receives input from one dataset (value_x, i.e. the actual data values), while the second model Enriched Two-Stacked Bidirectional
RNN (ETSB-RNN) receives input from three datasets (value_x, i.e. the actual data values, length_norm, i.e. the standardized length of value_x, as well as metadata information about the attributes). Therefore, the second model is more complex and needs more time for training

* TSB-RNN: Two-Stacked Bidirectional RNN
* ETSB-RNN: Enriched Two-Stacked Bidirectional RNN
<p align='center'>
  <img src='https://github.com/holzesev/E_TSB-RNN/blob/main/images/model_0_1.PNG' width="70%"/>
</p>

## Results (F1-Score)
| **Name**   | AVG (ex. Flights) | S.D. | AVG (inc. Flights) | S.D. |
| - | - | - | - | - |
| Raha      | 0.85 | 0.08 | 0.85 | 0.07 |
| Rotom     | 0.90 | 0.10 | n/a | n/a |
| Rotom+SSL | 0.86 | 0.17 | n/a | n/a |
| TSB-RNN   | 0.89 | 0.06 | 0.85 | 0.08 |
| ETSB-RNN  | **0.91** | 0.05 | **0.88** | 0.06 |

## Citation

```
@inproceedings{GuoIRNet2019,
  author={Jiaqi Guo and Zecheng Zhan and Yan Gao and Yan Xiao and Jian-Guang Lou and Ting Liu and Dongmei Zhang},
  title={Towards Complex Text-to-SQL in Cross-Domain Database with Intermediate Representation},
  booktitle={Proceeding of the 57th Annual Meeting of the Association for Computational Linguistics (ACL)},
  year={2019},
  organization={Association for Computational Linguistics}
}
```
