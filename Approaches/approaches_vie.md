<h3 align="center"> Deep Learning Approaches for </h3>
<h1 align="center"> Visual Information Extraction </h1>

<h2> Introduction </h2>

With the rapid development of Internet technology and the increasing needs of information exchange, quantities of documents are digitalized, stored and distributed in the form of images. Numerous application scenarios, such as receipt understanding, card recognition, automatic paper scoring and document matching, are concerned on how to obtain key information from document images. The process is called visual information extraction (VIE), which aims at **mining, analyzing, and extracting information contained in visually rich documents**. Take receipt understanding as an example, given an image of a receipt, the VIE algorithms will tell information such as store name, product details, price, etc.

Different from the information extraction in traditional natural language processing, results of VIE is not only determined by texts, but also closely related to the doucment layout, font style, block color, figures, charts and other components. The analysis and processing of visually rich documents is a challenging task.

Recently proposed deep-learning-based VIE methods can be roughly categorized into six types, namely the **grid-based methods**, the **graph-neural-network-based (GNN-based) methods**, the **Large Scale Pre-trained Models**, the **end-to-end methods**, the **few-shot methods**, **GPT-based methods**,and **other methods**. 

- `Grid-based Methods` take the document image as a two-dimensional matrix, pixels inside the text bounding box are filled with text embeddings, forming the grid representation for deep processing. Grid-based methods are often simple and less computationally expensive. However, its representation ability is not strong enough, features of text regions in small size may not be fully exploited. 
- `GNN-based Methods` take the text segments as graph nodes, relations between segment coordinates are encoded for edge representations. Operations like graph convolution are applied for feature extraction. GNN-based schemes achieve a good balance in cost and performance, but some characteristics of GNN itself, such as over-smoothing and gradient vanishing often make it hard to train the model. 
- `Large Scale Pre-trained Models` obtain effective generic models through pre-training with a vast amount of data. These methods tend to have powerful generalizability and can be applied in a wide range of scenarios that can be extended to other document understanding tasks. However, these models are often computationally expensive and require sufficient computing resources, finding a more efficient architecture and pre-training strategy is still a problem to be solved. 
- VIE is not an isolated process, results from text detection and recognition (optical character recognition, OCR) are needed as prerequisites. Problems in OCR results, such as coordinate mismatches and text recognition errors will affect the subsequent steps. Researchers tried to build `end-to-end paradigms`, which reduce the OCR error accumulation to some extent. But compared with state-of-the-art methods, there is still some way to go. 
- `Few-shot methods` propose some efficient structures to enhance the generalization ability of models and try to fully explore intrinsic features with only a small number of samples. Although some progress has been made, the overall model accuracy still has a lot of room for improvement from the actual application.
- Recently, the GPT series models (ChagGPT, GPT-4) have developed rapidly, and have achieved amazing results in many NLP tasks. `GPT-based methods` take advantage of the powerful capabilities of the GPT models to handle VIE by designing appropriate prompt inputs. These schemes provide a new solution to the field of Document Understanding.

---

<h2> 🗒️List of Index </h2>

- [Grid-based Methods](#grid-based-methods)
  - [Chargrid](#chargrid)
  - [BERTgrid](#bertgrid)
  - [ViBERTgrid](#vibertgrid)
  - [VisualWordgrid](#visualwordgrid)
- [GNN-based Methods](#gnn-based-methods)
  - [Liu GNN](#liu-gnn)
  - [PICK](#pick)
  - [MatchVIE](#matchvie)
  - [GraphDoc](#graphdoc)
- [Large Scale Pre-trained Models](#large-scale-pre-trained-models)
  - [LayoutLM](#layoutlm)
  - [LayoutLMv2](#layoutlmv2)
  - [LayoutXLM](#layoutxlm)
  - [LayoutLMv3](#layoutlmv3)
  - [LiLT](#lilt)
  - [StrucTexT](#structext)
  - [XYLayoutLM](#xylayoutlm)
  - [SelfDoc](#selfdoc)
  - [DocFormer](#docformer)
  - [TILT](#tilt)
  - [UDoc](#udoc)
  - [DocReL](#docrel)
  - [StructuralLM](#structurallm)
  - [BROS](#bros)
  - [Wei Robust Layout-aware IE](#wei-robust-layout-aware-ie)
- [End-to-End Methods](#end-to-end-methods)
  - [EATEN](#eaten)
  - [TRIE](#trie)
  - [VIES](#vies)
  - [Donut🍩](#donut)
  - [StrucTexTv2](#structextv2)
  - [ESP](#esp)
- [Few-shot Methods](#few-shot-methods)
- [GPT-based Methods](#gpt-based-methods)
  - [ICL-D3IE](#icl-d3ie)
- [Other Methods](#other-methods)
  - [TCPN](#tcpn)
  - [SPADE♠](#spade)

---
---

<br>

# Grid-based Methods

## Chargrid 

*Katti et al. Chargrid: Towards Understanding 2D Documents. EMNLP, 2018.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2018-orange"></img>
  <a href="https://aclanthology.org/D18-1476/">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-ACL-brightgreen"></img>
  </a> 
  <a href="https://github.com/antoinedelplace/Chargrid">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Unofficial 1-blue"></img>
  </a>
  <a href="https://github.com/sciencefictionlab/chargrid-pytorch">
    <img alt="Code 2" src="https://img.shields.io/badge/Code-Unofficial 2-blue"></img>
  </a>
  <a href="https://github.com/thanhhau097/chargrid2d">
    <img alt="Code 3" src="https://img.shields.io/badge/Code-Unofficial 3-blue"></img>
  </a>
  <a href="https://github.com/hikopensource/DAVAR-Lab-OCR/tree/main/demo/text_ie/chargrid">
    <img alt="Code 4" src="https://img.shields.io/badge/Code-Unofficial 4-blue"></img> 
  </a>
</p>

- **Highlights**: Seminal Work
- **Modalities**: Semantic; Layout
- **Abstract**: We introduce a novel type of text representation that preserves the 2D layout of a document. This is achieved by encoding each document page as a two-dimensional grid of characters. Based on this representation, we present a generic document understanding pipeline for structured documents. This pipeline makes use of a fully convolutional encoder-decoder network that predicts a segmentation mask and bounding boxes. We demonstrate its capabilities on an information extraction task from invoices and show that it significantly outperforms approaches based on sequential text or document images.

---

##  BERTgrid
*Timo I. Denk and Christian Reisswig. BERTgrid: Contextualized Embedding for 2D Document Representation and Understanding. Document Intelligence Workshop at NeurIPS, 2019.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2019-orange"></img>
  <a href="https://arxiv.org/abs/1909.04948">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
</p>

- **Highlights**: Introduce Large LM to VIE 
- **Modalities**: Semantic; Layout
- **Abstract**: For understanding generic documents, information like font sizes, column layout, and generally the positioning of words may carry semantic information that is crucial for solving a downstream document intelligence task. Our novel BERTgrid, which is based on Chargrid by Katti et al. (2018), represents a document as a grid of contextualized word piece embedding vectors, thereby making its spatial structure and semantics accessible to the processing neural network. The contextualized embedding vectors are retrieved from a BERT language model. We use BERTgrid in combination with a fully convolutional network on a semantic instance segmentation task for extracting fields from invoices. We demonstrate its performance on tabulated line item and document header field extraction.

---

##  ViBERTgrid

*Lin et al. ViBERTgrid: A Jointly Trained Multi-Modal 2D Document Representation for Key Information Extraction from Documents. ICDAR, 2021*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://arxiv.org/abs/2105.11672">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/ZeningLin/ViBERTgrid-PyTorch">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Unofficial-blue"></img>
  </a>
</p>

- **Highlights**: Flexible Modeling Level; Joint Training
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Recent grid-based document representations like BERTgrid allow the simultaneous encoding of the textual and layout information of a document in a 2D feature map so that state-of-the-art image segmentation and/or object detection models can be straightforwardly leveraged to extract key information from documents. However, such methods have not achieved comparable performance to state-of-the-art sequence- and graph-based methods such as LayoutLM and PICK yet. In this paper, we propose a new multi-modal backbone network by concatenating a BERTgrid to an intermediate layer of a CNN model, where the input of CNN is a document image and the BERTgrid is a grid of word embeddings, to generate a more powerful grid-based document representation, named ViBERTgrid. Unlike BERTgrid, the parameters of BERT and CNN in our multimodal backbone network are trained jointly. Our experimental results demonstrate that this joint training strategy improves significantly the representation ability of ViBERTgrid. Consequently, our ViBERTgrid-based key information extraction approach has achieved state-of-the-art performance on real-world datasets.

---

## VisualWordgrid 

*Mohamed Kerroumi, Othmane Sayem and Aymen Shabou. VisualWordGrid: Information Extraction From Scanned Documents Using A Multimodal Approach. ICDAR, 2021*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://arxiv.org/abs/2010.02358">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a> 
</p>

- **Highlights**: Introduce visual modality to grid
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: We introduce a novel approach for scanned document representation to perform field extraction. It allows the simultaneous encoding of the textual, visual and layout information in a 3-axis tensor used as an input to a segmentation model. We improve the recent Chargrid and Wordgrid \cite{chargrid} models in several ways, first by taking into account the visual modality, then by boosting its robustness in regards to small datasets while keeping the inference time low. Our approach is tested on public and private document-image datasets, showing higher performances compared to the recent state-of-the-art methods.

---

<br>
<br>

# GNN-based Methods

##  Liu GNN

*Liu et al. Graph Convolution for Multimodal Information Extraction from Visually Rich Documents. NAACL, 2019*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2019-orange"></img>
  <a href="https://aclanthology.org/N19-2005/">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-ACL-brightgreen"></img>
  </a>
</p>

- **Highlights**: Introduce GCN to VIE
- **Modalities**: Semantic; Layout
- **Abstract**: Visually rich documents (VRDs) are ubiquitous in daily business and life. Examples are purchase receipts, insurance policy documents, custom declaration forms and so on. In VRDs, visual and layout information is critical for document understanding, and texts in such documents cannot be serialized into the one-dimensional sequence without losing information. Classic information extraction models such as BiLSTM-CRF typically operate on text sequences and do not incorporate visual features. In this paper, we introduce a graph convolution based model to combine textual and visual information presented in VRDs. Graph embeddings are trained to summarize the context of a text segment in the document, and further combined with text embeddings for entity extraction. Extensive experiments have been conducted to show that our method outperforms BiLSTM-CRF baselines by significant margins, on two real-world datasets. Additionally, ablation studies are also performed to evaluate the effectiveness of each component of our model.

---

##  PICK

*Yu et al. PICK: Processing Key Information Extraction from Documents using Improved Graph Learning-Convolutional Networks. ICPR, 2020*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2020-orange"></img>
  <a href="https://arxiv.org/abs/2004.07464">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/wenwenyu/PICK-pytorch">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Strong Baseline
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Computer vision with state-of-the-art deep learning models has achieved huge success in the field of Optical Character Recognition (OCR) including text detection and recognition tasks recently. However, Key Information Extraction (KIE) from documents as the downstream task of OCR, having a large number of use scenarios in real-world, remains a challenge because documents not only have textual features extracting from OCR systems but also have semantic visual features that are not fully exploited and play a critical role in KIE. Too little work has been devoted to efficiently make full use of both textual and visual features of the documents. In this paper, we introduce PICK, a framework that is effective and robust in handling complex documents layout for KIE by combining graph learning with graph convolution operation, yielding a richer semantic representation containing the textual and visual features and global layout without ambiguity. Extensive experiments on real-world datasets have been conducted to show that our method outperforms baselines methods by significant margins.

---

##  MatchVIE

*Tang et al. MatchVIE: Exploiting Match Relevancy between Entities for Visual Information Extraction. IJCAI, 2021*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://www.ijcai.org/proceedings/2021/0144">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-IJCAI-brightgreen"></img>
  </a>
</p>

- **Highlights**: Entity Linking
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Visual Information Extraction (VIE) task aims to extract key information from multifarious document images (e.g., invoices and purchase receipts). Most previous methods treat the VIE task simply as a sequence labeling problem or classification problem, which requires models to carefully identify each kind of semantics by introducing multimodal features, such as font, color, layout. But simply introducing multimodal features can't work well when faced with numeric semantic categories or some ambiguous texts. To address this issue, in this paper we propose a novel key-value matching model based on a graph neural network for VIE (MatchVIE). Through key-value matching based on relevancy evaluation, the proposed MatchVIE can bypass the recognitions to various semantics, and simply focuses on the strong relevancy between entities. Besides, we introduce a simple but effective operation, Num2Vec, to tackle the instability of encoded values, which helps model converge more smoothly. Comprehensive experiments demonstrate that the proposed MatchVIE can significantly outperform previous methods. Notably, to the best of our knowledge, MatchVIE may be the first attempt to tackle the VIE task by modeling the relevancy between keys and values and it is a good complement to the existing methods.

---

##  GraphDoc

*Zhang et al. Multimodal Pre-training Based on Graph Attention Network for Document Understanding. arXiv preprint, 2022*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://arxiv.org/abs/2203.13530">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/ZZR8066/GraphDoc">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Low Data Consumption
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Document intelligence as a relatively new research topic supports many business applications. Its main task is to automatically read, understand, and analyze documents. However, due to the diversity of formats (invoices, reports, forms, etc.) and layouts in documents, it is difficult to make machines understand documents. In this paper, we present the GraphDoc, a multimodal graph attention-based model for various document understanding tasks. GraphDoc is pre-trained in a multimodal framework by utilizing text, layout, and image information simultaneously. In a document, a text block relies heavily on its surrounding contexts, accordingly we inject the graph structure into the attention mechanism to form a graph attention layer so that each input node can only attend to its neighborhoods. The input nodes of each graph attention layer are composed of textual, visual, and positional features from semantically meaningful regions in a document image. We do the multimodal feature fusion of each node by the gate fusion layer. The contextualization between each node is modeled by the graph attention layer. GraphDoc learns a generic representation from only 320k unlabeled documents via the Masked Sentence Modeling task. Extensive experimental results on the publicly available datasets show that GraphDoc achieves state-of-the-art performance, which demonstrates the effectiveness of our proposed method.


---

<br>

# Large Scale Pre-trained Models

##  LayoutLM

*Xu et al. LayoutLM: Pre-training of Text and Layout for Document Image Understanding. SIGKDD, 2020*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2020-orange"></img>
  <a href="https://arxiv.org/abs/1912.13318">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/microsoft/unilm/tree/master/layoutlm">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>


- **Highlights**: Seminal Work; Strong Baseline
- **Modalities**: Semantic; Layout; Visual(fine-tuning)
- **Abstract**: Pre-training techniques have been verified successfully in a variety of NLP tasks in recent years. Despite the widespread use of pre-training models for NLP applications, they almost exclusively focus on text-level manipulation, while neglecting layout and style information that is vital for document image understanding. In this paper, we propose the LayoutLM to jointly model interactions between text and layout information across scanned document images, which is beneficial for a great number of real-world document image understanding tasks such as information extraction from scanned documents. Furthermore, we also leverage image features to incorporate words' visual information into LayoutLM. To the best of our knowledge, this is the first time that text and layout are jointly learned in a single framework for document-level pre-training. It achieves new state-of-the-art results in several downstream tasks, including form understanding (from 70.72 to 79.27), receipt understanding (from 94.02 to 95.24) and document image classification (from 93.07 to 94.42).

---

##  LayoutLMv2

*Xu et al. LayoutLMv2: Multi-modal Pre-training for Visually-rich Document Understanding. ACL, 2021*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://aclanthology.org/2021.acl-long.201/">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-ACL-brightgreen"></img>
  </a>
  <a href="https://github.com/microsoft/unilm/tree/master/layoutlmv2">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>


- **Highlights**: Introduce Visual Modality
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Pre-training of text and layout has proved effective in a variety of visually-rich document understanding tasks due to its effective model architecture and the advantage of large-scale unlabeled scanned/digital-born documents. We propose LayoutLMv2 architecture with new pre-training tasks to model the interaction among text, layout, and image in a single multi-modal framework. Specifically, with a two-stream multi-modal Transformer encoder, LayoutLMv2 uses not only the existing masked visual-language modeling task but also the new text-image alignment and text-image matching tasks, which make it better capture the cross-modality interaction in the pre-training stage. Meanwhile, it also integrates a spatial-aware self-attention mechanism into the Transformer architecture so that the model can fully understand the relative positional relationship among different text blocks. Experiment results show that LayoutLMv2 outperforms LayoutLM by a large margin and achieves new state-of-the-art results on a wide variety of downstream visually-rich document understanding tasks, including FUNSD (0.7895 to 0.8420), CORD (0.9493 to 0.9601), SROIE (0.9524 to 0.9781), Kleister-NDA (0.8340 to 0.8520), RVL-CDIP (0.9443 to 0.9564), and DocVQA (0.7295 to 0.8672).

---

##  LayoutXLM

*Xu et al. LayoutXLM: Multimodal Pre-Training for Multilingual Visually-Rich Document Understanding. arXiv preprint, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://arxiv.org/abs/2104.08836">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/microsoft/unilm/tree/master/layoutxlm">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Multi-language
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Multimodal pre-training with text, layout, and image has achieved SOTA performance for visually-rich document understanding tasks recently, which demonstrates the great potential for joint learning across different modalities. In this paper, we present LayoutXLM, a multimodal pre-trained model for multilingual document understanding, which aims to bridge the language barriers for visually-rich document understanding. To accurately evaluate LayoutXLM, we also introduce a multilingual form understanding benchmark dataset named XFUND, which includes form understanding samples in 7 languages (Chinese, Japanese, Spanish, French, Italian, German, Portuguese), and key-value pairs are manually labeled for each language. Experiment results show that the LayoutXLM model has significantly outperformed the existing SOTA cross-lingual pre-trained models on the XFUND dataset. 

---

##  LayoutLMv3

*Huang et al. LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking. ACMMM, 2022.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://arxiv.org/abs/2204.08387">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/microsoft/unilm/tree/master/layoutlmv3">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>


- **Highlights**: Image Patch Encoding; Excellent Performance
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Self-supervised pre-training techniques have achieved remarkable progress in Document AI. Most multimodal pre-trained models use a masked language modeling objective to learn bidirectional representations on the text modality, but they differ in pre-training objectives for the image modality. This discrepancy adds difficulty to multimodal representation learning. In this paper, we propose LayoutLMv3 to pre-train multimodal Transformers for Document AI with unified text and image masking. Additionally, LayoutLMv3 is pre-trained with a word-patch alignment objective to learn cross-modal alignment by predicting whether the corresponding image patch of a text word is masked. The simple unified architecture and training objectives make LayoutLMv3 a general-purpose pre-trained model for both text-centric and image-centric Document AI tasks. Experimental results show that LayoutLMv3 achieves state-of-the-art performance not only in text-centric tasks, including form understanding, receipt understanding, and document visual question answering, but also in image-centric tasks such as document image classification and document layout analysis.

---

## LiLT

*Jiapeng Wang, Lianwen Jin and Kai Ding. LiLT: A Simple yet Effective Language-Independent Layout Transformer for Structured Document Understanding. ACL, 2022.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://aclanthology.org/2022.acl-long.534/">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-ACL-brightgreen"></img>
  </a>
  <a href="https://github.com/jpWang/LiLT">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Multi-language; Flexible LM backbone
- **Modalities**: Semantic; Layout
- **Abstract**: Structured document understanding has attracted considerable attention and made significant progress recently, owing to its crucial role in intelligent document processing. However, most existing related models can only deal with the document data of specific language(s) (typically English) included in the pre-training collection, which is extremely limited. To address this issue, we propose a simple yet effective Language-independent Layout Transformer (LiLT) for structured document understanding. LiLT can be pre-trained on the structured documents of a single language and then directly fine-tuned on other languages with the corresponding off-the-shelf monolingual/multilingual pre-trained textual models. Experimental results on eight languages have shown that LiLT can achieve competitive or even superior performance on diverse widely-used downstream benchmarks, which enables language-independent benefit from the pre-training of document layout structure.

---

## StrucTexT

*Li et al. StrucTexT: Structured Text Understanding with Multi-Modal Transformers. ACMMM, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://arxiv.org/abs/2108.02923">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/PaddlePaddle/VIMER/tree/main/StrucTexT/v1">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Entity Linking; Multi-language
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Structured text understanding on Visually Rich Documents (VRDs) is a crucial part of Document Intelligence. Due to the complexity of content and layout in VRDs, structured text understanding has been a challenging task. Most existing studies decoupled this problem into two sub-tasks: entity labeling and entity linking, which require an entire understanding of the context of documents at both token and segment levels. However, little work has been concerned with the solutions that efficiently extract the structured data from different levels. This paper proposes a unified framework named StrucTexT, which is flexible and effective for handling both sub-tasks. Specifically, based on the transformer, we introduce a segment-token aligned encoder to deal with the entity labeling and entity linking tasks at different levels of granularity. Moreover, we design a novel pre-training strategy with three self-supervised tasks to learn a richer representation. StrucTexT uses the existing Masked Visual Language Modeling task and the new Sentence Length Prediction and Paired Boxes Direction tasks to incorporate the multi-modal information across text, image, and layout. We evaluate our method for structured text understanding at segment-level and token-level and show it outperforms the state-of-the-art counterparts with significantly superior performance on the FUNSD, SROIE, and EPHOIE datasets.


---

## XYLayoutLM

*Gu et al. XYLayoutLM: Towards Layout-Aware Multimodal Networks for Visually-Rich Document Understanding. CVPR, 2022.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://openaccess.thecvf.com/content/CVPR2022/html/Gu_XYLayoutLM_Towards_Layout-Aware_Multimodal_Networks_for_Visually-Rich_Document_Understanding_CVPR_2022_paper.html">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-CVF-brightgreen"></img>
  </a>
</p>

- **Highlights**: Reading Order Sort; Varial Length Input
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Recently, various multimodal networks for Visually-Rich Document Understanding(VRDU) have been proposed, showing the promotion of transformers by integrating visual and layout information with the text embeddings. However, most existing approaches utilize the position embeddings to incorporate the sequence information, neglecting the noisy improper reading order obtained by OCR tools. In this paper, we propose a robust layout-aware multimodal network named XYLayoutLM to capture and leverage rich layout information from proper reading orders produced by our Augmented XY Cut. Moreover, a Dilated Conditional Position Encoding module is proposed to deal with the input sequence of variable lengths, and it additionally extracts local layout information from both textual and visual modalities while generating position embeddings. Experiment results show that our XYLayoutLM achieves competitive results on document understanding tasks.

---

## SelfDoc

*Li et al. SelfDoc: Self-supervised Document Representation Learning. CVPR, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://openaccess.thecvf.com/content/CVPR2021/html/Li_SelfDoc_Self-Supervised_Document_Representation_Learning_CVPR_2021_paper.html">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-CVF-brightgreen"></img>
  </a>
</p>

- **Highlights**: Cross-modality Encoder
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: We propose SelfDoc, a task-agnostic pre-training framework for document image understanding. Because documents are multimodal and are intended for sequential reading, our framework exploits the positional, textual, and visual information of every semantically meaningful component in a document, and it models the contextualization between each block of content. Unlike existing document pre-training models, our model is coarse-grained instead of treating individual words as input, therefore avoiding an overly fine-grained with excessive contextualization. Beyond that, we introduce cross-modal learning in the model pre-training phase to fully leverage multimodal information from unlabeled documents. For downstream usage, we propose a novel modality-adaptive attention mechanism for multimodal feature fusion by adaptively emphasizing language and vision signals. Our framework benefits from self-supervised pre-training on documents without requiring annotations by a feature masking training strategy. It achieves superior performance on multiple downstream tasks with significantly fewer document images used in the pre-training stage compared to previous works.

---

## DocFormer

*Appalaraju et al. DocFormer: End-to-End Transformer for Document Understanding. ICCV, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://openaccess.thecvf.com/content/ICCV2021/html/Appalaraju_DocFormer_End-to-End_Transformer_for_Document_Understanding_ICCV_2021_paper.html">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-CVF-brightgreen"></img>
  </a>
  <a href="https://github.com/shabie/docformer">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Unofficial-blue"></img>
  </a>
</p>

- **Highlights**: Novel Multi-modal Attention Layer
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: We present DocFormer - a multi-modal transformer based architecture for the task of Visual Document Understanding (VDU). VDU is a challenging problem which aims to understand documents in their varied formats(forms, receipts etc.) and layouts. In addition, DocFormer is pre-trained in an unsupervised fashion using carefully designed tasks which encourage multi-modal interaction. DocFormer uses text, vision and spatial features and combines them using a novel multi-modal self-attention layer. DocFormer also shares learned spatial embeddings across modalities which makes it easy for the model to correlate text to visual tokens and vice versa. DocFormer is evaluated on 4 different datasets each with strong baselines. DocFormer achieves state-of-the-art results on all of them, sometimes beating models 4x its size (in no. of parameters)


---

## TILT

*Powalski et al. Going Full-TILT Boogie on Document Understanding with Text-Image-Layout Transformer. ICDAR, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://arxiv.org/abs/2102.09550">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
</p>

- **Highlights**: Novel Attention Mechanism
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: We address the challenging problem of Natural Language Comprehension beyond plain-text documents by introducing the TILT neural network architecture which simultaneously learns layout information, visual features, and textual semantics. Contrary to previous approaches, we rely on a decoder capable of unifying a variety of problems involving natural language. The layout is represented as an attention bias and complemented with contextualized visual information, while the core of our model is a pretrained encoder-decoder Transformer. Our novel approach achieves state-of-the-art results in extracting information from documents and answering questions which demand layout understanding (DocVQA, CORD, SROIE). At the same time, we simplify the process by employing an end-to-end model.


---

## UDoc

*Gu et al. UniDoc: Unified Pretraining Framework for Document Understanding. NeurIPS, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://proceedings.neurips.cc/paper/2021/hash/0084ae4bc24c0795d1e6a4f58444d39b-Abstract.html">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-NeruIPS-brightgreen"></img>
  </a>
</p>

- **Highlights**: Gated Cross-Attention
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Document intelligence automates the extraction of information from documents and supports many business applications. Recent self-supervised learning methods on large-scale unlabeled document datasets have opened up promising directions towards reducing annotation efforts by training models with self-supervised objectives. However, most of the existing document pretraining methods are still language-dominated. We present UDoc, a new unified pretraining framework for document understanding. UDoc is designed to support most document understanding tasks, extending the Transformer to take multimodal embeddings as input. Each input element is composed of words and visual features from a semantic region of the input document image. An important feature of UDoc is that it learns a generic representation by making use of three self-supervised losses, encouraging the representation to model sentences, learn similarities, and align modalities. Extensive empirical analysis demonstrates that the pretraining procedure learns better joint representations and leads to improvements in downstream tasks.


---

## DocReL

*Li et al. Relational Representation Learning in Visually-Rich Documents. ACMMM, 2022.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://arxiv.org/abs/2205.02411">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
</p>

- **Highlights**: Contrastive Learning; Global/Local Relational Consistency Modeling
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Relational understanding is critical for a number of visually-rich documents (VRDs) understanding tasks. Through multi-modal pre-training, recent studies provide comprehensive contextual representations and exploit them as prior knowledge for downstream tasks. In spite of their impressive results, we observe that the widespread relational hints (e.g., relation of key/value fields on receipts) built upon contextual knowledge are not excavated yet. To mitigate this gap, we propose DocReL, a Document Relational Representation Learning framework. The major challenge of DocReL roots in the variety of relations. From the simplest pairwise relation to the complex global structure, it is infeasible to conduct supervised training due to the definition of relation varies and even conflicts in different tasks. To deal with the unpredictable definition of relations, we propose a novel contrastive learning task named Relational Consistency Modeling (RCM), which harnesses the fact that existing relations should be consistent in differently augmented positive views. RCM provides relational representations which are more compatible to the urgent need of downstream tasks, even without any knowledge about the exact definition of relation. DocReL achieves better performance on a wide variety of VRD relational understanding tasks, including table structure recognition, key information extraction and reading order detection.


---

## StructuralLM

*Li et al. StructuralLM: Structural Pre-training for Form Understanding. ACL, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://aclanthology.org/2021.acl-long.493/">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-ACL-brightgreen"></img>
  </a>
  <a href="https://github.com/alibaba/AliceMind/tree/main/StructuralLM">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Cell-level Modeling
- **Modalities**: Semantic; Layout
- **Abstract**: Large pre-trained language models achieve state-of-the-art results when fine-tuned on downstream NLP tasks. However, they almost exclusively focus on text-only representation, while neglecting cell-level layout information that is important for form image understanding. In this paper, we propose a new pre-training approach, StructuralLM, to jointly leverage cell and layout information from scanned documents. Specifically, we pre-train StructuralLM with two new designs to make the most of the interactions of cell and layout information: 1) each cell as a semantic unit; 2) classification of cell positions. The pre-trained StructuralLM achieves new state-of-the-art results in different types of downstream tasks, including form understanding (from 78.95 to 85.14), document visual question answering (from 72.59 to 83.94) and document image classification (from 94.43 to 96.08).


---

## BROS

*Hong et al. BROS: A Pre-Trained Language Model Focusing on Text and Layout for Better Key Information Extraction from Documents. AAAI, 2022.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://ojs.aaai.org/index.php/AAAI/article/view/21322">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-AAAI-brightgreen"></img>
  </a>
  <a href="https://github.com/clovaai/bros">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Out-of-Order OCR Results Compatible
- **Modalities**: Semantic; Layout
- **Abstract**: Key information extraction (KIE) from document images requires understanding the contextual and spatial semantics of texts in two-dimensional (2D) space. Many recent studies try to solve the task by developing pre-trained language models focusing on combining visual features from document images with texts and their layout. On the other hand, this paper tackles the problem by going back to the basic: effective combination of text and layout. Specifically, we propose a pre-trained language model, named BROS (BERT Relying On Spatiality), that encodes relative positions of texts in 2D space and learns from unlabeled documents with area-masking strategy. With this optimized training scheme for understanding texts in 2D space, BROS shows comparable or better performance compared to previous methods on four KIE benchmarks (FUNSD, SROIE*, CORD, and SciTSR) without relying on visual features. This paper also reveals two real-world challenges in KIE tasks-(1) minimizing the error from incorrect text ordering and (2) efficient learning from fewer downstream examples-and demonstrates the superiority of BROS over previous methods.


---

## Wei Robust Layout-aware IE

*Wei et al. Robust layout-aware IE for visually rich documents with pre-trained language models. SIGIR, 2020.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2020-orange"></img>
  <a href="https://arxiv.org/abs/2005.11017">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
</p>

- **Highlights**: Font-type Encoding
- **Modalities**: Semantic; Layout
- **Abstract**: Many business documents processed in modern NLP and IR pipelines are visually rich: in addition to text, their semantics can also be captured by visual traits such as layout, format, and fonts. We study the problem of information extraction from visually rich documents (VRDs) and present a model that combines the power of large pre-trained language models and graph neural networks to efficiently encode both textual and visual information in business documents. We further introduce new fine-tuning objectives to improve in-domain unsupervised fine-tuning to better utilize large amount of unlabeled in-domain data. We experiment on real world invoice and resume data sets and show that the proposed method outperforms strong text-based RoBERTa baselines by 6.3% absolute F1 on invoices and 4.7% absolute F1 on resumes. When evaluated in a few-shot setting, our method requires up to 30x less annotation data than the baseline to achieve the same level of performance at ~90% F1.



<br>
<br>

# End-to-End Methods

## EATEN

*Guo et al. EATEN: Entity-Aware Attention for Single Shot Visual Text Extraction. ICDAR, 2019.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2019-orange"></img>
  <a href="https://arxiv.org/abs/1909.09380">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/beacandler/EATEN">
    <img alt="Code 1" src="https://img.shields.io/badge/DatasetRelease-Official-yellow"></img>
  </a>
</p>

- **Highlights**: Pure End-to-End
- **Modalities**: Visual
- **Abstract**: Extracting Text of Interest (ToI) from images is a crucial part of many OCR applications, such as entity recognition of cards, invoices, and receipts. Most of the existing works employ complicated engineering pipeline, which contains OCR and structure information extraction, to fulfill this task. This paper proposes an Entity-aware Attention Text Extraction Network called EATEN, which is an end-to-end trainable system to extract the ToIs without any post-processing. In the proposed framework, each entity is parsed by its corresponding entity-aware decoder, respectively. Moreover, we innovatively introduce a state transition mechanism which further improves the robustness of visual ToI extraction. In consideration of the absence of public benchmarks, we construct a dataset of almost 0.6 million images in three real-world scenarios (train ticket, passport and business card), which is publicly available at https://github.com/beacandler/EATEN. To the best of our knowledge, EATEN is the first single shot method to extract entities from images. Extensive experiments on these benchmarks demonstrate the state-of-the-art performance of EATEN.

---

## TRIE

*Zhang et al. TRIE: End-to-End Text Reading and Information Extraction for Document Understanding. ACMMM, 2020.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2020-orange"></img>
  <a href="https://arxiv.org/abs/2005.13118">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/hikopensource/DAVAR-Lab-OCR/tree/main/demo/text_ie/trie">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Seminal Work
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Since real-world ubiquitous documents (e.g., invoices, tickets, resumes and leaflets) contain rich information, automatic document image understanding has become a hot topic. Most existing works decouple the problem into two separate tasks, (1) text reading for detecting and recognizing texts in images and (2) information extraction for analyzing and extracting key elements from previously extracted plain text. However, they mainly focus on improving information extraction task, while neglecting the fact that text reading and information extraction are mutually correlated. In this paper, we propose a unified end-to-end text reading and information extraction network, where the two tasks can reinforce each other. Specifically, the multimodal visual and textual features of text reading are fused for information extraction and in turn, the semantics in information extraction contribute to the optimization of text reading. On three real-world datasets with diverse document images (from fixed layout to variable layout, from structured text to semi-structured text), our proposed method significantly outperforms the state-of-the-art methods in both efficiency and accuracy.

---

## VIES

*Wang et al. Towards Robust Visual Information Extraction in Real World: New Dataset and Novel Solution. AAAI, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://ojs.aaai.org/index.php/AAAI/article/view/16378">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-AAAI-brightgreen"></img>
  </a>
  <a href="https://github.com/HCIILAB/EPHOIE">
    <img alt="Code 1" src="https://img.shields.io/badge/DatasetRelease-Official-yellow"></img>
  </a>
</p>

- **Highlights**: Segment/Char-level Encoding
- **Modalities**: Semantic; Layout; Visual
- **Abstract**: Visual information extraction (VIE) has attracted considerable attention recently owing to its various advanced applications such as document understanding, automatic marking and intelligent education. Most existing works decoupled this problem into several independent sub-tasks of text spotting (text detection and recognition) and information extraction, which completely ignored the high correlation among them during optimization. In this paper, we propose a robust visual information extraction system (VIES) towards real-world scenarios, which is a unified end-to-end trainable framework for simultaneous text detection, recognition and information extraction by taking a single document image as input and outputting the structured information. Specifically, the information extraction branch collects abundant visual and semantic representations from text spotting for multimodal feature fusion and conversely, provides higher-level semantic clues to contribute to the optimization of text spotting. Moreover, regarding the shortage of public benchmarks, we construct a fully-annotated dataset called EPHOIE (this https URL), which is the first Chinese benchmark for both text spotting and visual information extraction. EPHOIE consists of 1,494 images of examination paper head with complex layouts and background, including a total of 15,771 Chinese handwritten or printed text instances. Compared with the state-of-the-art methods, our VIES shows significant superior performance on the EPHOIE dataset and achieves a 9.01% F-score gain on the widely used SROIE dataset under the end-to-end scenario.

---

## Donut🍩

*Kim et al. OCR-free Document Understanding Transformer. ECCV, 2022.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2022-orange"></img>
  <a href="https://arxiv.org/abs/2111.15664">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/clovaai/donut">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Pure End-to-End; Structured IE
- **Modalities**: Visual
- **Abstract**: Understanding document images (e.g., invoices) is a core but challenging task since it requires complex functions such as reading text and a holistic understanding of the document. Current Visual Document Understanding (VDU) methods outsource the task of reading text to off-the-shelf Optical Character Recognition (OCR) engines and focus on the understanding task with the OCR outputs. Although such OCR-based approaches have shown promising performance, they suffer from 1) high computational costs for using OCR; 2) inflexibility of OCR models on languages or types of document; 3) OCR error propagation to the subsequent process. To address these issues, in this paper, we introduce a novel OCR-free VDU model named Donut, which stands for Document understanding transformer. As the first step in OCR-free VDU research, we propose a simple architecture (i.e., Transformer) with a pre-training objective (i.e., cross-entropy loss). Donut is conceptually simple yet effective. Through extensive experiments and analyses, we show a simple OCR-free VDU model, Donut, achieves state-of-the-art performances on various VDU tasks in terms of both speed and accuracy. In addition, we offer a synthetic data generator that helps the model pre-training to be flexible in various languages and domains.

---

## StrucTexTv2

*Yu et al. StrucTexTv2: Masked Visual-Textual Perdiction for Document Image Pre-training. ICLR, 2023.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2023-orange"></img>
  <a href="https://arxiv.org/abs/2303.00289">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/PaddlePaddle/VIMER/tree/main/StrucTexT/v2">
    <img alt="DatasetRelease" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Low Inference Memory Consumption
- **Modalities**: Visual
- **Abstract**: In this paper, we present StrucTexTv2, an effective document image pre-training framework, by performing masked visual-textual prediction. It consists of two self-supervised pre-training tasks: masked image modeling and masked language modeling, based on text region-level image masking. The proposed method randomly masks some image regions according to the bounding box coordinates of text words. The objectives of our pre-training tasks are reconstructing the pixels of masked image regions and the corresponding masked tokens simultaneously. Hence the pre-trained encoder can capture more textual semantics in comparison to the masked image modeling that usually predicts the masked image patches. Compared to the masked multi-modal modeling methods for document image understanding that rely on both the image and text modalities, StrucTexTv2 models image-only input and potentially deals with more application scenarios free from OCR pre-processing. Extensive experiments on mainstream benchmarks of document image understanding demonstrate the effectiveness of StrucTexTv2. It achieves competitive or even new state-of-the-art performance in various downstream tasks such as image classification, layout analysis, table structure recognition, document OCR, and information extraction under the end-to-end scenario.

---

## ESP

*Yang et al. Modeling Entities as Semantic Points for Visual Information Extraction in the Wild. CVPR, 2023.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2023-orange"></img>
  <a href="https://arxiv.org/abs/2303.13095">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://www.modelscope.cn/datasets/damo/SIBR/summary">
    <img alt="DatasetRelease" src="https://img.shields.io/badge/Dataset-Official-yellow"></img>
  </a>
</p>

- **Highlights**: Low Inference Memory Consumption; Entity Linking; Multi-line Entity Merging
- **Modalities**: Visual
- **Abstract**: Recently, Visual Information Extraction (VIE) has been becoming increasingly important in both the academia and industry, due to the wide range of real-world applications. Previously, numerous works have been proposed to tackle this problem. However, the benchmarks used to assess these methods are relatively plain, i.e., scenarios with real-world complexity are not fully represented in these benchmarks. As the first contribution of this work, we curate and release a new dataset for VIE, in which the document images are much more challenging in that they are taken from real applications, and difficulties such as blur, partial occlusion, and printing shift are quite common. All these factors may lead to failures in information extraction. Therefore, as the second contribution, we explore an alternative approach to precisely and robustly extract key information from document images under such tough conditions. Specifically, in contrast to previous methods, which usually either incorporate visual information into a multi-modal architecture or train text spotting and information extraction in an end-to-end fashion, we explicitly model entities as semantic points, i.e., center points of entities are enriched with semantic information describing the attributes and relationships of different entities, which could largely benefit entity labeling and linking. Extensive experiments on standard benchmarks in this field as well as the proposed dataset demonstrate that the proposed method can achieve significantly enhanced performance on entity labeling and linking, compared with previous state-of-the-art models.


<br>
<br>

# Few-shot Methods

Under Construction


<br>
<br>

---

# GPT-based Methods

## ICL-D3IE

*He et al. ICL-D3IE: In-Context Learning with Diverse Demonstrations Updating for Document Information Extraction*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2023-orange"></img>
  <a href="https://arxiv.org/abs/2303.05063">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-arXiv-brightgreen"></img>
  </a>
  <a href="https://github.com/MAEHCM/ICL-D3IE">
    <img alt="Code" src="https://img.shields.io/badge/Code-GitHub-blue"></img>
  </a>
</p>

- **Highlights**: Seminal Work
- **Modalities**: Semantic Only
- **Abstract**: Large language models (LLMs), such as GPT-3 and ChatGPT, have demonstrated remarkable results in various natural language processing (NLP) tasks with in-context learning, which involves inference based on a few demonstration examples. Despite their successes in NLP tasks, no investigation has been conducted to assess the ability of LLMs to perform document information extraction (DIE) using in-context learning. Applying LLMs to DIE poses two challenges: the modality and task gap. To this end, we propose a simple but effective in-context learning framework called ICL-D3IE, which enables LLMs to perform DIE with different types of demonstration examples. Specifically, we extract the most difficult and distinct segments from hard training documents as hard demonstrations for benefiting all test instances. We design demonstrations describing relationships that enable LLMs to understand positional relationships. We introduce formatting demonstrations for easy answer extraction. Additionally, the framework improves diverse demonstrations by updating them iteratively. Our experiments on three widely used benchmark datasets demonstrate that the ICL-D3IE framework enables GPT-3/ChatGPT to achieve superior performance when compared to previous pre-trained methods fine-tuned with full training in both the in-distribution (ID) setting and in the out-of-distribution (OOD) setting.


<br>
<br>

---



# Other Methods

## TCPN

*Wang et al. Tag, Copy or Predict: A Unified Weakly-Supervised Learning Framework for Visual Information Extraction using Sequences. IJCAI, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://www.ijcai.org/proceedings/2021/150">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-IJCAI-brightgreen"></img>
  </a>
</p>

- **Highlights**: OCR Error Correction
- **Modalities**: Semantic; Layout
- **Abstract**: Visual information extraction (VIE) has attracted increasing attention in recent years. The existing methods usually first organized optical character recognition (OCR) results in plain texts and then utilized token-level category annotations as supervision to train a sequence tagging model. However, it expends great annotation costs and may be exposed to label confusion, the OCR errors will also significantly affect the final performance. In this paper, we propose a unified weakly-supervised learning framework called TCPNet (Tag, Copy or Predict Network), which introduces 1) an efficient encoder to simultaneously model the semantic and layout information in 2D OCR results, 2) a weakly-supervised training method that utilizes only sequence-level supervision; and 3) a flexible and switchable decoder which contains two inference modes: one (Copy or Predict Mode) is to output key information sequences of different categories by copying a token from the input or predicting one in each time step, and the other (Tag Mode) is to directly tag the input sequence in a single forward pass. Our method shows new state-of-the-art performance on several public benchmarks, which fully proves its effectiveness.

---

## SPADE♠

*Hwang et al. Spatial Dependency Parsing for Semi-Structured Document Information Extraction. ACL Findings, 2021.*

<p>
  <img alt="year" src="https://img.shields.io/badge/Year-2021-orange"></img>
  <a href="https://aclanthology.org/2021.findings-acl.28/">
    <img alt="Paper Link" src="https://img.shields.io/badge/PaperLink-ACL-brightgreen"></img>
  </a>
  <a href="https://github.com/clovaai/spade">
    <img alt="Code 1" src="https://img.shields.io/badge/Code-Official-blue"></img>
  </a>
</p>

- **Highlights**: Structured IE; Entity Linking
- **Modalities**: Semantic; Layout
- **Abstract**: Information Extraction (IE) for semi-structured document images is often approached as a sequence tagging problem by classifying each recognized input token into one of the IOB (Inside, Outside, and Beginning) categories. However, such problem setup has two inherent limitations that (1) it cannot easily handle complex spatial relationships and (2) it is not suitable for highly structured information, which are nevertheless frequently observed in real-world document images. To tackle these issues, we first formulate the IE task as spatial dependency parsing problem that focuses on the relationship among text segment nodes in the documents. Under this setup, we then propose SPADE (SPAtial DEpendency parser) that models highly complex spatial relationships and an arbitrary number of information layers in the documents in an end-to-end manner. We evaluate it on various kinds of documents such as receipts, name cards, forms, and invoices, and show that it achieves a similar or better performance compared to strong baselines including BERT-based IOB taggger, with up to 37.7% improvement.
