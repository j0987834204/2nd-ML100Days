# 模型選擇（Model Selection）

[超參數調整](<https://cambridgecoding.wordpress.com/2016/04/03/scanning-hyperspace-how-to-tune-machine-learning-models/>)

### 決策樹

### 隨機森林

​	Random Forest 的每一棵樹皆是獨立的樹，前一棵樹的結果不會影響下一顆

​	Bagging 是透過抽樣的方式來生成每一棵樹，樹與樹之間是獨立生成的

​	特徵重要性的概念是，觀察某一特徵被⽤來切分的次數而定。假設有兩個一模⼀樣的特徵，在隨機森林中每棵樹皆為獨立，因此兩個特徵皆有可能被使用，最終統計出來的次數會被均分

* [調整參數](<https://towardsdatascience.com/hyperparameter-tuning-the-random-forest-in-python-using-scikit-learn-28d2aa77dd74>)

### 梯度提升機

​	Gradient boosting 因為下一棵樹是為了了修正前一棵樹的錯誤，因此每一棵樹皆有相關聯

​	Boosting 是透過序列的方式來生成每一顆樹，每棵樹都會與前面的樹關聯，因為後面的樹要能夠修正

​	在梯度提升機中，每棵樹皆有關連，因此模型僅會使用其中⼀個特徵，另一個相同特徵的重要性則會消失

* [調整參數](<https://www.analyticsvidhya.com/blog/2016/02/complete-guide-parameter-tuning-gradient-boosting-gbm-python/>)