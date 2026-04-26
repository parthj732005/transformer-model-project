We have chosen the following datasets (original source):
1. Wikitext-103 : https://www.kaggle.com/datasets/vadimkurochkin/wikitext-103
2. BookCorpus   : https://huggingface.co/datasets/rojagtap/bookcorpus

Wikitext's original size was around 550mb (equivalent to 80M tokens post preprocessing) 
We had sampled various books from BookCorpus(because of compute constraints) and performed data-centric optimisation later based on our initial tests. 

This resulted in 3 dataset: 
1.  Wikitext-103
2.  BookCorpusv1 (BookCorpus + Wikitext-103)
3.  BookCorpusv2 (optimised BookCorpusv1 to BookCorpusv2)

Because of size file constraints, the datasets resulting from preprocessing are saved here: https://drive.google.com/drive/folders/1bpHocRVDFHZRcTcS2eZ4PCFYMoAw_sY2?usp=sharing
