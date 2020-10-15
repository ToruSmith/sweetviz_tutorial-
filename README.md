# Sweetviz

Sweetviz是一個開放式的Python函式庫，可以利用簡單的code便快速產生

(1) 特徵的EDA(探索性資料分析)和相關統計計算，並能

(2) 比較兩個不同資料集的特徵樣態，或

(3) 比較兩個子資料集的特徵樣態

## 如何開始

### 在本機端上開啟cmd

```sh
git clone http://10.95.42.31:8282/i9h00233/sweetviz_tutorial.git
```

```sh
pip install sweetviz
```

### 安裝完成後

最重要的步驟:

要準備一個DataFrame

在此使用範例為Titanic資料集

### 開始準備做報表

```sh
import sweetviz as sv
```

可以參考Demo.ipynb

#### 1. 基本報表

```sh

report_train = sv.analyze([train, 'train'])
report_train.show_html(filepath='Basic_train_report.html')

```

檔案:  Basic_train_report.html

### 2. 加入目標變數的報表

加入目標變數前，可以先給予資料一個正確的格式，否則其會自動判定特徵的屬性

```sh
# 給予特徵想要或正確的規格
feature_config = sv.FeatureConfig(skip='Name',  # 要忽略哪個特徵
                                  force_cat=['Pclass', 'Sex', 'SibSp', 'Parch', 'Ticket', 'Cabin'], # Categorical特徵
                                  force_num=['Age', 'Fare'], # Numerical特徵
                                  force_text=None) # Text特徵
```

```sh
report_train_with_target = sv.analyze([train, 'train'],
                                     target_feat='Survived', # 加入特徵變數
                                     feat_cfg=feature_config)
                                     
report_train_with_target.show_html(filepath='Basic_train_report_with_target.html')
```

檔案:  Basic_train_report_with_target.html


### 3. 比較train和test的報表

比較在train和test資料集後，資料集的樣態是否有不同

```sh
compare_report = sv.compare([train, 'Training Data'],
                            [test, 'Test Data'],
                            'Survived',
                            feat_cfg=feature_config)

compare_report.show_html(filepath='Compare_train_test_report.html')
```

檔案:  Compare_train_test_report.html

### 4. 比較Male和Female兩個子資料集的報表

比較在train資料集下，分成Male和Female兩個資料集的樣態是否有不同

缺點是只能分割一個binary的特徵

```sh
compare_subsets_report = sv.compare_intra(train,
                                          train['Sex']=='male', # 給條件區分
                                          ['Male', 'Female'], # 為兩個子資料集命名 
                                          target_feat='Survived',
                                          feat_cfg=feature_config)

compare_subsets_report.show_html(filepath='Compare_male_female_report.html'
```

檔案: Compare_male_female_report.html

## 還想要甚麼功能

可以開Issue給我(佑偉)