

# 2nd-ML100Days

－ 從基礎重新訓練自己，填補不足、穩固基底。

#### [Part I] 資料清理數據前處理 `Day1 to Day16`

* 第十六天為總整理，對於檢查`資料型態`與`尋找遺失值`的方法更為了解。除了練習python語法外，最重要的還是了解資料想解決的問題及相關領域背景，如何用有限的資料發揮最大效益。

* EDA（Exploratory Data Analysis）探索式資料分析與敘述統計做差不多的事，只是換了更炫砲的名字。

  [KDE（Kernel Density Estimation）](http://rightthewaygeek.blogspot.com/2015/09/kernel-density-estimation.html)以無母數方法看樣本密度函數。

  －[核密度估計](<https://blog.csdn.net/unixtch/article/details/78556499>)

  

#### [Part II] 資料科學特徵工程技術 `Day17 to Day30`

完全不會特徵工程，花了更多時間在閱讀相關資料。

寫太多開另一個Markdown：[Note](https://github.com/j0987834204/2nd-ML100Days/blob/master/PartII_note.md)

#### [Part III] 資料科學特徵工程技術 `Day31 to Day`

[Loss Function]([https://medium.com/@chih.sheng.huang821/%E6%A9%9F%E5%99%A8-%E6%B7%B1%E5%BA%A6%E5%AD%B8%E7%BF%92-%E5%9F%BA%E7%A4%8E%E4%BB%8B%E7%B4%B9-%E6%90%8D%E5%A4%B1%E5%87%BD%E6%95%B8-loss-function-2dcac5ebb6cb](https://medium.com/@chih.sheng.huang821/機器-深度學習-基礎介紹-損失函數-loss-function-2dcac5ebb6cb))

[利用學習曲線診斷模型的偏差和方差](<http://bangqu.com/yjB839.html>)

* [評估指標](<https://zhuanlan.zhihu.com/p/30721429>)

  回歸：

  1. MSE（Mean Square Error）
  2. MAE（Mean Absolute Error）
  3. $R^2$（R-square）
  4. MAPE（Mean Absolute Percentage Error）

  分類：

  1. [AUC](<https://www.dataschool.io/roc-curves-and-auc-explained/>)（Area Under Curve）：線越左上越好；機率值

  2. F1-Score（Precision, Recall）：希望某類不要分錯；分類結果

     True Positive, False Positive, True Negative, False Negative

     T / F：模型預測對錯, P / N：模型預測結果

     Precision：模型判定瑕疵，樣本確實為瑕疵的比例

     Recall：模型判定的瑕疵，佔樣本所有瑕疵的比例（以瑕疵檢測為例，若為 recall=1 則代表所有瑕疵都被找到）
     $$
     F_{\beta} = (1+\beta^2)*\frac{precision*recall}{(\beta^2+precision)+recall}
     $$
     

     ![img](https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Precisionrecall.svg/350px-Precisionrecall.svg.png)

  3. 混淆矩陣（Confusion Matrix）
  4. top-k accuracy：用於多分類問題