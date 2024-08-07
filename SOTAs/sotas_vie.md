<h3 align="center"> Visual Information Extraction </h3>
<h1 align="center"> SOTAs </h1>

This page serves as a compilation of the performance metrics achieved by various visual information extraction algorithms on public benchmarks. The data presented here are collected from research papers as well as official code repositories.

<h2>🎖️Commonly Used Metrics</h2>

<h3><b>F1-score</b></h3>

Given the prediction of the model and the ground-truth, if the predicted content is exactly consistent with the ground-truth, it will be recorded as a true positive(TP) sample. Let $N_p$ denotes the number of predictions, $N_g$ for the number of ground-truths, $N_t$ for the number of TP samples, then we have

$$
precision = \frac{N_t}{N_p}
$$

$$
recall = \frac{N_t}{N_g}
$$

$$
F1 = \frac{2 \times precision \times recall}{precision + recall}
$$

<h4><b>Entity F1 score</b></h4>

The Entity F1 score is a metric used for the Entity Extraction task (also known as Semantic Entity Recognition, SER). It measures the accuracy of the predicted string and its corresponding category with respect to the ground-truth. When both the predicted string and category match the ground-truth, it is considered a TP sample. 

If you are using BIO-tagging models, such as LayoutLM, LiLT, etc., you can utilize the [seqeval](https://github.com/chakki-works/seqeval) library for metric calculation.

<h4><b>Linking F1 score</b></h4>

Used as a metric for Entity Linking (or Relation Extraction, RE) task. **Models takes the ground-truths of Entity Extraction as input**, then predicts the linking relation between entities. A linking is considered as TP if and only if the predicted pair exists in the ground-truth pairs.


<h4><b>Pair F1 score</b></h4>

Used as a metric for end-to-end pair extraction task. A prediction is considered TP if and only if the predicted key-value pair exactly matches the ground-truth pair.

<h4><b>QA F1 score</b></h4>

The metric is used specifically for LLM-based models.

For Entity Extraction, two types of operations are employed:
1. The model takes the text content of an entity as input and predicts its corresponding key category. Used for datasets like FUNSD, where each key category contains multiple entities.
2. The model takes the key category name as input and predicts the corresponding text content. Used for datasets where each key category contains one or no entity.

For Entity Linking, the model takes the question entity as input, then predicts the corresponding answer entity.

⚠️ **It is worth-noting that, the QA F1 score is a more relaxed metric compared to the conventional settings, since prior information like the entity span is provided to the model. Therefore, scores obtained through the QA pipeline cannot be directly compared with the scores obtained through the conventional settings.** In this section, we will list these QA scores separately.


<h3><b>Edit Distance Score</b></h3>

The edit distance between the prediction string and ground-truth of a key category is calculated as follow

$$
score = 1 - \frac{i + d + m}{N}
$$

where $i$, $d$, $m$, $N$ denotes the number of insertions, number of deletions, number of modifications and the total number of instances occurring in the ground truth, respectively.

The document parsing task in CORD employs this metric. The [zhang-shasha](https://github.com/timtadh/zhang-shasha) library can be used to calculate the edit distance between strings.

<br>

<h2>🗒️List of Index</h2>

- [SROIE](#sroie)
- [CORD](#cord)
- [FUNSD](#funsd)
- [XFUND](#xfund)
- [EPHOIE](#ephoie)
- [DeepForm](#deepform)
- [Kleister Charity](#kleister-charity)

---

## SROIE

The SROIE dataset takes the entity micro F1-score as the evaluation metric. The dataset contains 4 key categories, each category contains one or no entity. The dataset consists of four key categories, with each category containing one or no entity. In this metric, if the predicted string of a key category is consistent with the ground-truth string, it will be recorded as a true positive (TP) sample. The total number of TP samples, total number of predictions, and total number of ground-truth strings are used to calculate the micro-F1 score.

You can find the evaluation scripts for the SROIE dataset on the [ICDAR2019 SROIE official page](https://rrc.cvc.uab.es/?ch=13&com=downloads) (Download tab, Task 3 Evaluation script).

<table align="center">
<tr>
    <th > Type </th>
    <th colspan=2> Approach </th>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
    <th> QA F1 </th>
</tr>
<tr>
    <td rowspan=2>Grid-based</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#vibertgrid">ViBERTgrid</a></td>
    <td>BERT-base</td>
    <td>-</td>
    <td>-</td>
    <td>96.25</td>
    <td>-</td>
</tr>
<tr>
    <td>RoBERTa-base</td>
    <td>-</td>
    <td>-</td>
    <td>96.40</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=4>GNN-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#pick">PICK</a></td>
    <td>-</td>
    <td>-</td>
    <td>96.12</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#matchvie">MatchVIE</a></td>
    <td>-</td>
    <td>-</td>
    <td>96.57</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#graphdoc">GraphDoc</a></td>
    <td>-</td>
    <td>-</td>
    <td>98.45</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#formnetv2">FormNetV2</a></td>
    <td>-</td>
    <td>-</td>
    <td>98.31</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=19>Large Scale Pre-trained</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlm">LayoutLM</a></td>
    <td>base</td>
    <td>94.38</td>
    <td>94.38</td>
    <td>94.38</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>95.24</td>
    <td>95.24</td>
    <td>95.24</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlmv2">LayoutLMv2</a></td>
    <td>base</td>
    <td>96.25</td>
    <td>96.25</td>
    <td>96.25</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>99.04</td>
    <td>96.61</td>
    <td>97.81</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#tilt">TILT</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>97.65</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>98.10</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#bros">BROS</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>95.91</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>96.62</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=3><a href="../Approaches/approaches_vie.md/#structext">StrucTexT</a></td>
    <td>eng-base</td>
    <td>-</td>
    <td>-</td>
    <td>96.88</td>
    <td>-</td>
</tr>
<tr>
    <td>chn&eng-base</td>
    <td>-</td>
    <td>-</td>
    <td>98.27</td>
    <td>-</td>
</tr>
<tr>
    <td>chn&eng-large</td>
    <td>-</td>
    <td>-</td>
    <td>98.70</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#wukong-reader">WUKONG-READER</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>96.88</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>98.15</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=1><a href="../Approaches/approaches_vie.md/#ernie-layout">ERNIE-layout</a></td>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.55</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#qgn">QGN</a></td>
    <td>-</td>
    <td>-</td>
    <td>97.90</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutmask">LayoutMask</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>96.87</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.27</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#hgalayoutlm">HGALayoutLM</a></td>
    <td>base</td>
    <td>99.58</td>
    <td>99.48</td>
    <td>99.53</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>99.69</td>
    <td>99.53</td>
    <td>99.61</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=6>End-to-End</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#trie">TRIE</a></td>
    <td>ground-truth</td>
    <td>-</td>
    <td>-</td>
    <td>96.18</td>
    <td>-</td>
</tr>
<tr>
    <td>end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>82.06</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#vies">VIES</a></td>
    <td>ground-truth</td>
    <td>-</td>
    <td>-</td>
    <td>96.12</td>
    <td>-</td>
</tr>
<tr>
    <td>end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>91.07</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=1><a href="../Approaches/approaches_vie.md/#kuang-cfam">Kuang CFAM</a></td>
    <td>end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>85.87</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approached_vie.md/#omniparser">OmniParser</a></td>
    <td>-</td>
    <td>-</td>
    <td>85.60</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=10>LLM-based</td>
    <td colspan=2><a href="../Approaches/approached_vie.md/#hrvda">HRVDA</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>91.00</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#monkey">Monkey</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>41.90</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approached_vie.md/#textmonkey">TextMonkey</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>47.00</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approached_vie.md/#minimonkey">MiniMonkey</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>70.30</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#unidoc">UniDoc</a></td>
    <td>224</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>1.40</td>
</tr>
<tr>
    <td>336</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>2.92</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docpedia">DocPedia</a></td>
    <td>224</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>17.01</td>
</tr>
<tr>
    <td>336</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>21.44</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutllm">LayoutLLM</a></td>
    <td>Llama2-7B-chat</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>70.97</td>
</tr>
<tr>
    <td>Vicuna-1.5-7B</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>72.12</td>
</tr>
</tr>
    <td rowspan=4>Other Methods</td>
    <td rowspan=4><a href="../Approaches/approaches_vie.md/#tcpn">TCPN</a></td>
    <td>TextLattice</td>
    <td>-</td>
    <td>-</td>
    <td>96.54</td>
    <td>-</td>
</tr>
<tr>
    <td>Tag, ground-truth</td>
    <td>-</td>
    <td>-</td>
    <td>95.46</td>
    <td>-</td>
</tr>
</tr>
    <td>Tag, end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>91.21</td>
    <td>-</td>
</tr>
<tr>
    <td>Tag&Copy, end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>91.93</td>
    <td>-</td>
</tr>

</table>

<br>

## CORD

The authors of the CORD dataset, the Clova-AI team, have not explicitly specified the task type and evaluation metrics for this dataset. However, upon reviewing the source code of [Donut](https://github.com/clovaai/donut/blob/217cffb111a57ebce1025ff84a722a8d9914e05b/donut/util.py#L242), one of Clova-AI's works, it is apparent that they evaluate the model's performance in **Document Structure Parsing**. In a typical receipt, various details about the purchased items are provided, such as their names, quantities, and unit prices. These entities have a hierarchical relationship, and a receipt can be represented by a JSON-like structure as shown below:
```json
{
    "menu": [
        {
            "nm": "EGG TART",
            "cnt": "1",
            "price": "13,000"
        },
        {
            "nm": "CHOCO CUS ARD PASTRY",
            "cnt": "2",
            "price": "24,000"
        },
        {
            "nm": "REDBEAN BREAD",
            "cnt": "1",
            "price": "9,000"
        }
    ],
    "total": {
        "total_price": "46,000",
        "cashprice": "50,000",
        "changeprice": "4,000"
    }
}
```
The evaluation metric used by [Donut](https://github.com/clovaai/donut/blob/217cffb111a57ebce1025ff84a722a8d9914e05b/donut/util.py#L242) is the **TED Acc** (Tree Edit Distance Accuracy), which measures the similarity between the predicted JSON and the ground-truth. 

In addition to Document Structure Parsing, [Donut](https://github.com/clovaai/donut/blob/217cffb111a57ebce1025ff84a722a8d9914e05b/donut/util.py#L242) also evaluates the model's performance on the **Entity Extraction** task, using the **Entity F1 score** as the evaluation metric. Most SOTA models follows this evaluation pipeline.

Another work by clovvai, [SPADE](https://github.com/clovaai/spade/blob/master/spade/postprocess/eval.py), evaluate the model's performance on **Document Structure Parsing** through a relaxed **structured field F1-score**. This evaluation measures the accuracy of dependency parsing by computing the F1 score of predicted edges. The task is simplified by not considering differences between predictions and ground truth in certain fields (such as `store name`, `menu name`, and `item name`) when the edit distance is less than 2 or when the ratio of edit distance to the ground truth string length is less than or equal to 0.4. Details can be found in their [paper](https://arxiv.org/pdf/2005.00642.pdf) (Section 5.3 and A.2).

Some other works, such as [BROS](https://github.com/clovaai/bros/blob/master/lightning_modules/bros_spade_rel_module.py), evaluate the model's performance on **Entity Linking** using the **Linking F1 score**.


<table align="center">
<tr>
    <th rowspan=2> Type </th>
    <th rowspan=2 colspan=2> Approach </th>
    <th colspan=4> Entity Extraction </th>
    <th colspan=3> Entity Linking </th>
    <th colspan=4> Document Structure Parsing </th>
</tr>
<tr>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
    <th> QA F1 </th>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
    <th> TED Acc </th>
</tr>
<tr>
    <td rowspan=3>GNN-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#graphdoc">GraphDoc</a></td>
    <td>-</td>
    <td>-</td>
    <td>96.93</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#formnet">FormNet</a></td>
    <td>98.02</td>
    <td>96.55</td>
    <td>97.28</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#formnetv2">FomNetV2</a></td>
    <td>-</td>
    <td>-</td>
    <td>97.70</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=31>Large Scale Pre-trained</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlm">LayoutLM</a></td>
    <td>base</td>
    <td>94.37</td>
    <td>95.08</td>
    <td>94.72</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>94.32</td>
    <td>95.54</td>
    <td>94.93</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlmv2">LayoutLMv2</a></td>
    <td>base</td>
    <td>94.53</td>
    <td>95.39</td>
    <td>94.95</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>95.65</td>
    <td>96.37</td>
    <td>96.01</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlmv3">LayoutLMv3</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>96.56</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.46</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docformer">DocFormer</a></td>
    <td>base</td>
    <td>96.52</td>
    <td>96.14</td>
    <td>96.33</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>97.25</td>
    <td>96.74</td>
    <td>96.99</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#tilt">TILT</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>95.11</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>96.33</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docformer">BROS</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>96.50</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>95.73</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.28</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>97.40</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#udoc">UDoc</a></td>
    <td>UDoc</td>
    <td>-</td>
    <td>-</td>
    <td>96.64</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>UDoc*</td>
    <td>-</td>
    <td>-</td>
    <td>96.86</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#lilt">LiLT</a></td>
    <td>[EN-RoBERTa]base</td>
    <td>-</td>
    <td>-</td>
    <td>96.07</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>[InfoXLM]base</td>
    <td>-</td>
    <td>-</td>
    <td>95.77</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#docrel">DocReL</a></td>
    <td>-</td>
    <td>-</td>
    <td>97.00</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#wukong-reader">WUKONG-READER</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>96.54</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.27</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=1><a href="../Approaches/approaches_vie.md/#ernie-layout">ERNIE-layout</a></td>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>96.99</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#qgn">QGN</a></td>
    <td>-</td>
    <td>-</td>
    <td>96.84</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#geolayoutlm">GeoLayoutLM</a></td>
    <td>-</td>
    <td>-</td>
    <td>97.97</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>99.45</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#graphlayoutlm">GraphLayoutLM</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>97.28</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.75</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#hgalayoutlm">HGALayoutLM</a></td>
    <td>base</td>
    <td>97.89</td>
    <td>97.16</td>
    <td>97.52</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>97.97</td>
    <td>97.38</td>
    <td>97.67</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docformerv2">DocFormerv2</a></td>
    <td>base</td>
    <td>97.51</td>
    <td>96.10</td>
    <td>96.80</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>97.71</td>
    <td>97.70</td>
    <td>97.70</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#doctr">DocTr</a></td>
    <td>-</td>
    <td>-</td>
    <td>98.20</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>94.40</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutmask">LayoutMask</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>96.99</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>97.19</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=5>End-to-End</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#donut">Donut</a></td>
    <td>-</td>
    <td>-</td>
    <td>84.10</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>90.90</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#esp">ESP</a></td>
    <td>-</td>
    <td>-</td>
    <td>95.65</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#udop">UDOP</a></td>
    <td>-</td>
    <td>-</td>
    <td>97.58</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#donut">CREPE</a></td>
    <td>-</td>
    <td>-</td>
    <td>85.00</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#omniparser">OmniParser</a></td>
    <td>-</td>
    <td>-</td>
    <td>84.80</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>88.00</td>
</tr>
<tr>
    <td rowspan=3>LLM-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#hrvda">HRVDA</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>89.30</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutllm">LayoutLLM</a></td>
    <td>Llama2-7B-chat</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>62.21</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>Vicuna-1.5-7B</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>63.10</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=8>Other Methods</td>
    <td rowspan=8><a href="../Approaches/approaches_vie.md/#spade">SPADE</a></td>
    <td>♠ CORD, oracle input</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>92.50</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ CORD</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>88.20</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ CORD+</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>87.40</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ CORD++</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>83.10</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ w/o TCM, CORD, oracle input</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>91.50</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ w/o TCM, CORD</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>87.40</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ w/o TCM, CORD+</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>86.10</td>
    <td>-</td>
</tr>
<tr>
    <td>♠ w/o TCM, CORD++</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>82.60</td>
    <td>-</td>
</tr>

</table>

<br>

## FUNSD

FUNSD comprises two tasks: **Entity Extraction** and **Entity Linking**. The **Entity Extraction** task requires extracting `header`, `question`, and `answer` entities from the document, and employs **Entity F1 Score** as the evaluation metric. The **Entity Linking** task focuses on linking predictions between `question` and `answer` entities, and uses **Linking F1 Score** as the evaluation metric.

It is worth noting that, in most mainstream approaches, these two subtasks are considered independent. For instance, LayoutLM's Entity Linking [official implementation](https://github.com/microsoft/unilm/blob/master/layoutlmft/layoutlmft/modules/decoders/re.py) takes the ground-truth of `question` and `answer` entities as input and predict the linkings only, without considering the performance of Entity Extraction.

Real-world applications require extracting all key-value pairs from the document, which involves combining the EE and EL tasks to predict the entire kv-pair content. We termed this task as the **End-to-end Pair Extraction**. It presents challenges such as error accumulation and text segment aggregation. Regrettably, only a few studies have recognized and addressed these challenges, while the majority of research continues to follow the conventional EE+EL setting. We hope to see more studies that delve into this particular case.

<table align="center">
<tr>
    <th rowspan=2> Type </th>
    <th rowspan=2 colspan=2> Approach </th>
    <th colspan=4> Entity Extraction </th>
    <th colspan=4> Entity Linking </th>
    <th colspan=3> E2E Pair Extraction </th>
</tr>
<tr>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
    <th> QA F1 </th>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
    <th> QA F1 </th>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
</tr>
<tr>
    <td rowspan=1>Grid-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#msau-paf">MSAU-PAF</a></td>
    <td>-</td>
    <td>-</td>
    <td>83.00</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>75.00</td>
</tr>
<tr>
    <td rowspan=4>GNN-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#graphdoc">GraphDoc</a></td>
    <td>-</td>
    <td>-</td>
    <td>87.77</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#matchvie">MatchVIE</a></td>
    <td>-</td>
    <td>-</td>
    <td>81.33</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#formnet">FormNet</a></td>
    <td>-</td>
    <td>-</td>
    <td>84.69</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#formnetv2">FormNetV2</a></td>
    <td>-</td>
    <td>-</td>
    <td>92.51</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<td rowspan=43>Large Scale Pre-trained</td>
<td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlm">LayoutLM</a></td>
        <td>base</td>
        <td>75.97</td>
        <td>81.55</td>
        <td>78.66</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>75.96</td>
    <td>82.19</td>
    <td>78.95</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlmv2">LayoutLMv2</a></td>
        <td>base</td>
        <td>80.29</td>
        <td>85.39</td>
        <td>82.76</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>83.24</td>
    <td>85.19</td>
    <td>84.20</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=4><a href="../Approaches/approaches_vie.md/#layoutlxlm">LayoutXLM</a></td>
        <td>base, Language Specific Fine-tuning</td>
        <td>-</td>
        <td>-</td>
        <td>79.40</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>54.83</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large, Language Specific Fine-tuning</td>
    <td>-</td>
    <td>-</td>
    <td>82.25</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>64.04</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>base, Multitask Fine-tuning</td>
    <td>-</td>
    <td>-</td>
    <td>79.24</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>66.71</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large, Multitask Fine-tuning</td>
    <td>-</td>
    <td>-</td>
    <td>80.68</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>76.83</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutlmv3">LayoutLMv3</a></td>
        <td>base</td>
        <td>-</td>
        <td>-</td>
        <td>90.29</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>92.08</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#xylayoutlm">XYLayoutLM</a></td>
    <td>-</td>
    <td>-</td>
    <td>83.35</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#selfdoc">SelfDoc</a></td>
    <td>-</td>
    <td>-</td>
    <td>83.36</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#DocFormer">DocFormer</a></td>
        <td>base</td>
        <td>80.76</td>
        <td>86.09</td>
        <td>83.34</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>82.29</td>
    <td>86.94</td>
    <td>84.55</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#structurallm">StructuralLM-large</a></td>
    <td>83.52</td>
    <td>-</td>
    <td>85.14</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#bros">BROS</a></td>
    <td>base</td>
    <td>81.16</td>
    <td>85.02</td>
    <td>83.05</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>71.46</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>82.81</td>
    <td>86.31</td>
    <td>84.52</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>77.01</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=3><a href="../Approaches/approaches_vie.md/#structext">StrucTexT</a></td>
    <td>eng-base</td>
    <td>-</td>
    <td>-</td>
    <td>83.09</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>44.10</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>chn&eng-base</td>
    <td>-</td>
    <td>-</td>
    <td>84.83</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>70.45</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>chn&eng-large</td>
    <td>-</td>
    <td>-</td>
    <td>87.56</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>74.21</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#udoc">UDoc</a></td>
    <td>UDoc</td>
    <td>-</td>
    <td>-</td>
    <td>87.96</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>UDoc*</td>
    <td>-</td>
    <td>-</td>
    <td>87.93</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=4><a href="../Approaches/approaches_vie.md/#lilt">LiLT</a></td>
    <td>[En RoBERTa]base</td>
    <td>87.21</td>
    <td>89.65</td>
    <td>88.41</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>[InfoXLM]base</td>
    <td>84.67</td>
    <td>87.09</td>
    <td>85.86</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>[InfoXLM]base, Language Specific Fine-tuning</td>
    <td>-</td>
    <td>-</td>
    <td>84.15</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>62.76</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>[InfoXLM]base, Multitask Fine-tuning</td>
    <td>-</td>
    <td>-</td>
    <td>85.74</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>74.07</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#docrel">DocReL</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>46.10</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#wukong-reader">WUKONG-READER</a></td>
    <td>base</td>
    <td>-</td>
    <td>-</td>
    <td>91.52</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>93.62</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=1><a href="../Approaches/approaches_vie.md/#ernie-layout">ERNIE-layout</a></td>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>93.12</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#geolayoutlm">GeoLayoutLM</a></td>
    <td>-</td>
    <td>-</td>
    <td>92.86</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>89.45</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#kvpformer">KVPFormer</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>90.86</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#graphlayoutlm">GraphLayoutLM</a></td>
        <td>base</td>
        <td>-</td>
        <td>-</td>
        <td>93.15</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>-</td>
    <td>-</td>
    <td>94.39</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#hgalayoutlm">HGALayoutLM</a></td>
        <td>base</td>
        <td>94.84</td>
        <td>93.80</td>
        <td>94.32</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>95.67</td>
    <td>94.95</td>
    <td>95.31</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docformerv2">DocFormerv2</a></td>
    <td>base</td>
    <td>89.15</td>
    <td>87.60</td>
    <td>88.37</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>89.88</td>
    <td>87.92</td>
    <td>88.89</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#doctr">DocTr</a></td>
    <td>-</td>
    <td>-</td>
    <td>84.00</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>73.90</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docformerv2">DocFormerv2</a></td>
        <td>base</td>
        <td>89.15</td>
        <td>87.60</td>
        <td>88.37</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td>large</td>
    <td>89.88</td>
    <td>87.92</td>
    <td>88.89</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutmask">LayoutMask</a></td>
        <td>base</td>
        <td>-</td>
        <td>-</td>
        <td>92.91</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
    </tr>
    <tr>
        <td>large</td>
        <td>-</td>
        <td>-</td>
        <td>93.20</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
</tr>
<tr>
    <td rowspan=2>End-to-End</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#esp">ESP</a></td>
    <td>-</td>
    <td>-</td>
    <td>91.12</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>88.88</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
<td colspan=2><a href="../Approaches/approaches_vie.md/#udop">UDOP</a></td>
    <td>-</td>
    <td>-</td>
    <td>91.62</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=9>LLM-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#monkey">Monkey</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>24.10</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#textmonkey">TextMonkey</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>32.30</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#minimonkey">MiniMonkey</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>42.90</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#unidoc">UniDoc</a></td>
    <td>224</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>1.19</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>336</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>1.02</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#docpedia">DocPedia</a></td>
    <td>224</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>18.75</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>336</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>29.86</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#layoutllm">LayoutLLM</a></td>
    <td>Llama2-7B-chat</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>78.65</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td>Vicuna-1.5-7B</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>79.98</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
<tr>
    <td rowspan=1>Other Methods</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#spade">SPADE</a></td>
    <td>-</td>
    <td>-</td>
    <td>71.60</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>41.30</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</table>

<br>

## XFUND

XFUND is an multi-lingual extension of FUNSD, covering 7 languages: Chinese, Japanese, Spanish, French, Italian, German, and Portuguese. It contains 1,393 fully annotated forms, with each language containing 199 forms. The training set comprises 149 forms, while the test set includes 50 forms. XFUND also includes two subtasks: **Entity Extraction** and **Entity Linking**. Its follows the same evaluation protocol as FUNSD.

Note: In the following chart, the term `Avg.` represents the average score of the 7 non-English subsets. Some methods include the English subset in their reported average scores. To ensure a fair comparison, we made adjustments accordingly.

<table align="center">
<tr>
    <th rowspan=2> Type </th>
    <th rowspan=2 colspan=2> Approach </th>
    <th colspan=8> Entity Extraction </th>
    <th colspan=8> Entity Linking </th>
</tr>
<tr>
    <td>ZH</td>
    <td>JA</td>
    <td>ES</td>
    <td>FR</td>
    <td>IT</td>
    <td>DE</td>
    <td>PT</td>
    <td>Avg.</td>
    <td>ZH</td>
    <td>JA</td>
    <td>ES</td>
    <td>FR</td>
    <td>IT</td>
    <td>DE</td>
    <td>PT</td>
    <td>Avg.</td>
</tr>
</tr>
    <td rowspan=12>Large Scale Pre-trained</td>
    <td rowspan=6><a href="../Approaches/approaches_vie.md/#layoutlxlm">LayoutXLM</a></td>
    <td>base, Language Specific Fine-tuning</td>
    <td>89.24</td>
    <td>79.21</td>
    <td>75.50</td>
    <td>79.02</td>
    <td>80.02</td>
    <td>82.22</td>
    <td>79.03</td>
    <td>82.40</td>
    <td>70.73</td>
    <td>69.63</td>
    <td>68.96</td>
    <td>63.53</td>
    <td>64.15</td>
    <td>65.51</td>
    <td>57.18</td>
    <td>65.67</td>
</tr>
<tr>
    <td>large, Language Specific Fine-tuning</td>
    <td>91.61</td>
    <td>80.33</td>
    <td>78.30</td>
    <td>80.98</td>
    <td>82.75</td>
    <td>83.61</td>
    <td>82.73</td>
    <td>82.90</td>
    <td>78.88</td>
    <td>72.25</td>
    <td>76.66</td>
    <td>71.02</td>
    <td>76.91</td>
    <td>68.43</td>
    <td>67.96</td>
    <td>73.16</td>
</tr>
<tr>
    <td>base, Zero-shot transfer</td>
    <td>60.19</td>
    <td>47.15</td>
    <td>45.65</td>
    <td>57.57</td>
    <td>48.46</td>
    <td>52.52</td>
    <td>53.90</td>
    <td>52.21</td>
    <td>44.94</td>
    <td>44.08</td>
    <td>47.08</td>
    <td>44.16</td>
    <td>40.90</td>
    <td>38.20</td>
    <td>36.85</td>
    <td>42.31</td>
</tr>
<tr>
    <td>large, Zero-shot transfer</td>
    <td>68.96</td>
    <td>51.90</td>
    <td>49.76</td>
    <td>61.35</td>
    <td>55.17</td>
    <td>59.05</td>
    <td>60.77</td>
    <td>58.14</td>
    <td>55.31</td>
    <td>56.96</td>
    <td>57.80</td>
    <td>56.15</td>
    <td>51.84</td>
    <td>48.90</td>
    <td>47.95</td>
    <td>53.56</td>
</tr>
<tr>
    <td>base, Multitask Fine-tuning</td>
    <td>89.73</td>
    <td>79.64</td>
    <td>77.98</td>
    <td>81.73</td>
    <td>82.10</td>
    <td>83.22</td>
    <td>82.41</td>
    <td>82.40</td>
    <td>82.41</td>
    <td>81.42</td>
    <td>81.04</td>
    <td>82.21</td>
    <td>83.10</td>
    <td>78.54</td>
    <td>70.44</td>
    <td>79.88</td>
</tr>
<tr>
    <td>large, Multitask Fine-tuning</td>
    <td>91.55</td>
    <td>82.16</td>
    <td>80.55</td>
    <td>83.84</td>
    <td>83.72</td>
    <td>85.30</td>
    <td>86.50</td>
    <td>84.80</td>
    <td>90.00</td>
    <td>86.21</td>
    <td>85.92</td>
    <td>86.69</td>
    <td>86.75</td>
    <td>82.63</td>
    <td>81.60</td>
    <td>85.69</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#xylayoutlm">XYLayoutLM</a></td>
    <td>91.76</td>
    <td>80.57</td>
    <td>76.87</td>
    <td>79.97</td>
    <td>81.75</td>
    <td>83.35</td>
    <td>80.01</td>
    <td>82.04</td>
    <td>74.45</td>
    <td>70.59</td>
    <td>72.59</td>
    <td>65.21</td>
    <td>65.72</td>
    <td>67.03</td>
    <td>58.98</td>
    <td>67.79</td>
</tr>
</tr>
    <td rowspan=3><a href="../Approaches/approaches_vie.md/#lilt">LiLT</a></td>
    <td>[InfoXLM] base, Language Specific Fine-tuning</td>
    <td>89.38</td>
    <td>79.64</td>
    <td>79.11</td>
    <td>79.53</td>
    <td>83.76</td>
    <td>82.31</td>
    <td>82.20</td>
    <td>82.27</td>
    <td>72.97</td>
    <td>70.37</td>
    <td>71.95</td>
    <td>69.65</td>
    <td>70.43</td>
    <td>65.58</td>
    <td>58.74</td>
    <td>68.53</td>
</tr>
<tr>
    <td>[InfoXLM] base, Zero-shot transfer</td>
    <td>61.52</td>
    <td>51.84</td>
    <td>51.01</td>
    <td>59.23</td>
    <td>53.71</td>
    <td>60.13</td>
    <td>63.25</td>
    <td>57.24</td>
    <td>47.64</td>
    <td>50.81</td>
    <td>49.68</td>
    <td>52.09</td>
    <td>46.97</td>
    <td>41.69</td>
    <td>42.72</td>
    <td>47.37</td>
</tr>
<tr>
    <td>[InfoXLM] base, Multi-task Fine-tuning</td>
    <td>90.47</td>
    <td>80.88</td>
    <td>83.40</td>
    <td>85.77</td>
    <td>87.92</td>
    <td>87.69</td>
    <td>84.93</td>
    <td>85.86</td>
    <td>84.71</td>
    <td>83.45</td>
    <td>83.35</td>
    <td>84.66</td>
    <td>84.58</td>
    <td>78.78</td>
    <td>76.43</td>
    <td>82.28</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#kvpformer">KVPFormer</a></td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>94.27</td>
    <td>94.23</td>
    <td>95.23</td>
    <td>97.19</td>
    <td>94.11</td>
    <td>92.41</td>
    <td>92.19</td>
    <td>94.23</td>
</tr>
</tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#xylayoutlm">HGALayoutLM</a></td>
    <td>94.22</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
</tr>
</tr>
    <td rowspan=2>End-to-End</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#esp">ESP</a></td>
    <td>Language Specific Fine-tuning</td>
    <td>90.30</td>
    <td>81.10</td>
    <td>85.40</td>
    <td>90.50</td>
    <td>88.90</td>
    <td>87.20</td>
    <td>87.50</td>
    <td>87.30</td>
    <td>90.80</td>
    <td>88.30</td>
    <td>85.20</td>
    <td>90.90</td>
    <td>90.00</td>
    <td>85.20</td>
    <td>86.20</td>
    <td>88.10</td>
</tr>
<tr>
    <td>Multitask Fine-tuning</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>89.13</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>-</td>
    <td>92.31</td>
</tr>
</table>

<br>

## EPHOIE

EPHOIE consists of 11 key categories for **Entity Extraction** and takes the **Entity F1** as the evaluation metric. If the predicted string of a key category is consistent with the ground-truth string and not empty, it will be recorded as a TP sample.

<table align="center">
<tr>
    <th > Type </th>
    <th colspan=2> Approach </th>
    <th> Precision </th>
    <th> Recall </th>
    <th> F1 </th>
</tr>
<tr>
    <td rowspan=1>Grid-based</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#matchvie">MathcVIE</a></td>
    <td>-</td>
    <td>-</td>
    <td>96.87</td>
</tr>
<tr>
    <td rowspan=5>Large-Scale Pre-trained</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#structext">StrucTexT</a></td>
    <td>chn&eng-base</td>
    <td>-</td>
    <td>-</td>
    <td>98.84</td>
</tr>
<tr>
    <td>chn&eng-large</td>
    <td>-</td>
    <td>-</td>
    <td>99.30</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#lilt">LiLT</a></td>
    <td>[InfoXLM]base</td>
    <td>96.99</td>
    <td>98.20</td>
    <td>97.59</td>
</tr>
<tr>
    <td>[ZH-RoBERTa]base</td>
    <td>97.62</td>
    <td>98.33</td>
    <td>97.97</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#qgn">QGN</a></td>
    <td>-</td>
    <td>-</td>
    <td>98.49</td>
</tr>
<tr>
    <td rowspan=2>End-to-End</td>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#vies">VIES</a></td>
    <td>ground-truth</td>
    <td>-</td>
    <td>-</td>
    <td>95.23</td>
</tr>
<tr>
    <td>end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>83.81</td>
</tr>
<tr>
    <td rowspan=4>Other Methods</td>
    <td rowspan=4><a href="../Approaches/approaches_vie.md/#tcpn">TCPN</a></td>
    <td>TextLattice</td>
    <td>-</td>
    <td>-</td>
    <td>98.06</td>
</tr>
<tr>
    <td>Copy Mode, end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>84.67</td>
</tr>
<tr>
    <td>Tag Mode, end-to-end</td>
    <td>-</td>
    <td>-</td>
    <td>86.19</td>
</tr>
<tr>
    <td>Tag Mode, ground-truth</td>
    <td>-</td>
    <td>-</td>
    <td>97.59</td>
</tr>
</table>



## DeepForm


<table align="center">
<tr>
    <th > Type </th>
    <th colspan=2> Approach </th>
    <th> QA F1 </th>
</tr>
<tr>
    <td rowspan=1>End-to-end</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#donut🍩">Donut</a></td>
    <td>61.60</td>
</tr>
<tr>
    <td rowspan=6>LLM-based</td>
    <td colspan=2>Qwen-VL</td>
    <td>4.10</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#monkey">Monkey</a></td>
    <td>40.60</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#mplug-docowl">mPLUG-DocOwl</a></td>
    <td>42.60</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#mplug-docowl-15">mPLUG-DocOwl 1.5</a></td>
    <td>DocOwl-1.5</td>
    <td>68.80</td>
</tr>
<tr>
    <td>DocOwl-1.5 chat</td>
    <td>68.80</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#ureader">UReader</a></td>
    <td>49.50</td>
</tr>

</table>




## Kleister Charity

Kleister Charity (KLC) contains 8 kind of key categories. It contains 2788 financial reports with 61643 pages in total. This benchmark is commonly used by LLM-based approaches in a QA-manner.

<table align="center">
<tr>
    <th > Type </th>
    <th colspan=2> Approach </th>
    <th> QA F1 </th>
</tr>
<tr>
    <td rowspan=1>End-to-end</td>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#donut🍩">Donut</a></td>
    <td>30.00</td>
</tr>
<tr>
    <td rowspan=8>LLM-based</td>
    <td colspan=2>Qwen-VL</td>
    <td>15.90</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#monkey">Monkey</a></td>
    <td>32.80</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#mplug-docowl">mPLUG-DocOwl</a></td>
    <td>30.30</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#mplug-docowl-15">mPLUG-DocOwl 1.5</a></td>
    <td>DocOwl-1.5</td>
    <td>37.90</td>
</tr>
<tr>
    <td>DocOwl-1.5 chat</td>
    <td>38.70</td>
</tr>
<tr>
    <td colspan=2><a href="../Approaches/approaches_vie.md/#ureader">UReader</a></td>
    <td>32.80</td>
</tr>
<tr>
    <td rowspan=2><a href="../Approaches/approaches_vie.md/#doco">DoCo</a></td>
    <td>Qwen-VL-Chat</td>
    <td>33.80</td>
</tr>
<tr>
    <td>mPLUG-Owl</td>
    <td>32.90</td>
</tr>
</table>