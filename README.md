# Predictors for Resource Overcommitment
This repository contains the code that tests various proposed predictors for resource overcommitment. 

### Predictors

* __Borg__. Google’s cluster manager, called Borg, assumes that a fixed percentage of 10% of the resources are overcommited at all times. According to this simple policy, it is expected that all tasks use the 90% of their user-defined limits.
* __Resource Central (RC-like)__. Microsoft Azure’s resource management system also uses a simple strategy and predicts the sum of the k-th percentile as future resource usage. We use the 99%ile, as it is shown to yield good performance.
* __N-Sigma__. A Gaussian distribution can sufficiently approximate the resource usage patterns at the machine level, as validated by various practical systems. The prediction of N-Sigma is U+N*std(U), where U is the average resource usage across time for a certain task and std(U) is its standard deviation. The variable N denotes how many times the standard deviation is extended or compressed to predict where most of the data lies in the normal distribution. Most commonly N = 5.
* __Take it to the Limit (TITTL)__. This is a conservative resource overcommitment approach that Google recently proposed. The prediction at every timestep is the maximum of the outputs of the three above predictors. They opt for the maximum value, often overestimating resource usage, to guarantee the availability of the user requested resources.

### Dataset

The __Google Cluster Workload Traces__ is a public dataset that captures information on resource usage over time for tasks executing over physical machines. Resource usage is measured every 5 minutes across several days of execution. In addition, it contains the user-defined limits per type of resource at the task-level. Our analysis focuses on the CPU usage. The CPU measurements are normalized and scaled against the machine with the largest capacity, thus their values can appear to be quite low within the (0, 1) range. Since the size of the complete dataset is massive, we focus our analysis at cell A, where a cell is a set of physical machines in Google’s datacenter.

### Simulator

Google has open-sourced a simulator originally proposed in the paper __Take it to the Limit__. This simulator mimics Google’s production environment and allows the configuration of different task execution scenarios and the implementation of various predictors. The input of the simulator is the aforementioned dataset, while the output is the predicted resource usage time series.

## Repository Structure <br />



## Paper Reference <br />
Georgia Christofidi and Thaleia Dimitra Doudali. 2024. <br /><br /> __Do Predictors for Resource Overcommitment Even Predict?__ <br /><br />  In 4th Workshop on Machine Learning and Systems (EuroMLSys ’24), April 22, 2024, Athens, Greece. <br /> <br /> 

## Licence <br />
The MIT License (MIT).
 
## Acknowledgements <br />
This work is part of the grants FJC2021-047102-I, TED2021-132464B-I00, PID2022-142290OB-I00, funded by the European Union «NextGenerationEU»/PRTR, the ESF+ and MCIN/AEI/10.13039/501100011033. <br />  <br /> 
<img src="docs/images/micin-financiadoUEnextgeneration-prtr-aei-1.png" width="1000"/>


