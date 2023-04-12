# Table of Contents

- [Table of Contents](#table-of-contents)
- [Reviewer p7r1](#reviewer-p7r1)
    - [Weakness #1: Clarification](#weakness-1-clarification)
    - [Question #1: Problem Definition](#question-1-problem-definition)
    - [Question #2: On topology manipulations and aggregators](#question-2-on-topology-manipulations-and-aggregators)
- [Reviewer aakq](#reviewer-aakq)
    - [Weakness #1: How does our methodology alleviates class imbalance](#weakness-1-how-does-our-methodology-alleviates-class-imbalance)
    - [Weakness #2 \& Question #2: Related Works](#weakness-2--question-2-related-works)
    - [Weakness #3: Format](#weakness-3-format)
    - [Question #1: Novelty](#question-1-novelty)
- [Reviewer ZyGi](#reviewer-zygi)
    - [Weakness #1: GraphSMOTE \& GraphENS results in Figure 1](#weakness-1-graphsmote--graphens-results-in-figure-1)
    - [Weakness #2: Effectiveness of ambivalent and distant message-passing](#weakness-2-effectiveness-of-ambivalent-and-distant-message-passing)
    - [Weakness #3: Relationship with TAM](#weakness-3-relationship-with-tam)
    - [Weakness #4: Ambivalent message-passing and homophily assumption](#weakness-4-ambivalent-message-passing-and-homophily-assumption)
    - [Weakness #5: Unsteady results?](#weakness-5-unsteady-results)
    - [Weakness #6: Extreme class imbalance](#weakness-6-extreme-class-imbalance)
    - [Weakness #7: Natural class imbalance](#weakness-7-natural-class-imbalance)
- [Reviewer KB6H](#reviewer-kb6h)
    - [Weakness #1: On the high-risk but correct prediction](#weakness-1-on-the-high-risk-but-correct-prediction)
    - [Weakness #2: Early stage of training](#weakness-2-early-stage-of-training)
    - [Weakness #3: Mild class imbalance](#weakness-3-mild-class-imbalance)
    - [Quesiton #1: Using variance in Eq. (7)](#quesiton-1-using-variance-in-eq-7)
    - [Quesiton #2: Micro-averaged metrics](#quesiton-2-micro-averaged-metrics)


# Reviewer p7r1

We appreciate for your thoughtful review as well as the time and effort you have taken to evaluate our work. We have carefully considered your comments and criticisms, please see our itermized responses to each of your concerns:

### Weakness #1: Clarification

Thank you for your valuable comment. We apologize for any confusion that may have arisen and assure you that we will carefully revise this section. We would like to stress that all the techniques mentioned in our work have demonstrated significant success in addressing the heterophilic link/long-distance propagation problem in graph learning. However, while this issue has a considerable impact on the performance and bias of class-imbalanced graph learning models, we are unaware of any work that explicitly explores the relationship and interplay between the widely-discussed heterophilic link/long-distance propagation challenges and the class imbalance problem.

### Question #1: Problem Definition

We apologize for the confusion, we will provide further clarification regarding the problem setting in the abstract to prevent any potential ambiguities.

### Question #2: On topology manipulations and aggregators

Thank you for your insightful suggestion. We find this a very interesting direction to be explored. 

- **Observation & discussion:** Regarding our work, we considered three GNN architectures (GCN, GAT, and GraphSAGE) with varying aggregation functions (e.g., mean, max, attention-based) and evaluated their performance on several IGL tasks. Our experiments revealed that compared to the performance gain from imbalance handling techniques (e.g., GraphSMOTE, GraphENS, GBA), the difference in performance between different GNNs/aggregators was relatively small. There is no single GNN/aggregator proved universally superior for IGL tasks. Nevertheless, GBA consistently improved the performance of various GNNs regardless of the message aggregator used, which is expected given its model-agnostic nature.
- **Future directions:** Looking to the future, we believe that exploring the joint influence of message aggregators and topology manipulation in IGL holds significant promise. This could lead to the development of (1) more intelligent graph augmentation methods that can adapt to different aggregators, or even (2) class-imbalance-aware aggregators that can directly mitigate the class-imbalance bias in message-passing. We consider this to be an important direction for our future work.

Thank you once again for your feedback, and please let us know if you have any further questions or concerns.


# Reviewer aakq

We appreciate for your thoughtful review as well as the time and effort you have taken to evaluate our work. We have carefully considered your comments and criticisms, please see our itermized responses to each of your concerns:

### Weakness #1: How does our methodology alleviates class imbalance

We apologize for any confusion that may have arisen and would like to provide a brief clarification.

**Problem Definition:**

The problem addressed in our work is the *class imbalance* problem in transductive node classification. *Topology imbalance*, which is defined as "asymmetric topological properties of the labeled nodes, i.e., labeled nodes are not equal in terms of their structural role in the graph," is another problem proposed in the ReNode paper [1]. While we include ReNode as one of our baseline methods, we would like to emphasize that topology imbalance is orthogonal to class imbalance and is not the focus of our work.

**How does GBA alleviate class imbalance problem:**

- First, we show that ambivalent and distant message-passing can exacerbate the bias towards the majority class, as depicted in Figure 1.
- To address this issue, GBA identifies nodes with high prediction risks, which are likely to be misclassified minority class nodes due to their greater susceptibility to ambivalent and distant message-passing (as shown in Figure 1). 
- We then utilize similarity-based candidate class selection and topological augmentation to rectify misclassifications caused by the joint effect of ambivalent/distant message-passing and class imbalance.

Our approach is effective in alleviating class imbalance because the disadvantaged minority classes stand to benefit the most from our proposed GBA approach. We provide empirical evidence of this in Figure 6 and Appendix 2.1, where GBA demonstrates a significant improvement in minority class accuracy under ambivalent and distant message-passing. Additionally, Table 6 and Appendix 2.2 show that our approach can also greatly reduce the disparity in class accuracy, i.e., promoting fairness among majority and minority classes. We appreciate your feedback and will make revisions to improve the clarity of our paper.


### Weakness #2 & Question #2: Related Works

Thank you for the valuable suggestion. We will incorporate additional discussions in the related work section as per your recommendation. We acknowledge the contributions of DEMO-Net and Tail-GNN in addressing degree-related biases. However, it is worth noting that these works aim to mitigate the bias between high-degree (head) nodes and low-degree (tail) nodes rather than handling the bias between head/tail classes. Hence, it may not be appropriate to regard them as direct counterparts to the IGL techniques employed in this study.

### Weakness #3: Format

Thank you for bringing this matter to our attention. We will diligently revise the paper and place increased emphasis on ensuring that the formatting adheres to appropriate standards.

### Question #1: Novelty

Our work is novel in the following aspects:
- We propose to address the issue of Imbalanced Graph Learning (IGL) through a topology-centric lens. To tackle the node-level class imbalance via topological manipulations, we explore the role of topology structure in the context of IGL, which has received limited attention in prior literature.
- Our investigation reveals that ambivalent and distant message-passing can greatly amplify the bias resulting from class imbalance. While extensive research has been conducted on both of these challenges separately, no prior work has explicitly examined their relationship and interaction with the class imbalance issue.
- Based on our findings, we have developed a lightweight, efficient, and versatile augmentation technique called GBA to mitigate ambivalent and distant message-passing in IGL. This technique is compatible with existing imbalanced graph learning techniques and can be used to further enhance their performance. To our best knowledge, it is the first work to handle node-level class imbalance via topology-centric operations.

Extensive experiments validate the effectiveness of GBA in addressing class imbalance, resulting in consistent and significant gains in various real-world IGL tasks in terms of classificaiton performance (Table 2 & 3 & 7 & 8 & 9 & 10) and reducing class accuracy disparity (Table 6 & 8).

Thank you once again for your feedback, and please let us know if you have any further questions or concerns.


# Reviewer ZyGi

We appreciate for your thoughtful review as well as the time and effort you have taken to evaluate our work. We have carefully considered your comments and criticisms, please see our itermized responses to each of your concerns:

### Weakness #1: GraphSMOTE & GraphENS results in Figure 1

Thank you for your valuable suggestion. There is no doubt that other IGL baselines such as GraphSMOTE and GraphENS can alleviate the long-tail problem since they can oversample the labeled nodes of minority classes and make them more robust to the challenges in message-passing. We have run the GraphSMOTE and GraphENS under the same setting as in Figure 1: [Fig-GraphENS-Ambivalent](https://anonymous.4open.science/r/KDD23_Paper275-E66D/pics/mp_ambivalent_gens.png), [Fig-GraphENS-Distant](https://anonymous.4open.science/r/KDD23_Paper275-E66D/pics/mp_distant_gens.png), [Fig-GraphSMOTE-Ambivalent](https://anonymous.4open.science/r/KDD23_Paper275-E66D/pics/mp_ambivalent_gsmote.png), [Fig-GraphSMOTE-Distant](https://anonymous.4open.science/r/KDD23_Paper275-E66D/pics/mp_distant_gsmote.png).

Compared with the naive GCN without any IGL techniques, the gap between the minority class and majority class curves shrinks but still exists, and the gap is still non-neglectable. We also notice that compared to GraphSMOTE, GraphENS usually yields a smaller gap. This observation is in line with our findings that GraphENS has a lower accuracy disparity across different classes than other baselines. However, the gap can be further reduced using GBA, as detailed in Appendix A2.2 and Table 6.



### Weakness #2: Effectiveness of ambivalent and distant message-passing

We are sorry for any confusion that may have arisen. We wish to clarify that **we neither consider nor claim that ambivalent and distant message-passing constitute our technical contribution**. Rather, they represent the challenges that inherently exist in graph learning tasks and have been extensively discussed in previous works aimed at addressing heterophilic graphs and long-distance propagation.

Our contributions are:
- We propose to address the issue of Imbalanced Graph Learning (IGL) through a topology-centric lens. To tackle the node-level class imbalance via topological manipulations, we explore the role of topology structure in the context of IGL, which has received limited attention in prior literature.
- Our investigation reveals that ambivalent and distant message-passing can greatly amplify the bias resulting from class imbalance. While extensive research has been conducted on both of these challenges separately, no prior work has explicitly examined their relationship and interaction with the class imbalance issue.
- Based on our findings, we have developed a lightweight, efficient, and versatile augmentation technique called GBA to mitigate ambivalent and distant message-passing in IGL. This technique is compatible with existing imbalanced graph learning techniques and can be used to further enhance their performance. 
- Extensive experiments validate the effectiveness of GBA in addressing class imbalance, resulting in consistent and significant gains in various real-world IGL tasks in terms of classificaiton performance (Table 2 & 3 & 7 & 8 & 9 & 10) and reducing class accuracy disparity (Table 6 & 8).

In Appendix 2.1 and Fig. 6, we provide a detailed discussion of the effectiveness of GBA in mitigating the influence of ambivalent and distant message-passing. Our results demonstrate that GBA can effectively alleviate the negative impact of these challenges in IGL, thereby enabling GNN models to achieve better prediction performance on minority classes.

### Weakness #3: Relationship with TAM

Thank you for bringing this to our attention. In TAM, the authors demonstrate that "a significantly high false positive ratio appears around minor nodes that have higher connectivity with major nodes". While this is conceptually similar to the challenge of ambivalent message-passing, there are several key differences between TAM and our work:
- **Problem Scope**: TAM does not consider the influence of distant message-passing in IGL, which is non-negligible in practice, as demonstrated in Fig. 1(b). In contrast, our work examines the joint effect of both ambivalent and distant message-passing. This difference in scope also results in varying empirical performance, as further discussed in the following response.
- **Technical Solution**: TAM proposes to down-weight nodes/classes with anomalous connectivity patterns in the loss function, mainly focusing on reweighting labeled nodes (except the class-wise temperature strategy). In comparison, our approach is a general data augmentation strategy that considers both labeled and unlabeled nodes, aimed at mitigating both ambivalent and distant message-passing in IGL.
- **Performance**: Lastly, there are notable differences in the empirical performance of TAM and our work. As evidenced by Table 2 in our paper and Table 1 in TAM, X+GBA consistently outperforms X+TAM across all settings with a notable margin. For instance, with GCN and BAcc, the best results from GBA/TAM are 74.24/71.52 (Cora), 66.35/57.47 (CiteSeer), and 77.38/74.13 (PubMed). We have checked the random seed and other settings that may cause inconsistent evaluation and confirmed that the above results are comparable.

### Weakness #4: Ambivalent message-passing and homophily assumption

We apologize for the confusion. We would like to make a brief reclarification here.
- **Regarding the issue of ambivalent message-passing and graph heterophily:** We respectfully direct your attention to our answer to question 2, as well as the Related Works section (GNNs with heterophilic/long-distance propagation) and relevant results presented in Appendix 2.4.
- **Regarding the graph heterophily and homophily assumption:** We would like to note that as discussed in Section A.3, graph with high heterophily (i.e., heterophilic edges prevail) is beyond the scope of this work. Our approach GBA aims to address class imbalance bias caused by local heterophilic connections in graphs exhibiting low heterophily, i.e., we follow the homophily assumption in this work. Therefore, high-risk misclassified nodes that suffer local ambivalent message-passing are likely to be linked to their ground truth class, enabling GBA to execute candidate class selection. Please also refer to Figure 2 (Section 3.2 part) that illustrates this concept with an intuitive example.

### Weakness #5: Unsteady results?

 Sorry for the confusion and we wish to clarify that the imbalanced semi-supervised learning setting we adopted in our study has been widely used in prior literature [1, 2, 3]. Therefore, we deemed it appropriate to adhere to their settings and evaluation procedures to ensure a fair comparison.

Furthermore, we emphasize that to mitigate the impact of randomness and produce reliable results, we performed five independent runs for all experiments. Each run consisted of the entire data filtering, model initialization, and training phases. Notably, we randomly selected the labeled nodes of minority classes in each run to ensure that any enhancements attributed to the GBA were not due to a selective choice of node combinations or chance events.

We will elaborate on this aspect further in the Reproducibility section.

[1] [Topology-Imbalance Learning for Semi-Supervised Node Classification](https://arxiv.org/pdf/2110.04099v1.pdf)  
[2] [GraphENS: Neighbor-Aware Ego Network Synthesis for Class-Imbalanced Node Classification](https://openreview.net/pdf?id=MXEl7i-iru)  
[3] [TAM: Topology-Aware Margin Loss for Class-Imbalanced Node Classification](https://proceedings.mlr.press/v162/song22a/song22a.pdf)


### Weakness #6: Extreme class imbalance

Thank you for the great question! Extreme class imbalance ratio for sure will further degrade the performance of minority classes. However, numerous prior studies [1, 2, 3] have indicated that other factors related to data complexity (e.g., noise, distribution overlapping, and small disjuncts) often play a more significant role in causing bias in learning systems. These investigations and some recent works [4] have also suggested that a higher class imbalance ratio does not necessarily correlate with an increase in task difficulty.

Returning to graph learning, the ambivalent and distant message-passing present in the graph topology can also be considered as data complexity factors that can impact the learning process. All factors, including those from both the node features and topology structure, can significantly influence the task's outcome.

Considering these factors, for a minority test node from class A but predicted to be class B, the uncertainty-based risk estimation will likely fail only if it is indistinguishable from class B in both (1) node feature space and (2) connectivity pattern. Such a scenario is particularly problematic since all training signals available for the test node are misleading, and most existing learning models would fail in this situation.

Fortunately, such extreme cases are uncommon in practice, and we validate this by conducting experiments under more extreme class imbalance with IR = 100. Results show that GBA can further boost the BEST performance among all IGL techniques by a large margin even under extreme class imbalance. For example, for best BAcc with GCN, GBA\_P achieved 14.10\%/20.04\%/42.52\% improvement on Cora/CiteSeer/PubMed, respectively. For best Marco-F1, this improvement is 21.35\%/23.81\%/73.41\%. Due to space limitation, we only report the BEST results among 7 baselines under each GBA setting, please refer to the [anonymous page](https://anonymous.4open.science/r/KDD23_Paper275-E66D) for the full results.


| GNN - Metric           | Cora  | w/ GBA_P        | w/ GBA_T          | CiteSeer | w/ GBA_P          | w/ GBA_T          | PubMed | w/ GBA_P          | w/ GBA_T        |
| ---------------------- | ----- | --------------- | ----------------- | -------- | ----------------- | ----------------- | ------ | ----------------- | --------------- |
| **GCN BEST BAcc**      | 69.56 | *79.37*(14.10%) | **80.16**(15.25%) | 60.99    | *73.21*(20.04%)   | **73.25**(20.11%) | 41.36  | **58.95**(42.52%) | *52.91*(27.93%) |
| **GCN BEST Macro-F1**  | 64.81 | *78.65*(21.35%) | **79.66**(22.91%) | 57.74    | **71.48**(23.81%) | *70.49*(22.09%)   | 33.02  | **57.26**(73.41%) | *50.69*(53.53%) |
| **GAT BEST BAcc**      | 69.13 | *79.36*(14.80%) | **79.87**(15.54%) | 59.96    | **70.95**(18.34%) | *70.84*(18.15%)   | 38.71  | **55.80**(44.15%) | *51.30*(32.52%) |
| **GAT BEST Macro-F1**  | 63.46 | *78.56*(23.79%) | **79.09**(24.63%) | 57.07    | **69.11**(21.11%) | *66.55*(16.62%)   | 30.07  | **54.23**(80.34%) | *50.35*(67.45%) |
| **SAGE BEST BAcc**     | 67.65 | *79.77*(17.91%) | **80.36**(18.78%) | 57.64    | *69.22*(20.09%)   | **73.42**(27.37%) | 40.73  | **62.32**(52.99%) | *53.48*(31.29%) |
| **SAGE BEST Macro-F1** | 64.37 | *78.93*(22.62%) | **79.82**(24.00%) | 53.64    | *66.57*(24.11%)   | **69.72**(29.98%) | 32.38  | **60.98**(88.33%) | *52.20*(61.21%) |



[1] [Dealing with Data Difficulty Factors while Learning from Imbalanced Data](https://citeseerx.ist.psu.edu/document?repid=rep1&type=pdf&doi=a4c275fefe646a0a578713cd14070affc0594286)  
[2] [Effect of label noise in the complexity of classification problems](https://www.sciencedirect.com/science/article/pii/S0925231215001241)  
[3] [Overlap versus imbalance](https://web.cs.dal.ca/~tt/papers/AI2010a.pdf)  
[4] [Class-balanced loss based on effective number of samples](https://openaccess.thecvf.com/content_CVPR_2019/papers/Cui_Class-Balanced_Loss_Based_on_Effective_Number_of_Samples_CVPR_2019_paper.pdf)


### Weakness #7: Natural class imbalance


Thanks for your advice. OGB has set a great large-scale benchmark for graph learning research. However as stated in the paper, on each dataset we have to consider combinations of 7 baselines and 3 GBA settings (w/o GBA, + GBA\_P, + GBA\_T), and each combination needs to be run 5 times independently to get credible results. Also, some IGL baselines have high space complexity, e.g. the official implementation of ReNode, GraphSMOTE and GraphENS require space for a dense adjacency matrix of $O(n^2)$ size. Due to the limitation of computational resources, we are currently unable to run experiments on graphs of this scale.

Despite these constraints, we were able to simulate the long-tail class imbalance present in real-world data by utilizing a power-law distribution. We set the imbalance ratio (largest class to smallest class) to 100 to test GBA's robustness under natural and extreme class imbalance. Our results demonstrated that GBA consistently improved the performance of all IGL techniques by a significant margin. For instance, the BAcc of GCN with GBA\_T achieved an improvement of 4.14\%/8.97\%/4.16\% on Cora/CiteSeer/PubMed, respectively, while the Marco-F1 also showed improvements of 3.67\%/10.37\%/3.09\%. Such improvement is consistent with other GNN architectures and metrics. Similar to the above, due to the space limitation, we only report the BEST results among 7 baselines under each GBA setting, please kindly refer to the [anonymous page](https://anonymous.4open.science/r/KDD23_Paper275-E66D) for full results.


| GNN - Metric           | Cora  | w/ GBA_P       | w/ GBA_T         | CiteSeer | w/ GBA_P        | w/ GBA_T          | PubMed | w/ GBA_P         | w/ GBA_T         |
| ---------------------- | ----- | -------------- | ---------------- | -------- | --------------- | ----------------- | ------ | ---------------- | ---------------- |
| **GCN BEST BAcc**      | 73.80 | *74.10*(0.41%) | **76.86**(4.14%) | 56.25    | *59.23*(5.29%)  | **61.30**(8.97%)  | 72.84  | **75.92**(4.22%) | *75.87*(4.16%)   |
| **GCN BEST Macro-F1**  | 73.35 | *73.97*(0.84%) | **76.04**(3.67%) | 53.83    | *58.59*(8.83%)  | **59.41**(10.37%) | 73.72  | **76.08**(3.21%) | *75.99*(3.09%)   |
| **GAT BEST BAcc**      | 73.23 | *73.92*(0.94%) | **74.30**(1.47%) | 54.42    | *58.41*(7.33%)  | **60.54**(11.24%) | 72.90  | *74.30*(1.92%)   | **74.61**(2.35%) |
| **GAT BEST Macro-F1**  | 72.74 | *73.68*(1.29%) | **73.80**(1.46%) | 50.87    | *58.05*(14.11%) | **59.01**(15.99%) | 73.34  | *73.69*(0.49%)   | **75.39**(2.79%) |
| **SAGE BEST BAcc**     | 71.07 | *73.78*(3.82%) | **74.68**(5.08%) | 52.19    | *60.74*(16.37%) | **61.85**(18.49%) | 72.12  | *77.64*(7.66%)   | **78.43**(8.76%) |
| **SAGE BEST Macro-F1** | 71.05 | *72.80*(2.47%) | **73.50**(3.45%) | 48.89    | *60.31*(23.36%) | **60.75**(24.27%) | 72.02  | *77.37*(7.43%)   | **78.22**(8.61%) |


Thank you once again for your feedback, and please let us know if you have any further questions or concerns.


# Reviewer KB6H

### Weakness #1: On the high-risk but correct prediction

Thank you for your insightful question. Given that  the model prediction, labeled nodes, and graph topology are the only available signals, it is hard to determine whether a high-risk node is misclassified or not. However, this does not pose a significant hindrance to GBA for the following reasons:
- Firstly, for minority classes, a high-uncertainty but correctly classified node will still have a small risk score due to the relative normalization approach employed in Eq. (7), which is designed to be imbalance-aware and protect minority classes. Therefore, such nodes are unlikely to be wrongly disturbed by the augmentation.
- Secondly, it is unlikely that nodes belonging to the majority classes will exhibit high-uncertainty as these classes have sufficient training labels. Among the high-risk nodes, the population of misclassified nodes is significantly larger than that of correctly classified nodes (as illustrated in Fig. 3 \& 4), thus the benefits of applying GBA clearly outweigh the losses.
- Lastly, GBA is resilient to "fake" high-uncertainty nodes produced by randomness in training dynamics, as it employs soft and dynamic augmentation during training. GBA does not generate virtual edges for all high-uncertainty/risk nodes in every iteration (as indicated in line \#11 in Algorithm 1), thereby is not sensitive to the temporary high-uncertainty pattern resulting from random training dynamics.

### Weakness #2: Early stage of training

Thank you for raising an important question. In Appendix 3 (Limitations and Future Works), we acknowledge that the reliance on exploiting model prediction for risk and similarity estimation may be considered a potential limitation of GBA. Nonetheless, our experimental results suggest that this limitation rarely occurs in practice. We attribute this to two factors:

- Fast approximate convergence. Our experiments on five distinct datasets and three GNN architectures have demonstrated that the GNN's predictive performance significantly improves in the early stage of training, reaching close to their maximum/best results within 10-50 epochs.  As a result, the imperfect predictions that occur only in the initial few epochs have limited impact.
- Soft augmentation. As discussed in our response to Question 1, GBA does not generate virtual edges for all high-uncertainty/risk nodes during each iteration. Additionally, unlike node-centric resampling techniques (e.g., GraphENS with a default `warmup_epoch=5`), GBA only introduces a small number of virtual super-nodes and edges, which is less likely to interfere with the training process within the initial few epochs.

Futhermore, we note that this issue can be easily prevented by introducing a "warmup" parameter, which we will implement and release along with our source code and documentation after the paper's acceptance.


### Weakness #3: Mild class imbalance

Thanks for the suggestion. We would like to note that the imbalanced semi-supervised learning setting we adopted has been widely used in previous research [1, 2, 3]. Therefore, we decided to employ their setup and evaluation protocols to ensure a just comparison.

Nevertheless, in order to test GBA's effectiveness with less label sparsity, we carry out experiments under mild class imbalance (IR = 5) following the previous works (e.g., ReNode, GraphENS, TAM), where all the minority class have 4 training samples. We note that this is also the smallest IR used in existing works. Under the mild class imbalance, GBA still consistently improves the performance of all IGL techniques by a considerable margin.
For example, in terms of best BAcc with GCN, GBA\_T achieves 3.54\%/1.70\%/2.77\% improvement on Cora/CiteSeer/PubMed, respectively.
It is also worth noting that GraphSAGE achieved the best performance among all 3 GNN architectures. With GraphSAGE, GBA\_T achieves larger improvements, i.e., 5.53\%/9.84\%/5.44\% best BAcc improvement and 4.01\%/10.18\%/7.11\% best macro-f1 on Cora/CiteSeer/PubMed, respectively. Due to space limitation, we only report the BEST results among 7 baselines under each GBA setting, please kindly refer to the following [anonymous page](https://anonymous.4open.science/r/KDD23_Paper275-E66D) for the full results.


| GNN - Metric           | Cora    | w/ GBA_P       | w/ GBA_T         | CiteSeer | w/ GBA_P         | w/ GBA_T          | PubMed | w/ GBA_P       | w/ GBA_T         |
| ---------------------- | ------- | -------------- | ---------------- | -------- | ---------------- | ----------------- | ------ | -------------- | ---------------- |
| **GCN BEST BAcc**      | 75.56   | *76.73*(1.54%) | **78.23**(3.54%) | 61.41    | **62.75**(2.18%) | *62.46*(1.70%)    | 74.53  | *75.79*(1.70%) | **76.59**(2.77%) |
| **GCN BEST Macro-F1**  | *75.48* | 75.29(-0.25%)  | **76.83**(1.79%) | 60.68    | **62.53**(3.04%) | *62.18*(2.46%)    | 73.52  | *75.73*(3.01%) | **75.98**(3.34%) |
| **GAT BEST BAcc**      | 74.17   | *75.65*(2.00%) | **78.00**(5.16%) | 57.95    | *63.01*(8.73%)   | **64.09**(10.60%) | 73.97  | *76.45*(3.35%) | **76.74**(3.75%) |
| **GAT BEST Macro-F1**  | 73.65   | *74.94*(1.75%) | **76.21**(3.48%) | 56.72    | *62.72*(10.58%)  | **63.90**(12.65%) | 73.48  | *75.66*(2.96%) | **76.26**(3.79%) |
| **SAGE BEST BAcc**     | 73.69   | *75.21*(2.07%) | **77.77**(5.53%) | 59.38    | *64.98*(9.43%)   | **65.23**(9.84%)  | 74.26  | *76.93*(3.60%) | **78.30**(5.44%) |
| **SAGE BEST Macro-F1** | 73.19   | *74.80*(2.20%) | **76.12**(4.01%) | 59.06    | *64.60*(9.38%)   | **65.07**(10.18%) | 72.60  | *76.21*(4.98%) | **77.76**(7.11%) |


[1] [Topology-Imbalance Learning for Semi-Supervised Node Classification](https://arxiv.org/pdf/2110.04099v1.pdf)  
[2] [GraphENS: Neighbor-Aware Ego Network Synthesis for Class-Imbalanced Node Classification](https://openreview.net/pdf?id=MXEl7i-iru)  
[3] [TAM: Topology-Aware Margin Loss for Class-Imbalanced Node Classification](https://proceedings.mlr.press/v162/song22a/song22a.pdf)


### Quesiton #1: Using variance in Eq. (7)

Thank you for your question. The similarity in the form of Eq. (7) and standard normalization is why we named it imbalance-aware normalization. To incorporate the class-imbalance prior directly into the normalization, we utilize the relative normalization weight in Eq. (6) instead of the variance. This approach accounts for the higher chance of misclassifying minority samples as majority, as opposed to the reverse.

Compared to the static weight defined in Eq. (6), actual variance need to be calculated in every iteration. More importantly, due to the lack of labels in minority classes, there may be only a few nodes predicted to be minority samples, leading to inaccurate and unstable variance estimation. Hence, we utilize both Eq. (6) and (7) for faster and more stable imbalance-aware normalization.


### Quesiton #2: Micro-averaged metrics

Sure. In accordance with previous research [1, 2, 3], we utilize the balanced accuracy and macro-f1 score to accurately assess the model's performance on both majority and minority classes. It should be noted that micro-averaged metrics may introduce biases and may not accurately reflect the model's performance on minority classes since they are likely to be dominated by majority classes. Nevertheless, we extend the main results (Table 2) in the original paper and present results using the Micro-F1. 

The outcomes show that GBA can still demonstrate competitive and even better performance to all baselines. More importantly, GBA consistently improves the best performance with micro-averaged metric. For example, with GCN, GBA\_T achieves 3.07\%/16.85\%/6.21\% improvement on Cora/CiteSeer/PubMed on the best Micro-f1 score. This further demonstrates the efficiency of GBA's design: it can boost the learning for minority classes without sacrificing the performance of majority classes. We only report the BEST results among 7 baselines under each GBA setting due to the space limitation, please kindly refer to the following [anonymous page](https://anonymous.4open.science/r/KDD23_Paper275-E66D) for the full results.

| GNN - Metric           | Cora  | w/ GBA_P       | w/ GBA_T         | CiteSeer | w/ GBA_P        | w/ GBA_T          | PubMed | w/ GBA_P         | w/ GBA_T         |
| ---------------------- | ----- | -------------- | ---------------- | -------- | --------------- | ----------------- | ------ | ---------------- | ---------------- |
| **GCN BEST Micro-F1**  | 74.36 | *75.88*(2.04%) | **76.64**(3.07%) | 56.62    | *63.46*(12.08%) | **66.16**(16.85%) | 72.18  | **76.90**(6.54%) | *76.66*(6.21%)   |
| **GAT BEST Micro-F1**  | 74.44 | *74.50*(0.08%) | **76.18**(2.34%) | 53.46    | *63.82*(19.38%) | **66.06**(23.57%) | 72.46  | **75.88**(4.72%) | *75.26*(3.86%)   |
| **SAGE BEST Micro-F1** | 72.78 | *73.64*(1.18%) | **75.18**(3.30%) | 54.88    | *67.78*(23.51%) | **67.84**(23.62%) | 70.42  | *75.66*(7.44%)   | **76.72**(8.95%) |

[1] [Topology-Imbalance Learning for Semi-Supervised Node Classification](https://arxiv.org/pdf/2110.04099v1.pdf)  
[2] [GraphENS: Neighbor-Aware Ego Network Synthesis for Class-Imbalanced Node Classification](https://openreview.net/pdf?id=MXEl7i-iru)  
[3] [TAM: Topology-Aware Margin Loss for Class-Imbalanced Node Classification](https://proceedings.mlr.press/v162/song22a/song22a.pdf)

Thank you once again for your feedback, and please let us know if you have any further questions or concerns.