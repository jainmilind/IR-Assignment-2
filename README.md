# CS F469 Assignment 2
## Plagiarism Detector in News Articles using LSH
<b>Locality sensitive hashing (LSH)</b> is a widely popular technique used in approximate nearest neighbor search. LSH uses an approximate search principle to get better performance while maintaining the quality of the results. </br>
We have used a variation of LSH consisting of three major steps: </br>
1. K-Shingling
2. Minhashing
3. Banded LSH function

At its core, the final LSH function allows us to segment and hash the same sample several times. And when we find that a pair of vectors has been hashed to the same value at least once, we tag them as candidate pairs — that is, potential matches.

In LSH we leverage these collisions of similar inputs to get our candidate pairs.

<img src="https://cdn.sanity.io/images/vr8gru94/production/862f88182a796eb16942c47d93ee03ba4cdaee4d-1920x1080.png" width="600" height="300">

The first step of LSH is the creation of the signature matrix. Since incident matrix is too sparse and dimension heavy, we create a compact signature matrix using the minhashing technique. 
</br> </br>
<span style="color:yellow">**get_hash_functions(hsh_cnt, mod)**</span> generates hsh_cnt random hash functions which will be used for minhashing. The generated hash functions are of the form $(ax + b)$ % $mod$
</br> </br>
#### MinHashing Technique : 
The signature matrix is created using the minhash technique where we apply all of the hash functions row-wise and update the minimum hash value in each document which has the current shingle. </br>
The signature matrix is divided into b bands of r row each, for each band we hash its portion of the column in the corresponding bucket, Candidate column pairs are those that hash to the same bucket for at least 1 band. </br> </br>
<img src="https://cdn.sanity.io/images/vr8gru94/production/00a27d5963a54c82b9f751845218b6beb8c09324-1280x720.png" width="600" height="300">

The results are verified by actually checking if those documents actually have similarity >= threshold. The top 3 similar documents, number of candidate pairs along with statistics depicting performance of LSH (True Positive, True Negative, False Positive, False Negative) is returned.

#### Band Analysis of LSH
Consider $s$ is the similarity between two documents. The probability that the two documents do not collide in a band will be $1 - s_{}^{r}$ where $r$ is the number of rows in a band. </br>
Hence the probability that the two documents collide in atleast one band (form a candidate pair) given the similarity $s$ will be $1 - (1 - s_{}^{r})_{}^{b}$ where $r$ is the number of rows in a band and $b$ is the number of bands.
</br> </br>
![1_iVfiM1wApga7bUMAWK5iAw](https://github.com/Ashwin-1709/Locality-Sensitive-Hashing/assets/98446038/a1054da4-106a-44ab-a0d6-eb1af47410d8)

### For running code - 
- Download the news article dataset from [Kaggle](https://www.kaggle.com/datasets/snapcrack/all-the-news?resource=download&select=articles2.csv)
- Extract the dataset zip

- Run `extract.ipynb` code entirely once before running `LSH.ipynb`
- K is set in `extract.ipynb` change according to your convience
- Pickled Files are initially git ignored (so you will have to run `extract.ipynb` at least once)
