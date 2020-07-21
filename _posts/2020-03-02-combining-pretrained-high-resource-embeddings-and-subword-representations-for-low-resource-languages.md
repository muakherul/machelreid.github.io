---
layout: single 
author: Machel Reid
toc: true
toc_sticky: true
---
In our paper *"Combining Pretrained High Resource Embeddings And Subword Representations For Low Resource Languages"* (Accepted to the ICLR 2020 AfricaNLP Workshop) 
[[paper](https://arxiv.org/abs/2003.04419)], we explore methods learning word representations for low resource languages, in particular, *Xhosa*. 

In particular we look at different combinations of pretrained vectors in high-resource langauges (such as GloVe for English) and subword representations using FASTTEXT. 

$$E_M = \texttt{FASTTEXT}(\mathbb{V}),\ E_V = \texttt{GloVe}(\mathbb{V})$$

### **APPROACH**

Our approach assumes the existence of a vocabulary in our low-resource language $$\mathbb{V} = \{v_1,\dots,v_T\}$$, the corresponding translations of the words in $$\mathbb{V}$$ in a high-resource language, referred to as $$\mathbb{D} = \{d_1,\dots,d_T\}$$, and a pretrained embedding matrix for the high resource language $$E_{HR}$$. $$\mathbb{D}$$ can either be comprised by individual words, in the case the word in the low-resource language can be accurately mapped to a single word in the high-resource language (e.g. indoda → man); or by a sequence of words in the case that the word in the low-resource language maps to more than one word in the high-resource language (e.g. bethuna → [listen, everyone]). Concretely, our objective is to use both V and D to produce vector representations for each word in $$\mathbb{V}$$.

To leverage the high-resource language, we embed the atomic elements of $$\mathbb{D}$$ in $$E_{HR}$$ and map the resulting vectors to the corresponding word in $$\mathbb{V}$$. In the case of $$d_i$$ being a sequence, we take a similar approach to [Lazaridou et al. (2017)](https://onlinelibrary.wiley.com/doi/full/10.1111/cogs.12481) and sum the normalized word vectors for each word in $$d_i$$ to produce a word representation for the word $$v_i$$. We refer to the resulting embedding matrix as $$E_V$$. Additionally, we pretrain another embedding matrix $$E_M$$ on a corpus in our low resource language using subword information to capture similarity correlated with the morphological nature of words ([Bojanowski et al., 2016](https://arxiv.org/abs/1607.04606)). We experiment with the following 4 methods to initialize the word embeddings for our downstream task (the vocabulary for our downstream task might differ from $$\mathbb{V}$$):
* ***Xh*Pre** - Initialization with $$E_V$$ . Words not present in $$E_V$$ are initialized with $$E_M$$ .
* ***Xh*Sub** - Initialization with $$E_M$$ only.
* **VecMap** - We learn cross-lingual word embedding mappings by taking two sets of monolingual word embeddings, $$E_V$$ and $$E_M$$ , and mapping them to a common space following
Artetxe et al. (2018).
* ***Xh*Meta** - We compute meta-embeddings for every word $$w_i$$ by taking the mean of $$E_V(w_i)$$
and $$E_M(w_i)$$, following [Coates & Bollegala (2018)](https://arxiv.org/abs/1804.05262). Words not present in $$E_V$$ are associated with an UNK token and its corresponding vector.

### **RESULTS**
#### **Bible**

| Embedding Configuration | BLEU | BEER |
|-------|--------|---------|
| Random Initialization |21.79|21.84|
| VecMap|22.46  | 22.03 |
| *Xh*Sub  | 24.65 |22.79  |
| *Xh*Pre | 27.67 |22.40  |
|*Xh*Meta|**29.09**|**23.33**|

#### **XhOxExamples**

| Embedding Configuration  | BLEU-4 | BEER |
|-------|--------|---------|
| Random Initialization |16.08|25.30|
| VecMap| 16.38 | 25.42 |
| *Xh*Sub  | 17.37 | 26.04  |
| *Xh*Pre | 17.06 | 25.70 |
|*Xh*Meta|**17.77**|**26.44**|

As is evident from the results, the *Xh*Meta approach performed the highest in all tasks, signifying the necessity for both embedding spaces for more "meaningful" word embeddings for this task.

For more details, like dataset statistics, please refer to the *[paper](https://arxiv.org/abs/2003.04419)*.

### **CITATION**
```bibtex
@misc{reid2020combining,
    title={Combining Pretrained High-Resource Embeddings and Subword Representations for Low-Resource Languages},
    author={Machel Reid and Edison Marrese-Taylor and Yutaka Matsuo},
    year={2020},
    eprint={2003.04419},
    archivePrefix={arXiv},
    primaryClass={cs.CL}
}
```
For the *XhOxExamples* data, feel free to download it here: [XhOxExamples.zip](/resources/XhOxExamples.zip)
