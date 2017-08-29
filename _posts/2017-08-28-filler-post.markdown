---
layout: post
title:  "Импорт ми бейби ван мор тайм"
date:   2017-08-28 23:53:43
categories: DS, ML, tutorial
comments: true
---

Снова здрасьте.

Ну мне же надо что-то написать.

Сделаю вид, как будто я вас учу импортировать библиотеки под ML.

(Анализ частотных рядов — как-нибудь в другой раз, уж извините)

Это пусть тут побудет, а вы смотрите и учитесь. Импортирую я как боженька, да-да.
Собственно, это мои импорты с последней построенной модельки для регрессии длины входящего звонка. Как бы моделька не особо большая, так что и импорты довольно скромные. Но не особо шарящих людей уже вполне себе может впечатлить. Такие дела.

{% highlight python %}
import numpy as np
import pandas as pd
from catboost import Pool, CatBoostClassifier, CatBoostRegressor, cv, CatboostIpythonWidget
import hyperopt
from sklearn.model_selection import train_test_split, GridSearchCV, cross_val_score, StratifiedKFold
from sklearn.feature_selection import RFECV
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor, GradientBoostingRegressor

%matplotlib inline
import matplotlib.pyplot as plt
import seaborn as sns
{% endhighlight %}

Ну ладно, ладно. Вот вам ещё немного кода.

Это пересчет суммы звонка от одного и того же абонента за определенный временной промежуток (window).

{% highlight python %}
for i in data['id_abonent'].unique():
    target_rows = data['id_abonent'] == i
    temp_df = data[target_rows]
    temp = pd.DataFrame(temp_df['id_abonent'])
    temp = temp.join(temp_df['call_start'])
    temp['called_lately'] = 1
    temp['called_lately'] = temp.rolling('4h', on='call_start').called_lately.sum()
    data.loc[target_rows, 'called_lately'] = temp['called_lately']
{% endhighlight %}

Ну и хватит с вас.
