---
title: Technical summary - Automated visual inspection machine for inspecting connector terminals of wire harnesses.
date: 2023-02-24
tags: ["QEUシステム", "メトリックス", "Julia言語", "SOART", "外観検査", "機械学習"]
excerpt: julia言語とテクノメトリックスを使った外観検査自動機
---

## Technical summary - Automated visual inspection machine for inspecting connector terminals of wire harnesses.

### ＞Donate me(click here)＜[https://www.paypal.com/paypalme/QEUglobal?v=1&utm_source=unp&utm_medium=email&utm_campaign=RT000481&utm_unptid=29844400-7613-11ec-ac72-3cfdfef0498d&ppid=RT000481&cnac=HK&rsta=en_GB%28en-HK%29&cust=5QPFDMW9B2T7Q&unptid=29844400-7613-11ec-ac72-3cfdfef0498d&calc=f860991d89600&unp_tpcid=ppme-social-business-profile-created&page=main%3Aemail%3ART000481&pgrp=main%3Aemail&e=cl&mchn=em&s=ci&mail=sys&appVersion=1.71.0&xt=104038]

### [Technology field]
This invention relates to an automatic computerized visual inspection machine for inspecting connector terminals of wire harnesses.

### [Technology background]
According to Kaggle which conducts a machine learning technology competition, one of the trends in machine learning in 2022 is TinyML, which refers to small-scale machine learning applications that works on edge computers for IoT. Thus, machine learning technology has already entered the popularization phase (Fig. 1 and Fig. 2).

**(Fig. 1: Kaggle Articles)**

![image3-20-1](/2023-02-23-QEUR22_VINSP19/image3-20-1.jpg)

**(Fig. 2: About TinyML)**

![image3-20-2](/2023-02-23-QEUR22_VINSP19/image3-20-2.jpg)

The performance of inspection by human visual observation (visual inspection) is shown in Figure 3. Generally, the defect detection rate by visual inspectors is about 80% at maximum. And the performance varies greatly depending on the physical and mental condition of the inspector (Fig. 4).

**(Fig. 3: Visual inspection performance)**

![image3-20-3](/2023-02-23-QEUR22_VINSP19/image3-20-3.jpg)

**(Fig. 4: Inspectors condition and flow-out)**

![image3-20-4](/2023-02-23-QEUR22_VINSP19/image3-20-4.jpg)

This invention applies TinyML to connector terminal inspection of wire harnesses (hereinafter referred to as "WH"). WH is a collection of wires and connectors to facilitate wiring (assembly) of electrical systems, as shown in Figure 5. As a result, the defect rate of WH products is higher than that of other products. Among product defects, connector and terminal defects are regarded as serious defects because they are directly related to the basic performance of the product (conduction stability). Incidentally, there are two types of connectors, male and female, and it is the male connectors that are more prone to (terminal) defects. "

**(Fig. 5: What is a wiring harness?)**

![image3-20-5](/2023-02-23-QEUR22_VINSP19/image3-20-5.jpg)

**(Fig. 6: Connector’s terminal inspection)**

![image3-20-6](/2023-02-23-QEUR22_VINSP19/image3-20-6.jpg)

For automatic inspection, it is necessary to collect learning data during the mass production prototype stage of the product realization process shown in Figure 7. However, in general, the number of prototypes is about 200pcs at most, which is not enough to obtain the training data necessary for complex machine learning.

**(Fig. 7: Product Realization Process)**

![image3-20-7](/2023-02-23-QEUR22_VINSP19/image3-20-7.jpg)

Therefore, it is necessary to collect data in the design and development (R&D) phase prior to mass production prototyping. For this purpose, it is necessary to prepare study data in VR (virtual space, virtual reality). In the case of male connectors, training data can be easily collected with a 3DCG production tool (Fig. 8).

**(Fig. 8: Production of images of connectors by VR)**

![image3-20-8](/2023-02-23-QEUR22_VINSP19/image3-20-8.jpg)

Although it appears to be very easy for a human to inspect connector terminals, it is significantly more difficult for a machine to perform this task. As an example, let us consider a typical defective item called "terminal pullout. Terminal disconnection occurs when a terminal is inserted into a connector and is not locked (fixed) as designed in the connector, causing the terminal to retract or tilt.

**(Fig. 9: Terminals retracted)**

![image3-20-9](/2023-02-23-QEUR22_VINSP19/image3-20-9.jpg)

**(Fig. 10: Terminals are tilted)**

![image3-20-10](/2023-02-23-QEUR22_VINSP19/image3-20-10.jpg)

The tilt of a terminal can be detected with only one image. However, a vertically retracted terminal may not be detected in a single image (Fig. 11). In other words, detecting anomalies in three-dimensional objects is a different kind of difficulty than using highly accurate deep learning to classify the types of objects in an image.

**(Fig. 11: Examples of Image Recognition)**

![image3-20-11](/2023-02-23-QEUR22_VINSP19/image3-20-11.jpg)

### [Problems to be solved by this invention]

Dr. Edward Deming and Dr. Genichi Taguchi, who laid the theoretical foundation for quality control, advocated that inspection work should be controlled based on cost. This approach is the "critical inspection point" shown in Fig. 12, which determines whether full inspection are required.

**(Fig. 12: Selection of full inspection based on the "Critical Inspection Point")**

![image3-20-12](/2023-02-23-QEUR22_VINSP19/image3-20-12.jpg)

To visualize the total loss involved in inspection, a line is drawn for a constant equipment cost for production (inspection) and a line of loss proportional. The total loss is the sum of these two lines. The point where these two lines intersect is the "inspection critical point (critical quantity x, critical loss y).


**(Fig. 13: Cpk defective rates and inspection strategies)**

![image3-20-13](/2023-02-23-QEUR22_VINSP19/image3-20-13.jpg)

According to general technical standards such as Six Sigma and PPAP, a Cpk of 1.6 or higher means no inspection, a Cpk of 1.2 or higher means sampling inspection, and a Cpk of 1.0 or lower means total inspection. However, since circumstances differ by industry and product characteristics, it is better to use the above costs to evaluate the practical situation.

Two findings can be drawn from the above discussion of inspection critical points. One is that a high defect rate is easily worth the cost of a full inspection. The other is that the lower the cost of the equipment, the more reasonable it is.

The following graph summarizes the practical cost structure of full visual inspection. With current technology, in many cases, inspections are performed by humans. Therefore, as production volume increases, it is necessary to increase the number of inspectors. The relationship between the defect rate, labor costs for inspectors, and the critical defect rate is as described above.


**(Fig. 14: Practical concept of (full) visual inspection)**

![image3-20-14](/2023-02-23-QEUR22_VINSP19/image3-20-14.jpg)

According the graph above, the cost of visual inspection equipment is set higher than labor costs. However, as shown in Figure 15, the amount of depreciation per month will rarely be higher than labor costs.


**(Fig. 15: Practical concept of equipment costs in the inspection strategy)**

![image3-20-15](/2023-02-23-QEUR22_VINSP19/image3-20-15.jpg)

In other words, the most important factor is "whether it is technically feasible (or detectable)" when full visual inspection is required.


### [Means to solve problems]

In order to have an automated visual inspection machine in operation immediately after mass production, learning must be completed prior to the design development phase. VR technology is used for this purpose. In addition, multiple cameras are installed in the VR as shown in Figures 16 and 17 to detect three-dimensional anomalies.

**(Fig. 16: Benefits of Multiple Cameras)**

![image3-20-16](/2023-02-23-QEUR22_VINSP19/image3-20-16.jpg)

**(Fig. 17: Multiple cameras installed in VR [Five-Eyes])**

![image3-20-17](/2023-02-23-QEUR22_VINSP19/image3-20-17.jpg)

In this invention, five cameras are installed to inspect the visual of three-dimensional objects (Fig. 18). Whereas the center camera is used to generate "standard vectors (data)" in Double-Eye RT method. The other cameras are used to generate "measurement vectors (data)" in left-right and vertical directions.

**(Fig. 18: Concept of Double-Eye RT Method in Five-Eyes)**

![image3-20-18](/2023-02-23-QEUR22_VINSP19/image3-20-18.jpg)

The processing flow of the invention is shown in Figure 19. In order to detect anomalies, the invention uses a combination of feature calculation methods called Double-Eye RT metrics and SOART metrics, and the output is input to "supervised learning (e.g., SVM)" for prediction.

**(Fig. 19: Flow diagram of the invention)**

![image3-20-19](/2023-02-23-QEUR22_VINSP19/image3-20-19.jpg)

Double-Eye RT method uses an average image from the center camera as the reference vector (Fig. 20) and compares it with images from the right and left cameras taken simultaneously (Fig. 21) to generate metrics for sensitivity and SN ratio.

**(Fig. 20: Central camera image)**

![image3-20-20](/2023-02-23-QEUR22_VINSP19/image3-20-20.jpg)

**(Fig. 21: Right and left camera images)**

![image3-20-21](/2023-02-23-QEUR22_VINSP19/image3-20-21.jpg)

RT method is one of the pattern recognition techniques of the Taguchi method, but in this invention, it is used as a techno-metric instead of being used as it is for discrimination. and outputs the SN ratio (Y2).

**(Fig. 22: Concept of RT method)**

![image3-20-22](/2023-02-23-QEUR22_VINSP19/image3-20-22.jpg)

However, the metrics calculation for Double-Eye RT method takes the difference between RT metrics calculated for the right and center cameras and RT metrics for the left and center cameras (Fig. 23). The top-center-bottom camera is the same as above.

**(Fig. 23: Concept of Double-Eyes RT Metrics [RT Difference])**

![image3-20-23](/2023-02-23-QEUR22_VINSP19/image3-20-23.jpg)

The results of generating images by transforming the values of Double-Eyes RT metrics are shown in Figure 24. The sensitivity and SN ratio of each eye include a unique "stereoscopic effect". Here, 31X indicates a collapse in the X-direction at Pin 3 (near the center). On the other hand, 61X indicates Pin 6 (near the right edge).

**(Fig. 24: Data processing results for tilt in the X-direction at PIN 3)**

![image3-20-24](/2023-02-23-QEUR22_VINSP19/image3-20-24.jpg)

**(Fig. 25: Data processing results for tilt in the X-direction at PIN 6)**

![image3-20-25](/2023-02-23-QEUR22_VINSP19/image3-20-25.jpg)

Thus, the distribution of the metrics is different depending on the PIN location and the way the PIN tilt. Next, Double-Eyes RT metrics processing was performed on the image with the terminal tilt in Y direction and the value of metrics were transferred to an image; in the case of collapses in the Y direction, both PIN 3 and PIN 6 can be detected in the same way (Fig. 26 and 27).

**(Fig. 26: Data processing results for tilt in the Y direction at PIN 3)**

![image3-20-26](/2023-02-23-QEUR22_VINSP19/image3-20-26.jpg)

**(Fig. 27: Data processing results for tilt in Y direction at PIN 6)**

![image3-20-27](/2023-02-23-QEUR22_VINSP19/image3-20-27.jpg)

As shown in the flow diagram above, the present invention uses a type of RT method called SOART metrics to convert Double-Eye RT metrics into a small number of metrics. Convolution is performed. Examples of convolutional components are shown in Figures 28 and 29.

**(Fig. 28: Parts used in convolution RT method Part 1)**

![image3-20-28](/2023-02-23-QEUR22_VINSP19/image3-20-28.jpg)

**(Fig. 29: Parts used in convolution RT method Part 2)**

![image3-20-29](/2023-02-23-QEUR22_VINSP19/image3-20-29.jpg)

Here, the BEND and LINE groups are convolved to generate the measurement vector for RT method, and the DATUM group is convolved to generate the reference vector for comparison, and the sensitivity and SN ratio (distance) are calculated. Thus, 12 different metrics are obtained, shown in Figure 30.

**(Fig. 30: Feature Engineering Part 1)**

![image3-20-30](/2023-02-23-QEUR22_VINSP19/image3-20-30.jpg)

The features extracted from the image are input to a "supervised learning" such as SVM (support vector machine). The features that are input to the SVM in this invention (Five-Eyes) are shown in Figure 31.

**(Fig. 31: Feature Engineering Part 2)**

![image3-20-31](/2023-02-23-QEUR22_VINSP19/image3-20-31.jpg)

In addition to feature values, the input information to the supervised learning logic must include information on the inspection location; in the case of SOART metrics, discrimination accuracy is improved when one set of features corresponds to one blob (Fig. 32). Since the object to be inspected contains many blobs, anomaly detection for each blob is more effective.

**(Fig. 32: Concept of Blob)**

![image3-20-32](/2023-02-23-QEUR22_VINSP19/image3-20-32.jpg)

### [Case Study]

In this case study, we present an example of detecting terminal tilt (X and Y directions) and terminal drawback with respect to connector terminal disconnection. Three cameras are used in this case, left-center-right only (Fig. 33 and 34).

**(Fig. 33: defect mode)**

![image3-20-33](/2023-02-23-QEUR22_VINSP19/image3-20-33.jpg)

**(Fig. 34: Multiple camera images)**

![image3-20-34](/2023-02-23-QEUR22_VINSP19/image3-20-34.jpg)

In this case study, we collected virtual space (VR) data with Blender software, extracted the features mentioned above, and got a result of predictions made with a support vector machine. Whereas, the support vector machine can switch the prediction pattern using the kernel, and the best results were obtained in Poly (polynomial) mode (Fig. 35).

**(Fig. 35: SVM Kernel Type)**

![image3-20-35](/2023-02-23-QEUR22_VINSP19/image3-20-35.jpg)

***(SVM program and predicted results)***


```python
# SVM for SOART metrics example
import pandas as pd
import math
import numpy as np
# Prediction
from sklearn import metrics, preprocessing
from sklearn.svm import SVC
from sklearn.metrics import confusion_matrix

# ----
# データを読み込む
# ----
# train
filepath_train = 'soart_mtxout_train_fiveye.csv'
df_org_train = pd.read_csv(filepath_train)

# test
filepath_test  = 'soart_mtxout_test_fiveye.csv'
df_org_test  = pd.read_csv(filepath_test)

# ----
# 欠陥分類を数字(0,1,2)に変換する
def create_numberlist(arr_defect, list_defect, list_number):
    arr_result = []
    for i in range(len(arr_defect)):
        for j, jStr in enumerate(list_defect):
            if arr_defect[i] == jStr:
                arr_result.append(list_number[j])
    return arr_result

# ----
# Resultコラムを作成する 
# ----
# train
list_train_defect = ['OK', 'new', 'old', '31D05','31X10','61D05','61X10','31Y10','61Y10',]
list_train_number = [   0,     0,     0,      1 ,      2,      1,      2,      3,      3,]
arr_defect_train  = df_org_train.loc[:,"defect"].values
arr_result_train  = create_numberlist(arr_defect_train, list_train_defect, list_train_number)
#print(arr_result_train)

# test(jCol = 4)
list_test_defect  = ['OK', '31D05','31X10','61D05','61X10','31Y10','61Y10',]
list_test_number  = [    0,      1,      2,      1,      2,      3,      3,]
df_test_jCol4     = df_org_test[df_org_test["jCol"]==4.0]
arr_defect_jCol4  = df_test_jCol4.loc[:,"defect"].values
arr_result_jCol4  = create_numberlist(arr_defect_jCol4, list_test_defect, list_test_number)
#print(arr_result_jCol4)

# test(jCol = 7)
#arr_test_defect   = ['OK', '31D05','31X10','61D05','61X10',]
df_test_jCol7     = df_org_test[df_org_test["jCol"]==7.0]
arr_defect_jCol7  = df_test_jCol7.loc[:,"defect"].values
arr_result_jCol7  = create_numberlist(arr_defect_jCol7, list_test_defect, list_test_number)
#print(arr_result_jCol7)

# ----
# パフォーマンス計測
# drop columun
df_org_train  = df_org_train.drop(labels=['iPic', 'icount', 'iRow', 'area'], axis=1)
df_test_jCol4 = df_test_jCol4.drop(labels=['iPic', 'icount', 'iRow', 'area'], axis=1)
df_test_jCol7 = df_test_jCol7.drop(labels=['iPic', 'icount', 'iRow', 'area'], axis=1)

# X and y dataset into train and test dataset
X_train = df_org_train.loc[:, "jCol":"DS_S6"].values
y_train = arr_result_train
X_test_jCol4 = df_test_jCol4.loc[:, "jCol":"DS_S6"].values
y_test_jCol4 = arr_result_jCol4
X_test_jCol7 = df_test_jCol7.loc[:, "jCol":"DS_S6"].values
y_test_jCol7 = arr_result_jCol7

# ----
# パフォーマンス計測
def performance_model(model, X_test, y_test):
    # predict
    y_pred = model.predict(X_test)

    # accuracy
    print("accuracy:", metrics.accuracy_score(y_true=y_test, y_pred=y_pred), "\n")
    # cm
    print(metrics.confusion_matrix(y_true=y_test, y_pred=y_pred))
                
# SVM学習の実行
kernel_names= ['linear','rbf','poly','sigmoid']
for kernel_name in kernel_names:

    # linear model
    model = SVC(kernel=kernel_name)
    model.fit(X_train, y_train)

    # jCol = 4.0
    print("---- {}-{} ----\n".format("jCol=4", kernel_name))
    performance_model(model, X_test_jCol4, y_test_jCol4)

    # jCol = 7.0
    print("---- {}-{} ----\n".format("jCol=7", kernel_name))
    performance_model(model, X_test_jCol7, y_test_jCol7)
```

***(Table : Confusion Matrix)***

**---- jCol=4-poly ----**
***accuracy: 0.9257142857142857 ***
[[200   0   0   0]
 [  0  50   0   0]
 [ 26   0  24   0]
 [  0   0   0  50]]
**---- jCol=7-poly ----**
***accuracy: 0.9428571428571428 ***
[[200   0   0   0]
 [  8  42   0   0]
 [ 12   0  38   0]
 [  0   0   0  50]]


As shown in the table above, the performance of this invention in anomaly detection exceeds 90%. In this case study, only three cameras are used, so the number of features input is 6x4 = 24. If Five-Eyes (5 cameras. 6x4x2=48 features), anomaly detection performance exceeding that can be expected. 


### [Industrial applicability]
This invention is applicable not only to connector terminal inspection, but also to visual inspection of three-dimensional objects; we simply chose connector inspection as an example that can be experimented with very easily using VR.

The challenge is that five cameras are required. This is a cost issue rather than a technical one. In this case, "Five-Eyes (scheme)," which covers X and Y axes, was selected as an example. However, it might be dependent on the inspected object, Simple "Double-Eyes method," with one axis only, could be sufficiently accurate. In the terminal inspection of male connectors in this case, even three cameras would produce a considerable degree of accuracy.

If information is generated and learned by computer through VR, the time required to prepare training data is small and no loss of production sites will occur. 


### [Supplement]
The cost of equipment elements using this invention and the task time for anomaly detection are roughly as follows.


**(Estimated cost amortization)**

カメラ5台：　10万円
照明： 5万円
コンピュータ周辺(Raspberry Pi4相当の場合): 2万円
トラバース装置：　10万円
その他治具：　10万円
合計：　37万円
### 原価償却年数：　2年（24か月）
### 1月当たりの償却費：　37万円/24月 = 1.54万円

**(Approximate task time)**

１つの予測作業について、5秒程度（Julia言語でプログラムが組まれている場合）
## ※
### 人件費（特に学習に伴う）を含んでいません。
### タスクタイムを短縮するときには、コンピュータを強力なものに取り換える必要があります。

In this case study, we are using a high-performance language called Julia, which is considered suitable for scientific calculations. Since technometrics are used, there are many custom-made calculations, and the task time is significantly longer in Python, which is slow in computation.

**(Fig. 36: Computational speed of Julia and Python languages)**

![image3-20-36](/2023-02-23-QEUR22_VINSP19/image3-20-36.jpg)

