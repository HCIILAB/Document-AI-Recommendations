<h3 align="center"> Datasets for </h3>
<h1 align="center"> Visual Information Extraction </h1>

<h2> 🗒️List of Index </h2>

- [SROIE](#sroie)
- [CORD](#cord)
- [FUNSD](#funsd)
- [XFUND](#xfund)
- [EPHOIE](#ephoie)
- [CER-VIR](#cer-vir)
- [EATEN](#eaten)
- [WildReceipt](#wildreceipt)
- [Kleister](#kleister)
- [DeepForm](#deepform)
- [SIBR](#sibr)


<br>

# SROIE

<p>
    <a href="https://guillaumejaume.github.io/FUNSD/work/">
        <img alt="License" src="https://img.shields.io/badge/License-CC BY 4.0-c1c1c1"></img>
    </a>
    <img src="https://i.creativecommons.org/l/by/4.0/88x31.png">
    <img align=right alt="Commercial" src="https://img.shields.io/badge/Commercial-✔️-brightgreen"></img>
    <img align=right alt="Adapt" src="https://img.shields.io/badge/Adapt-✔️-brightgreen"></img>
    <img align=right alt="Share" src="https://img.shields.io/badge/Share-✔️-brightgreen"></img>
</p>
<br>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td>626</td>
        <td>-</td>
        <td>347</td>
        <td>Receipt</td>
        <td rowspan=2>English</td>
        <td rowspan=2>
            <p>
                <a href="https://rrc.cvc.uab.es/?ch=13">
                    <img alt="Link2" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
                <br>
                <a href="https://github.com/zzzDavid/ICDAR-2019-SROIE">
                    <img alt="Link2" src="https://img.shields.io/badge/UnOfficial-pink"></img>
                </a> 
            </p>
        </td>
        <td rowspan=2>Entity Extraction</td>
        <td rowspan=2>Entity F1-score</td>
    </tr>
</table>

SROIE is a dataset for the 2019 ICDAR Robust Reading Challenge on Scanned Receipts OCR and Information Extraction competition. It contains 973 samples, 626 for training and 347 for testing. Each receipt contains four kinds of key entities: Company, Address, Date, and Total. 

OCR results and strings of key entities for each sample are provided. To do VIE with token tagging approaches like LayoutLM, the category of each word is required. You may use [rule-based methods](https://github.com/antoinedelplace/Chargrid) or re-label the data manually.

<p align=center>
    <img src="../img/dataset_img/SROIE_1.jpg" width=200>
</p>

It is worth noting that the quality of the data annotation will greatly affect the results of VIE. We launched experiments with [ViBERTgrid](https://github.com/ZeningLin/ViBERTgrid-PyTorch). When the model is trained with high quality annotations (re-labelled manually), the entity F1 can reach 97+. When poor quality annotations (rule-based matching) are used to train the model, the entity F1 is only 60.

<br>

# CORD

<p>
    <a href="https://guillaumejaume.github.io/FUNSD/work/">
        <img alt="License" src="https://img.shields.io/badge/License-CC BY 4.0-c1c1c1"></img>
    </a>
    <img src="https://i.creativecommons.org/l/by/4.0/88x31.png">
    <img align=right alt="Commercial" src="https://img.shields.io/badge/Commercial-✔️-brightgreen"></img>
    <img align=right  alt="Adapt" src="https://img.shields.io/badge/Adapt-✔️-brightgreen"></img>
    <img align=right alt="Share" src="https://img.shields.io/badge/Share-✔️-brightgreen"></img>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td rowspan=2>800</td>
        <td rowspan=2>100</td>
        <td rowspan=2>100</td>
        <td rowspan=2>Receipt</td>
        <td rowspan=2>English</td>
        <td rowspan=2>
            <p>
                <a href="https://github.com/clovaai/cord">
                    <img alt="Link" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td rowspan=1>Entity Extraction</td>
        <td rowspan=1>Entity F1-score</td>
    </tr>
    <tr>
        <td rowspan=1>Structure Parsing</td>
        <td rowspan=1>Structured Field F1-score </td>
    </tr>
</table>

CORD is an English receipt dataset proposed by Colva AI. 1000 samples are currently publicly available, 800 for training, 100 for validation, and 100 for testing. The receipt images are obtained through cameras, hence inteference like paper bending and background noise may inevitably occur. The data contains high-quality annotations, key labels for each words and linking between entities are provided. The dataset contains a total of four main key information categories such as payment information, and each main category can be further divided into 30 sub-key fields. Unlike other datasets, entities in CORD are hierarchically related. Models should be able to extract all the structured fields, which makes the task challenging.

<p align=center>
    <img src="../img/dataset_img/CORD_1.png" width=600>
</p>

<br>

# FUNSD

<p>
    <a href="https://guillaumejaume.github.io/FUNSD/work/">
        <img alt="License" src="https://img.shields.io/badge/License-Customized-c1c1c1"></img>
    </a>
    <img align=right alt="Commercial" src="https://img.shields.io/badge/Commercial-✖️-ff0000"></img>
    <img align=right alt="Research" src="https://img.shields.io/badge/Research-✔️-brightgreen"></img>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td rowspan=2>149</td>
        <td rowspan=2>-</td>
        <td rowspan=2>50</td>
        <td rowspan=2>Forms</td>
        <td rowspan=2>English</td>
        <td rowspan=2>
            <p>
                <a href="https://guillaumejaume.github.io/FUNSD/">
                    <img alt="Link" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td>Entity Extraction</td>
        <td>Entity F1-score</td>
    </tr>
    <tr>
        <td>Entity Linking</td>
        <td>Pair F1-score </td>
    </tr>
</table>

A dataset for Text Detection, Optical Character Recognition, Spatial Layout Analysis and Form Understanding. Contains 199 fully annotated forms, with 31485 words, 9707 semantic entities and 5304 relations. The OCR result of each text segment and word are given, and the category of each paragraph and linkings between entities are included in the annotations.

<p align=center>
    <img src="../img/dataset_img/FUNSD_1.jpg" width=500>
</p>

<br>

# XFUND

<p>
    <a href="">
        <img alt="License" src="https://img.shields.io/badge/License-CC BY NC SA 4.0-c1c1c1"></img>
        <img src="https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png">
    </a>
    <img align=right alt="Commercial" src="https://img.shields.io/badge/Commercial-✖️-ff0000"></img>
    <img align=right alt="Adapt" src="https://img.shields.io/badge/Adapt-✔️-brightgreen"></img>
    <img align=right alt="Share" src="https://img.shields.io/badge/Share-✔️-brightgreen"></img>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td rowspan=2>149*7</td>
        <td rowspan=2>-</td>
        <td rowspan=2>50*7</td>
        <td rowspan=2>Forms</td>
        <td rowspan=2>Chinese, Japanese, Spanish, French, Italian, German, Portuguese</td>
        <td rowspan=2>
            <p>
                <a href="https://github.com/doc-analysis/XFUND">
                    <img alt="Link" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td>Entity Extraction</td>
        <td>Entity F1-score</td>
    </tr>
    <tr>
        <td rowspan=1>Entity Linking</td>
        <td rowspan=1>Pair F1-score </td>
    </tr>
</table>

XFUND is a multilingual form understanding benchmark dataset that includes human-labeled forms with key-value pairs in 7 languages (Chinese, Japanese, Spanish, French, Italian, German, Portuguese). It is an extension of the FUNSD dataset, the annotations and evaluation metric are the same as FUNSD.

<p align=center>
    <img src="../img/dataset_img/XFUND_1.jpg" height=300>
</p>

<br>

# EPHOIE

<p>
    <a href="">
        <img alt="License" src="https://img.shields.io/badge/License-Customize-c1c1c1"></img>
    </a>
    <img align=right alt="Access" src="https://img.shields.io/badge/Access-Need Application-ffff00"></img>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td>1183</td>
        <td>-</td>
        <td>311</td>
        <td>Paper Head</td>
        <td>Chinese</td>
        <td>
            <p>
                <a href="https://github.com/HCIILAB/EPHOIEalysis/XFUND">
                    <img alt="Link" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td>Entity Extraction</td>
        <td>Entity F1-score</td>
    </tr>
</table>

THe EPHOIE Dataset contains 1,494 images which are collected and scanned from real examination papers of various schools in China, and the authors crop the paper head regions which contains all key information. The texts are composed of handwritten and printed Chinese characters in horizontal and arbitrary quadrilateral shape. Complex layouts and noisy background also enhance the generalization of EPHOIE dataset. The dataset contains a total of 11 key categories including name, class, student id, and so on. Annotations of each character are given, hence we can directly apply token classification models using the original labels.

<p align=center>
<img src="../img/dataset_img/EPHOIE_1.png" width=450 height=350>
</p>

<br>

# CER-VIR

<p>
    <a href="">
        <img alt="License" src="https://img.shields.io/badge/License-CC BY NC SA 4.0-c1c1c1"></img>
        <img src="https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png">
    </a>
    <img align=right alt="Commercial" src="https://img.shields.io/badge/Commercial-✖️-ff0000"></img>
    <img align=right alt="Adapt" src="https://img.shields.io/badge/Adapt-✔️-brightgreen"></img>
    <img align=right alt="Share" src="https://img.shields.io/badge/Share-✔️-brightgreen"></img>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td>2989</td>
        <td>-</td>
        <td>1200</td>
        <td rowspan=1>Receipt</td>
        <td rowspan=1>Chinese <br> English</td>
        <td rowspan=1>
            <p>
                <a href="https://github.com/jiangxiluning/CER-VIR">
                    <img alt="Link" src="https://img.shields.io/badge/Data Link-Official-2e8b57"></img>
                </a>
                <br>
                <a href="https://competition.huaweicloud.com/information/1000041696/circumstance">
                    <img alt="Link" src="https://img.shields.io/badge/Description-Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td rowspan=1>Structure Parsing</td>
        <td rowspan=1>
            <a href="https://competition.huaweicloud.com/information/1000041696/circumstance">Entity Matching Score</a
        </td>
    </tr>
</table>

The CER-VIR dataset contains receipts in both Chinese and English. Each sample contains key information including company, date, total, tax and items. The item field can be futherly divided into three subkeys including item name, item count, and item unit price. The task aims to extract all the key fields from a given sample, including all the subkeys in the item field. The extracted result should be formatted, for example, each date entity should be given in forms YYYY-MM-DD. The OCR result is provided for reference, and the annotation of the key entities are given in forms of formatted strings (it may be different from the actual content shown in the image), which makes the task much more challenging than other existing VIE benchmarks.

<p align=center>
    <img src="../img/dataset_img/CER_VIR.png" width=500>
</p>

<br>

# EATEN

<p>
     <img alt="License" src="https://img.shields.io/badge/License-Unknown-c1c1c1"></img>
    </a>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td>271440</td>
        <td>30160</td>
        <td>400</td>
        <td rowspan=1>Train Ticket</td>
        <td rowspan=3>Chinese</td>
        <td rowspan=3>
            <p>
                <a href="https://github.com/beacandler/EATEN">
                    <img alt="Link" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td rowspan=3>Entity Extraction</td>
        <td rowspan=1>Mean Entity Accuracy</td>
    </tr>
    <tr>
        <td>88200</td>
        <td>9800</td>
        <td>2000</td>
        <td>Passport</td>
        <td>Mean Entity Accuracy</td>
    </tr>
    <tr>
        <td>178200</td>
        <td>19800</td>
        <td>2000</td>
        <td>Business Card</td>
        <td>Entity F1-score</td>
    </tr>
</table>

The EATEN dataset covers three scenarios: Train Ticket, Passport, and Business Card. 

The train ticket subset includes a total of 2k real images and 300k synthetic images. Real images were shot in a finance department with inconsistent lighting conditions, orientations, background noise, imaging distortions. The train tickets contains 8 key categories.

The passport subset includes a total 100k synthetic images with 7 key categories. 

The business card subset contains 200k synthetic images with 10 key categories. The positions of the key entities are not constant and some entities may not exist, which is a challenge for appling VIE.

<p align=center>
    <img src="../img/dataset_img/EATEN_1.jpg" width=500>
</p>

The Meadn Entity Accuracy is calculated as shown below
$$
mEA = \sum_{i=0}^{I-1}\mathbb{I}(y^i==g^i)/I
$$
where $y^i$ denotes the prediction of the $i$th field, $g^i$ denotes the corresponding ground-truth, $I$ denotes the number of entities and $\mathbb{I}$ is the indicator function that return 1 if $y^i == g^i$ else return 0.

<br>

# WildReceipt

<p>
    <img alt="License" src="https://img.shields.io/badge/License-Apache License 2.0-c1c1c1"></img>
    <img align=right alt="Commercial" src="https://img.shields.io/badge/Commercial-✔️-brightgreen"></img>
    <img align=right  alt="Adapt" src="https://img.shields.io/badge/Adapt-✔️-brightgreen"></img>
    <img align=right alt="Share" src="https://img.shields.io/badge/Share-✔️-brightgreen"></img>
    </a>
</p>

*The WildReceipt dataset is introduced by the [mmocr](https://github.com/open-mmlab/mmocr) repository, which follow the Apache License 2.0.*

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td rowspan=2>1740</td>
        <td rowspan=2>-</td>
        <td rowspan=2>472</td>
        <td rowspan=2>Receipt</td>
        <td rowspan=2>English</td>
        <td rowspan=2>
            <p>
                <a href="https://github.com/open-mmlab/mmocr/blob/12558969ee6f11b469a8e964a57730d5df3df6b1/docs/en/datasets/kie.md">
                    <img alt="Link" src="https://img.shields.io/badge/Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td rowspan=1>Entity Extraction</td>
        <td rowspan=1>Entity F1-score</td>
    </tr>
    <tr>
        <td rowspan=1>Entity Linking</td>
        <td rowspan=1>
            <a href="https://github.com/open-mmlab/mmocr/blob/12558969ee6f11b469a8e964a57730d5df3df6b1/configs/kie/sdmgr/README.md">Node F1-score & Edge F1-score</a>
        </td>
    </tr>
</table>

The WildReceipt dataset has two version: the CloseSet and OpenSet. 

The CloseSet divides text boxes into 26 categories. There are 12 key-value pairs of fine-grained key information categories, such as (Prod_item_value, Prod_item_key), (Prod_price_value, Prod_price_key) and (Tax_value, Tax_key), plus two more "do not care" categories: Ignore and Others. The objective of the CloseSet is to apply Entity Extraction.

The OpenSet have only 4 possible categories: background, key, value, and others. The connectivity between nodes are annotated as edge labels. If a pair of key-value nodes have the same edge label, they are connected by an valid edge. The objective of the OpenSet is to extract pairs from the given sample.

<p align=center>
    <img src="../img/dataset_img/WildReceipt_1.jpeg">
</p>

<br>

# Kleister

<p>
     <img alt="License" src="https://img.shields.io/badge/License-Unknown-c1c1c1"></img>
    </a>
</p>

<table align=center>
    <th colspan=3>Number of Samples</th>
    <th rowspan=2>Type</th>
    <th rowspan=2>Language</th>
    <th rowspan=2>Access Link</th>
    <th rowspan=2>Task</th>
    <th rowspan=2>Evaluation Metric</th>
    <tr>
        <th>Train</th>
        <th>Validate</th>
        <th>Test</th>
    </tr>
    <tr>
        <td>254</td>
        <td>83</td>
        <td>203</td>
        <td rowspan=1>Contracts</td>
        <td rowspan=2>English</td>
        <td rowspan=1>
            <p>
                <a href="https://github.com/applicaai/kleister-nda">
                    <img alt="Link" src="https://img.shields.io/badge/NDA-Official-2e8b57"></img>
                </a>
            </p>
        </td>
        <td rowspan=2>Entity Extraction</td>
        <td rowspan=2>Entity F1-score</td>
    </tr>
    <tr>
        <td>1729</td>
        <td>440</td>
        <td>609</td>
        <td>Financial Reports</td>
        <td>
            <a href="https://github.com/applicaai/kleister-charity">
                <img alt="Link" src="https://img.shields.io/badge/Charity-Official-2e8b57"></img>
            </a>
        </td>
    </tr>
</table>

The Kleister dataset contains two subset: NDA and Charity. 

The goal of the NDA task is to Extract the key information from NDAs (Non-Disclosure Agreements) about the involved parties, jurisdiction, contract term, and effective date. It contains 540 documents with 3229 pages.

The goal of the Charity task is to retrieve 8 kinds of key information including charity address (but not other addresses), charity number, charity name and its annual income and spending in GBP (British Pounds) in PDF files published by British charities. It contains 2788 financial reports with 61643 pages in total.

<br>

# DeepForm

<br>

# SIBR

<br>