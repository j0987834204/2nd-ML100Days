

# 2nd-ML100Days

－ 從基礎重新訓練自己，填補不足、穩固基底。

#### [Part I] 資料清理數據前處理 `Day1 to Day16`

* 第十六天為總整理，對於檢查`資料型態`與`尋找遺失值`的方法更為了解。除了練習python語法外，最重要的還是了解資料想解決的問題及相關領域背景，如何用有限的資料發揮最大效益。

* EDA（Exploratory Data Analysis）探索式資料分析與敘述統計做差不多的事，只是換了更炫砲的名字。

  [KDE（Kernel Density Estimation）](http://rightthewaygeek.blogspot.com/2015/09/kernel-density-estimation.html)以無母數方法看樣本密度函數。

  －[核密度估計](<https://blog.csdn.net/unixtch/article/details/78556499>)

  

#### [Part II] 資料科學特徵工程技術 `Day17 to Day30`

完全不會特徵工程，花了更多時間在閱讀相關資料。

##### 數值型

* 處理遺失值

  1. 統計值

     －平均值：數值型，偏態不明顯

     －中位數：數值型，偏態明顯

     －眾數：類別型

  2. 指定值：具有相關`domain knowledge`

  3. 預測值：建模預測所需欄位

     e.g. R's [mice包](<http://rpubs.com/skydome20/R-Note10-Missing_Value>)

* 特徵縮放

  1. 標準化（Standard Scaler）：假定數值為常態分佈，適合本⽅方式平衡特徵
     －不易受離群值影響

  2. 最小最大化（MinMax Scaler）： 假定數值為均勻分佈，適合本⽅方式平衡特徵

     －易受離群值影響

  ※ 樹狀模型不會因為特徵縮放影響結果

* 離群值：若不處理離群值會對特徵所放產生問題

  刪除：只要離群值數量夠少，除去離群值，將可使得模型預測較為準確，但需要了解產生此離群值原因，再決定使否刪除

* 去偏態：當離群資料比例例太高，或者平均值沒有代表性時，可以考慮去除偏態

  1. 自然對數（$ln$）

     可能會有0值出現導致無法使用，故使用`np.log1p`（先+1再取對數）及`np.expm1`（先取指數再-1）

  2. 方根去偏（sqrt）

     將數值減去最小值後開根號，最大值有限時適用

  3. 分布去偏（[box-cox]([https://en.wikipedia.org/wiki/Power_transform#Box%E2%80%93Cox_transformation](https://en.wikipedia.org/wiki/Power_transform#Box–Cox_transformation))）
  
     [資料轉換](<http://www.hmwu.idv.tw/web/R/B01-3-hmwu_R-DataTransformation.pdf>)
  
     ※ 注意 λ 參數要介於 0 到 0.5 之間，並且要注意轉換前的數值不可⼩小於等於0

##### 類別型

* 標籤編碼（Label Encoding）
* 獨熱編碼（One Hot Encoding）

|                          | ⼤⼩有無意義 | 儲存空間/計算時間 | 適⽤模型   |
| ------------------------ | ------------ | ----------------- | ---------- |
| 標籤編碼Label Encoding   | 無           | ⼩                | 樹狀模型   |
| 獨熱編碼One Hot Encoding | 有           | 較⼤              | 非樹狀模型 |

* 均值編碼（Mean Encoding）：`類別特徵`與`目標`明顯相關時可使用

  使用目標值的平均值，取代原本的類別型特徵，但較容易過度配適（overfitting），須利用平滑化修正

* 計數編碼（Counting）

  別的目標均價與類別筆數呈正相關（或負相關），也可以將筆數本身當成特徵

  ※ 自然語言處理時，字詞的計數編碼又稱詞頻，本身就是一個很重要的特徵

* 特徵雜湊 / [特徵哈希](<https://blog.csdn.net/laolu1573/article/details/79410187>)（Feature Hash）

  當相異類別數量量相當大時，其他編碼方式效果更差，可以考慮雜湊編碼以節省時間

  註 : 雜湊編碼效果也不佳，這類問題更更好的解法是嵌入式編碼(Embedding)，但是需要深度學習並有其前提

* 嵌入式編碼（Embedding）

##### 時間型

* 加入第幾周、星期幾

* 週期循環特徵（首尾相接）

  年（春、夏、秋、冬、溫度相關）

  月（薪水、繳費相關）

  周（與周休、消費習慣相關）

  日（日夜、生活作息相關）

  ![1557713731308](C:\Users\lee\AppData\Roaming\Typora\typora-user-images\1557713731308.png)

  [python時間處理](<http://www.wklken.me/posts/2015/03/03/python-base-datetime.html>)、[時間型態](<https://docs.python.org/3/library/datetime.html>)

  

##### [特徵組合](<https://segmentfault.com/a/1190000014799038>)（特徵交叉, Feature Crosses）

數值與數值組合 e.g. 經緯度計算距離(點跟點距離 / 加上地球弧度)

類別與數值組合

常見的有 mean, median, mode, max, min, count 等

* 群聚編碼（Group by Encoding）

  |                         | ⼤⼩有無意義 | 群聚編碼       |
  | ----------------------- | ------------ | -------------- |
  | 平均對象                | 目標值       | 其他數值型特徵 |
  | 過度配適（Overfitting） | 容易         | 不容易         |
  | 對均值平滑（Smoothing） | 需要         | 不需要         |

[Machine Learning Course](<https://developers.google.cn/machine-learning/crash-course/ml-intro>)

##### [特徵選擇](<https://zhuanlan.zhihu.com/p/32749489>)（[Feature Selection](<https://machine-learning-python.kspax.io/intro-1#li-liu-univariate-feature-selection>)）

​	[特徵選擇算法流程、分類、優化與發展綜述](<https://juejin.im/post/5a1f7903f265da431c70144c>)

* 過濾法（Filter）：選定統計數值與設定門檻，刪除低於門檻的特徵

  1. 皮爾森相關係數（Pearson Correlation）

     缺點：對`非線性`特徵狀態，則無法看出關係

  2. 互信息和最大信息係數（MIC, Mutual information and maximal information coefficient）

     互信息公式：
     $$
     \begin{align*}
     MI(x_i,y) &= KL(p(x_i,y) || p(x_i)p(y))\\
     &= \sum_{x_i ∈｛0,1｝}\sum_{y ∈｛0,1｝}p(x_i,y)log\frac{p(x_i,y)}{p(x_i)p(y)}
     \end{align*}
     $$
     `互信息`直接用於特徵選擇不太方便：

     * 它不屬於度量方式，也沒有辦法歸一化，在不同數據及上的結果無法做比較

     * 對於連續變量的計算不是很方便（X 和Y都是集合，$x_i$，y都是離散的取值），通常變量需要先離散化，而互信息的結果對離散化的方式很敏感。

     `最大信息係數`克服了這兩個問題。首先尋找一種最優的離散化方式，然後把互信息取值轉換成一種度量方式，取值區間在 [0,1] 。

     ```python
     from minepy import MINE
     
     m = MINE()
     x = np.random.uniform(-1, 1, 10000)
     m.compute_score(x, x**2)
     print(m.mic())
     ```

  3. 距離相關係數（Distance correlation）

     距離相關係數是為了克服Pearson相關係數的弱點而生。在x和$x^2$這個例子中，即便Pearson相關係數是0，也不能斷定這兩個變量是獨立的（可能是非線性相關）；但如果距離相關係數是0，則這兩個變量是獨立的。

  4. 方差選擇法

     這種方法先要計算各個特徵的方差，然後根據閾值，選擇方差大於閾值的特徵。

     e.g. 假設我們有一個布林值的數據集，並且我們要刪除超過80％的樣本中的一個或零（開或關）的所有特徵。布林值是伯努利隨機變量，這些變量的方差由下式給出：$Var[X]=p(1-p)$

     [VarianceThreshold](<https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.VarianceThreshold.html#sklearn.feature_selection.VarianceThreshold>)是特徵選擇的簡單基線方法。刪除方差不符合某個閾值的所有特徵。默認情況下，它會刪除所有零差異特徵，即所有樣本中具有相同值的特徵。

     ```python
     from sklearn.feature_selection import VarianceThreshold
     X = [[0, 0, 1], [0, 1, 0], [1, 0, 0], [0, 1, 1], [0, 1, 0], [0, 1, 1]]
     sel = VarianceThreshold(threshold=(.8 * (1 - .8)))
     print(sel.fit_transform(X))
     ```

     ```
     array([[0, 1],
            [1, 0],
            [0, 0],
            [1, 1],
            [1, 0],
            [1, 1]]) 
     ```

* 包裝法 （Wrapper）：根據目標函數，逐步加入特徵或刪除特徵

  1. 向前選取法

  2. 向後選取法

  3. 遞歸特徵消除法
     遞歸消除特徵法使用一個模型來進行多輪訓練，每輪訓練後消除若干權值係數的特徵，再用新的特徵集進行下一輪訓練。

     ```python
     from sklearn.feature_selection import RFE
     from sklearn.linear_model import LogisticRegression
     
     #遞歸特徵消除法，返回特徵選擇後的數據
     #参数estimator為模型
     #参数n_features_to_select為選擇特徵個數
     RFE(estimator=LogisticRegression(), n_features_to_select=2).fit_transform(iris.data, iris.target)
     ```

     

* 嵌入法（Embedded）：使用機器學習模型，根據擬合後的係數，刪除係數低於門檻的特徵

  1. L1（[Lasso](<https://cosx.org/2011/12/stories-about-statistical-learning/>)）嵌入

     [Lasso Regression](<https://blog.csdn.net/daunxx/article/details/51596877>)

  2. GDBT（梯度提升樹）嵌入法

     * 特徵重要性

     |                    | Xgboost對應參數<br />（importance_type） | 計算時間 | 估計精確性 | sklearn是否有此功能 |
     | ------------------ | ---------------------------------------- | -------- | ---------- | ------------------- |
     | 分支次數           | weight                                   | 最快     | 最低       | 有                  |
     | 特徵（分支）覆蓋度 | cover                                    | 快       | 中         | 無                  |
     | 損失函數降低量     | gain                                     | 較慢     | 最高       | 無                  |
  
     ※ sklearn當中的樹狀模型，都有特徵重要性這項方法(.feature_importances_)，而實際上都是`分支次數`
  
     * 排列重要性（[permutation Importance](<https://www.kaggle.com/dansbecker/permutation-importance?utm_medium=email&utm_source=mailchimp&utm_campaign=ml4insights>)）
  
       打散單一特徵的資料排序順序，再用原本模型重新預測，觀察打散前後誤差會變化多少
  
     |              | 特徵重要性<br />（Feature Impotance） | 排序重要性<br />（Permutation Importance） |
     | ------------ | ------------------------------------- | ------------------------------------------ |
     | 適用模型     | 限定樹狀模型                          | 機器學習模型均可                           |
     | 計算原理     | 樹狀模型的分歧特徵                    | 打散原始資料中單一特徵的排序               |
     | 額外計算時間 | 較短                                  | 較長                                       |

##### 特徵優化

* [葉編碼](<https://zhuanlan.zhihu.com/p/31734283>)

