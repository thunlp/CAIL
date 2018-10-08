# 	Chinese AI and Law Chanllenge Competition

## 1. Introduction

Intellgient Legal aims at giving machines the ability of judging a case by predicting charges, relevant articles and the term of penalty. These application can help lawyers to judge more sufficiently. In recent years, the improvment of deep learning and natural language processing begins to help the field of law. The combination of AI and law has been noticed by many people.

In order to promote the development of the related technology of legal intelligence, under the guidance of xxx, yyy, together with zzz jointly sponsored 2018 Chinese AI and Law Chanllenge Competition([CAIL2018](http://cail.cipsc.org.cn/)). The competition aims to provide researchers with a platform for academic exchange, promote language understanding and the application of artificial intelligence technology in the legal field, and promote the development of Legal Artificial intelligence. Technical exchanges and awards will be held after the end of each year. Researchers and developers from academia and industry are invited to take part in this challenge.


## 2. Task Specification

### 2.1 Introduction

* Task 1(Charge Preidction): Predicting the charges according to the fact description in the law documents;
* Task 2(Relevant Articles Prediction): Predicting the relevant articles according to the fact description in the law documents;
* Task 3(Term of Penalty Prediction)：Predicting the term of penalty according to the fact description in the law documents.

The contestants can one or more tasks to take part in the competition. Meanwhile, we will provide rewards for every tasks in order to encourage contestants to take part in more tasks.

### 2.2 Data

The data of the competition comes from the law documents of criminal cases published on  [Chinese Judgment Online](http://wenshu.court.gov.cn/). Every document contains the fact description and the details of the cases. Moreover, there are relevant articles, the charges of the defendants, and the term of penalty including in the documents.

The dataset contains `2,680,000 criminal law documents`，covered [202 charges](meta/accu.txt)，[183 articles](meta/law.txt)，and the term of penalty varies from **0 to 25 years, including the life imprisonment and the death penalty**.

There are two parts of our dataset called CAIL2018-Small and CAIL2018-Large. CAIL2018-Small contains about 196,000 documents in total, including abour 150,000 documents for training, 16,000 documents for validating and 30,000 documents for testing. CAIL2018-Large contains 1,500,000 documents for training, and another 900,000 documents for testing. You can download the dataset from the [website](http://cail.cipsc.org.cn).

#### 2.2.1 The Fields of Data
The data are stored in json format and every line in the data contains one document. The details of the fields in the data are listed following:

* **fact**: The description of fact.
* **meta**: The label information which contains:
    * **criminals**: The defendant in the cases.(There will only be one defendant in the case.)
    * **punish\_of\_money**: The punish of money in unit RMB.
    * **accusation**: The defendant's charges.
    * **relevant\_articles**: The relevant articles to the case.
    * **term\_of\_imprisonment**: The term of imprisonment of the defendant.
        There three more fields in this part:
        * **death\_penalty**: Whether the defendant suffer the death penalty.
        * **life\_imprisonment**: Whether the defendant suffer the life imprisonment.
        * **imprisonment**: The length of the term of imprisonment in unit month.

Here is a example of the data:

```

{   
	"fact": "2015年11月5日上午，被告人胡某在平湖市乍浦镇的嘉兴市多凌金牛制衣有限公司车间内，与被害人孙某因工作琐事发生口角，后被告人胡某用木制坐垫打伤被害人孙某左腹部。经平湖公安司法鉴定中心鉴定：孙某的左腹部损伤已达重伤二级。",   
	"meta": 
	{  
		"relevant_articles": [234],  
		"accusation": ["故意伤害"], 
		"criminals": ["胡某"],  
		"term_of_imprisonment": 
		{  
			"death_penalty": false,  
			"imprisonment": 12,  
			"life_imprisonment": false
		}
	}
}
```

### 2.3 Evaluation Methods

We have provided the scoring program for contestants, and you can find the details of the evaluation methods, enviroments and model submmission from [here](https://github.com/thunlp/CAIL2018).

The full score of every task is 100, and here are the details of evaluation methods.

#### 2.3.1 Task 1, 2

Task 1(Charge Prediction) and task 2(Relevant Articles Prediction) use Micro-F1-measure and Macro-F1-measure as the evalution method. The calculation should follow:

![f1](pic/f1.png)

And the final score should be:

![score1](pic/score_1.png)

#### 2.3.2 Task 3

For task 3(The Term of Penalty Prediction), suppose the prediction result is `lp` and the standard answer is `la`, then let

![v](pic/v.png)

```
If v≤0.2，then score=1；
If 0.2<v≤0.4，then score=0.8
……
And so on。
```
**Special case**

If the standard answer is the death penalty or the life imprisonment, the prediction `lp` should equal to `-2` or `-1` otherwise there is no score. The details can be found from [here](https://github.com/thunlp/CAIL2018/blob/a258c1dae88e8fc576529e6dcb012a430da00b95/judger/judger.py#L90).

Finally, the score of task 3 should be:

![score3](pic/score_3.png)

#### 2.3.3 Total score

The total score shoudl be:

![score_all](pic/score_all.png)


### 2.4 Baseline

We have provided a baseline system for all the three tasks([LibSVM](https://github.com/thunlp/CAIL2018/tree/master/baseline)).

## FAQ

### 0. Is there a platform for contestants to communicate with others？

QQ group number: 237633234。
