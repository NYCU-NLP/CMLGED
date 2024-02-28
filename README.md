# Chinese Multi-Label Grammatical Error Detection
**C**hinese **M**ulti-**L**abel **G**rammatical **E**rror **D**etection (CMLGED) Corpus is  collected and annotated by NYCU NLP Lab (httpa://ainlp.tw/).<br><br>
The benchmark data came from the TOCFL learner corpus (Lee et al., 2018), including grammatical error annotation of 2,837 essays written by Chinese language learners originating from 46 different mother-tongue languages.We divided the paragraph into individual sentences splitting by the newline symbol and punctuations which include an exclamation, question, or sentence period.<br>

In the dataset, the sentences contained at least one of four error labels: Missing words (denoted as M), Redundant words (R), incorrect word Selection (S), and Word ordering error (W).Table 1 provided the describe and example for these four types error. Finally, we have 19,546 sentences with a total of 27,189 labels. Each sentence contains average 27.9 characters and 1.39 labels.
About two-third of sentences (13,265/67.8%) were annotated with only one label, followed by two labels (5,024/25.7%), three labels (1,152/5.9%), and four labels (105/0.005%).<br>

<table class="tg">
<thead>
  <tr>
    <th class="tg-lgpt"><span style="font-weight:600">Grammatical Error Type</span></th>
    <th class="tg-lgpt"><span style="font-weight:600">Description/Example</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-16kw" rowspan="2">Missing words (M)</td>
    <td class="tg-m2ts">Missing words means that some words in the sentence was missing.</td>
  </tr>
  <tr>
    <td class="tg-m2ts">他請我教 [M] 日文<br>他請我教他日文<br>(He asked me to teach him Japanese.)</td>
  </tr>
  <tr>
    <td class="tg-16kw" rowspan="2">Redundant words (R)</td>
    <td class="tg-m2ts">Resunant words means that some words in the sentence was redundant.</td>
  </tr>
  <tr>
    <td class="tg-m2ts">我會在第 [R] 一樓等你<br>我會在一樓等你<br>(I will wait for you on the first floor.)</td>
  </tr>
  <tr>
    <td class="tg-m2ts" rowspan="2">incorrect word Selection (S)</td>
    <td class="tg-m2ts">Incorrect word selection means that some words in the sentence were used incorrectly.</td>
  </tr>
  <tr>
    <td class="tg-m2ts">傑克是一個兩 [S] 年級的高中生<br>傑克是一個二年級的高中生<br>(Jack is a second-year senior high school student.)</td>
  </tr>
  <tr>
    <td class="tg-16kw" rowspan="2">Word ordering error (W)</td>
    <td class="tg-m2ts">Word ordering error means that some words in the sentence were used in the wrong order.</td>
  </tr>
  <tr>
    <td class="tg-m2ts">他平常起床七點鐘 [W]<br>他平常七點鐘起床<br>(He usually gets up at seven o’clock.)</td>
  </tr>
</tbody>
</table>
Table 2 shows the statisitcs in the CMLGED. The most common grammatical error type was Incorrect word selection (10,397 cases or 38.24%), and second grammatical error type was Missing words (9,431 cases or 34.69%). These 2 most common error types accounted for 73% of the total 27,189 labels, with the remaining 6 types accounting for 27%.<br>
<br>

| Grammatical Error Type | Number (Ratio%) |
|:-------:|:-----:|
| Missing words | 9431 (34.69%) |
| Resunant words | 5161 (18.98%) |
| Incorrect word selection | 10397 (38.24%) |
| Word ordering error | 2200 (8.09%) |


## Data Format 資料格式
+ `id` : a sentence identifier
+ `sentence` : a sentence of segmented word sequence
+ `M` : Missing words error
+ `R` : Redundant words error
+ `S` : Incorrect words selection error
+ `W`：Word ordering error

## Example 範例
```
id,sentence,M,R,S,W
0003_4, 我 先 恭喜 妳 ， 我 以前 知道 妳 又 很 聰明 又 用功 ， 所以 你 快 一點 找到 了 工作 。,1,1,0,0
1339_12, 老師 ， 張小春 希望 您 喜歡 的 意見 ， 如果 您 有 問題 問 ， 我 能 多 解釋 。,1,1,1,0
```
## Experiment 實驗
Our experimental neural networks can be further divided into three types: 1) Stacked-based: conventional neural network architectures, including traditional BiLSTM (Graves et al., 2013), CNN (Kim, 2014), and fastText (Bojanowski et al., 2017); 2) Graph-based: a class of neural networks used for processing data represented by graph data structures. We used the Graph-CNN (Defferrard et al., 2016), TextGCN (Yao et al., 2019), and HyperGAT (Ding et al., 2020); 3) Transformer-based: a type of pre-trained model that uses the encoder and self-attention mechanism. We compared the BERT (Devlin et al., 2018), RoBERTa (Liu et al., 2019), XLNet (Yang et al., 2019) and ELECTRA (Clark et al., 2020).
We randomly divided the CMLGED into 5 parts. The following experiment used these five data for 5-fold cross-validation to evaluated the performence.<br>
<table class="tg">
<thead>
  <tr>
    <th class="tg-3psh" colspan="2">Neural Network Models</th>
    <th class="tg-3vzc">Micro F1</th>
    <th class="tg-3vzc">Macro F1</th>
    <th class="tg-3vzc">Weighted F1</th>
    <th class="tg-3vzc">Subset Accuracy</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-m2ts" rowspan="3">Stack-based</td>
    <td class="tg-m2ts">BiLSTM</td>
    <td class="tg-cwad">0.4827</td>
    <td class="tg-cwad">0.2993</td>
    <td class="tg-cwad">0.4261</td>
    <td class="tg-cwad">0.2258</td>
  </tr>
  <tr>
    <td class="tg-m2ts">CNN</td>
    <td class="tg-cwad"><b>0.5035</b></td>
    <td class="tg-cwad"><b>0.3021</b></td>
    <td class="tg-cwad"><b>0.4338</b></td>
    <td class="tg-cwad"><b>0.2313</b></td>
  </tr>
  <tr>
    <td class="tg-m2ts">fastText</td>
    <td class="tg-cwad">0.436</td>
    <td class="tg-cwad">0.2355</td>
    <td class="tg-cwad">0.3457</td>
    <td class="tg-cwad">0.1844</td>
  </tr>
  <tr>
    <td class="tg-m2ts" rowspan="3">Graph-based</td>
    <td class="tg-m2ts">Graph-CNN</td>
    <td class="tg-cwad">0.4810</td>
    <td class="tg-cwad"><b>0.3972</b></td>
    <td class="tg-cwad"><b>0.4801</b></td>
    <td class="tg-cwad">0.1260</td>
  </tr>
  <tr>
    <td class="tg-m2ts">TextGCN</td>
    <td class="tg-cwad">0.4242</td>
    <td class="tg-cwad">0.3436</td>
    <td class="tg-cwad">0.4228</td>
    <td class="tg-cwad">0.1767</td>
  </tr>
  <tr>
    <td class="tg-m2ts">HyperGAT</td>
    <td class="tg-cwad"><b>0.5078</b></td>
    <td class="tg-cwad">0.2972</td>
    <td class="tg-cwad">0.4246</td>
    <td class="tg-cwad"><b>0.2461</b></td>
  </tr>
  <tr>
    <td class="tg-m2ts" rowspan="4">Transformer-based</td>
    <td class="tg-m2ts">BERT</td>
    <td class="tg-cwad">0.5698</td>
    <td class="tg-cwad">0.4973</td>
    <td class="tg-cwad">0.5645</td>
    <td class="tg-cwad">0.3374</td>
  </tr>
  <tr>
    <td class="tg-m2ts">RoBERTa</td>
    <td class="tg-cwad">0.5670</td>
    <td class="tg-cwad">0.4954</td>
    <td class="tg-cwad">0.5612</td>
    <td class="tg-cwad">0.3287</td>
  </tr>
  <tr>
    <td class="tg-cwad">XLNet</td>
    <td class="tg-cwad">0.5632</td>
    <td class="tg-cwad">0.4495</td>
    <td class="tg-cwad">0.5278</td>
    <td class="tg-cwad">0.3030</td>
  </tr>
  <tr>
    <td class="tg-cwad">ELECTRA</td>
    <td class="tg-cwad"><b>0.6147</b></td>
    <td class="tg-cwad"><b>0.5059</b></td>
    <td class="tg-cwad"><b>0.5978</b></td>
    <td class="tg-cwad"><b>0.3739</b></td>
  </tr>
</tbody>
</table>

## Citation 引用
Please cite the following papers if you use the CMLGED:

Tzu-Mi Lin, Chao-Yi Chen, Lung-Hao Lee, and Yuen-Hsien Tseng. 2022. Evaluating the performance of Chinese multi-Label grammatical error detection using deep neural networks. *Proceddings of the 30<sup>th</sup> International Conference on Computers in Education. Asia-Pacific Society for Computers in Education*, pages 524-526.

@article{LIN-ICCE-2022,<br>
         author={Tzu-Mi Lin, Chao-Yi Chen, Lung-Hao Lee, and Yuen-Hsien Tseng},<br>
         title={Evaluating the performance of Chinese multi-Label grammatical error detection using deep neural networks},<br>
         year={2022},<br>
         journal={In Proceddings of the 30<sup>th</sup> International Conference on Computers in Education. Asia-Pacific Society for Computers in Education},<br>
         pages={524-526},<br>
}
## Reference 參考資料
Piotr Bojanowski, Edouard Grave, Armand Joulin, and Tomas Mikolov. 2017. Enriching Word Vectors with Subword Information. Transactions of the Association for            Computational Linguistics, 5:135–146.<br>

Michaël Defferrard, Xavier Bresson, Pierre Vandergheynst. 2016. Convolutional Neural Networks on Graphs with Fast Localized Spectral Filtering. In Proceeding of the n  Neural Information Processing Systems. <br>

Jacob Devlin, Ming-Wei Chang, Kenton Lee, and Kristina Toutanova. 2019. BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding. In            Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies, Volume 1.               Association for Computational Linguistics, pages 4171–4186.<br>

Kaize Ding, Jianling Wang, Jundong Li, Dingcheng Li, and Huan Liu. 2020. Be More with Less: Hypergraph Attention Networks for Inductive Text Classification. In          Proceedings of the 2020 Conference on Empirical Methods in Natural Language Processing. Association for Computational Linguistics, pages 4927–4936.<br>

Alex Graves, Abdel-rahman Mohamed, Geoffrey Hinton. 2013. Speech recognition with deep recurrent neural networks. Proceedings of  International Conference on            Acoustics, Speech, and Signal Processing. IEEE Digital Library, pages 6645-6649. <br>

Yoon Kim. 2014. Convolutional Neural Networks for Sentence Classification. In Proceedings of the 2014 Conference on Empirical Methods in Natural Language Processing.    Association for Computational Linguistics, pages 1746–1751.<br>

Lung-Hao Lee, Yuen-Hsien Tseng, and Li-Ping Chang. 2018. Building a TOCFL learner corpus for Chinese grammatical error diagnosis. In Proceedings of the Eleventh       International Conference on Language Resources and Evaluation. European Language Resources Association, pages 2298-2304.<br>

Yinhan Liu, Myle Ott, Naman Goyal, Jingfei Du, Mandar Joshi, Danqi Chen, Omer Levy, Mike Lewis, Luke Zettlemoyer, Veselin Stoyanov. 2019. RoBERTa: A Robustly Optimized  BERT Pretraining Approach. arXiv preprint.<br>
Zhilin Yang, Zihang Dai, Yiming Yang, Jaime Carbonell, Ruslan Salakhutdinov, Quoc V. Le. 2020. XLNet: Generalized Autoregressive Pretraining for Language                Understanding. arXiv preprint.<br>

Liang Yao, Chengsheng Mao, Yuan Luo. 2019. Graph Convolutional Networks for Text Classification. In Proceedings of the Association for the Advancement of Artificial    Intelligence, pages 7370-7377.<br>
