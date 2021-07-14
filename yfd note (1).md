# yfd note
## 第一版本
1. 用 sw 一級行業分類，使用產品 (1000) 作為分類標的，對於單一公司的產業分類也是使用我們自己的分類器出來的結果作為行業 使用 25 個交易日的 return 市值加權作為行業打分   
```{python}
{
 'rank ic均值': -0.020438729618279455,
 'rank ic标准差': 0.11477912035872981,
 'rank IC_IR': -0.1780701015515749,
 'rank IC大于0的比率': 0.3984161660294921
}
```
![](https://i.imgur.com/4ov1UAi.png)
 
2. 用 sw 一級行業分類，使用產品 (1000) 作為分類標的，對於單一公司的產業分類用原本的該公司的行業分類 使用 25 個交易日的 return 市值加權作為行業打分   
```{python}

ic_report
{
 'rank ic均值': -0.02243148060490627,
 'rank ic标准差': 0.08854064554027825,
 'rank IC_IR': -0.25334670272651116,
 'rank IC大于0的比率': 0.3653741125068269
}
```
   ![](https://i.imgur.com/LT75H7I.png)
   ![](https://i.imgur.com/1HLhjlB.png)

> 主要問題可能是因為產品分類分得太垃圾了
> 解決方案: 
> 1. 使用主營產品中的****產業****名稱
> 2. 若分類分數低於 threshold 就使用原本的 sw 行業分類

## 用優化後的產品分類做出 benchmark

3. 用 sw 一級行業分類，使用產業 (4000) 作為分類標的，對於單一公司的產業分類用原本的該公司的行業分類 使用 20 個交易日的 return 市值加權作為行業打分 
    1. 全A
    ```{python}
    {
     'rank IC_IR': -0.15074375061404807,
     'rank IC大于0的比率': 0.42956592956592954,
     'rank ic均值': -0.014162961146053256,
     'rank ic标准差': 0.09395388590479574
     }
     
    ```   
    ![](https://i.imgur.com/IUgRO8B.png)
    ![](https://i.imgur.com/NocUHHg.png)
    ![](https://i.imgur.com/XKRLE5S.png)
    ![](https://i.imgur.com/wO0iC5g.png)
    
    2. in hs300 (因為股票數目較少->分成五組)
    ```{python}
    {'rank IC_IR': -0.03922067736169636,
     'rank IC大于0的比率': 0.48402948402948404,
     'rank ic均值': -0.007684928587401563,
     'rank ic标准差': 0.19594074106702722}
    ```
    ![](https://i.imgur.com/Ol8g9yL.png)
    ![](https://i.imgur.com/CXaYqFK.png)
    ![](https://i.imgur.com/PrFpzav.png)

    3. in zz500 
    ```{python}
    {'rank IC_IR': -0.1752692782168093,
     'rank IC大于0的比率': 0.4430794430794431,
     'rank ic均值': -0.02645075280586383,
     'rank ic标准差': 0.1509149411407062}
    ```
    ![](https://i.imgur.com/VYyaAiq.png)
    ![](https://i.imgur.com/RUgPUrO.png)
    ![](https://i.imgur.com/0TwVEXD.png)


> 上面的因子結果顯示 除了多頭一端明顯有上升趨勢，其餘組別呈現一個負向的關係
> 推論該因子中為行業打分的機制可能動量與反轉的特性都存在，但是因為我們進行了更複雜的操作，所以需要提純驗證打分(行業)方式的合理性
> 解決方案: 
> 1. 使用不同時間區間 n 的 (單一公司的過去 n 天 return) 收益作為行業打分的機制 
> 2. 我們在行業層級對該打分方式做一個討論

## 探討行業组合回报作為打分方式
### 使用不同時間區間 n 的 (單一公司的過去 n 天 return) 收益作為行業打分的機制
4. 用 sw 一級行業分類，使用產業 (4000) 作為分類標的，對於單一公司的產業分類用原本的該公司的行業分類 使用 10 個交易日的 return 市值加權作為行業打分 

    1. 全A
    ```
    {'rank IC_IR': -0.24375766729906984,
     'rank IC大于0的比率': 0.4057911908646003,
     'rank ic均值': -0.020545555323223563,
     'rank ic标准差': 0.0842868064454191}
    ```
    ![](https://i.imgur.com/kXqXXaY.png)
    ![](https://i.imgur.com/YL8RNiN.png)
    ![](https://i.imgur.com/VdEYsf8.png)
    ![](https://i.imgur.com/OVaFVqT.png)
    2. zz800
    ```
    {'rank IC_IR': -0.244172746767251,
     'rank IC大于0的比率': 0.39804241435562804,
     'rank ic均值': -0.031201495973258723,
     'rank ic标准差': 0.12778451480091035}`
    ```
    ![](https://i.imgur.com/sxWLdcI.png)
    ![](https://i.imgur.com/e3T9P3X.png)
    ![](https://i.imgur.com/I6E5kY2.png)
5. 用 sw 一級行業分類，使用產業 (4000) 作為分類標的，對於單一公司的產業分類用原本的該公司的行業分類 使用 5 個交易日的 return 市值加權作為行業打分 

    1. 全A
    ```
    {'rank IC_IR': -0.28214969341637636,
     'rank IC大于0的比率': 0.385022385022385,
     'rank ic均值': -0.022954535506159376,
     'rank ic标准差': 0.08135587612453901}
    ```
    ![](https://i.imgur.com/F9aeTOU.png)
    ![](https://i.imgur.com/hdSx6Ea.png)
    ![](https://i.imgur.com/OXtR47r.png)

    2. zz800
    ```
    {'rank IC_IR': -0.244172746767251,
     'rank IC大于0的比率': 0.39804241435562804,
     'rank ic均值': -0.031201495973258723,
     'rank ic标准差': 0.12778451480091035}`
    ```
    ![](https://i.imgur.com/sxWLdcI.png)
    ![](https://i.imgur.com/e3T9P3X.png)
    ![](https://i.imgur.com/I6E5kY2.png)

    









