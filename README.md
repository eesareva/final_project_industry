<h1>Оптимизация производственных расходод для металлургического комбината «Стальная птица»</h1>

Чтобы оптимизировать производственные расходы, металлургический комбинат «Стальная птица» решил уменьшить потребление электроэнергии на этапе обработки стали. Для этого комбинату нужно контролировать температуру сплава. Наша задача — построить модель, которая будет её предсказывать. 

Заказчик хочет использовать разработанную модель для имитации технологического процесса.

<h2>Цель исследования</h2>

Уменьшение потребления электроэнергии на этапе обработки стали. 

---

<h2>Задачи исследования</h2>

Построить модель, которая будет предсказывать температуру сплава. 

---

<h2>Инструменты решения задачи</h2>

- pandas 
- matplotlib.pyplot 
- seaborn
- numpy 
- os
- re
- warnings
- phik
- lightgbm
-  sklearn.model_selection.train_test_split
- sklearn.preprocessing.StandardScaler
- sklearn.model_selection.GridSearchCV
- sklearn.pipeline.Pipeline
- sklearn.linear_model.LinearRegression
- sklearn.tree.DecisionTreeRegressor
- catboost import CatBoostRegressor
- sklearn.dummy.DummyRegressor
- lightgbm.LGBMRegressor
- sklearn.ensemble.RandomForestRegressor
- sklearn.inspection.permutation_importance
- sklearn.metrics.mean_absolute_error
  
---

<h2>Описание этапа обработки</h2>

Сталь обрабатывают в металлическом ковше вместимостью около 100 тонн. Чтобы ковш выдерживал высокие температуры, изнутри его облицовывают огнеупорным кирпичом. Расплавленную сталь заливают в ковш и подогревают до нужной температуры графитовыми электродами. Они установлены в крышке ковша.

Из сплава выводится сера (этот процесс — десульфурация), добавлением примесей корректируется химический состав и отбираются пробы. Сталь легируют — изменяют её состав — подавая куски сплава из бункера для сыпучих материалов или проволоку через специальный трайб-аппарат (от англ. tribe — «масса»).

Перед тем как первый раз ввести легирующие добавки, измеряют температуру стали и производят её химический анализ. Потом температуру на несколько минут повышают, добавляют легирующие материалы и продувают сплав инертным газом. Затем его перемешивают и снова проводят измерения. Такой цикл повторяется до достижения целевого химического состава и оптимальной температуры плавки.

Тогда расплавленная сталь отправляется на доводку металла или поступает в машину непрерывной разливки. Оттуда готовый продукт выходит в виде заготовок-слябов (от англ. slab — «плита»).

<h2>Исходные данные</h2>  

Данные состоят из нескольких файлов, полученных из разных источников:

- `data_arc_new.csv` — данные об электродах:
    - key — номер партии;
    - Начало нагрева дугой — время начала нагрева;
    - Конец нагрева дугой — время окончания нагрева;
    - Активная мощность — значение активной мощности;
    - Реактивная мощность — значение реактивной мощности.
- `data_bulk_new.csv` — данные о подаче сыпучих материалов (объём);
    - key — номер партии;
    - Bulk 1 … Bulk 15 — объём подаваемого материала.
- `data_bulk_time_new.csv` — данные о подаче сыпучих материалов (время);
    - key — номер партии;
    - Bulk 1 … Bulk 15 — время подачи материала.
- `data_gas_new.csv` — данные о продувке сплава газом;
    - key — номер партии;
    - Газ 1 — объём подаваемого газа.
- `data_temp_new.csv` — результаты измерения температуры;
    - key — номер партии;
    - Время замера — время замера;
    - Температура — значение температуры.
- `data_wire_new.csv` — данные о проволочных материалах (объём);
    - key — номер партии;
    - Wire 1 … Wire 9 — объём подаваемых проволочных материалов.
- `data_wire_time_new.csv` — данные о проволочных материалах (время).
    - key — номер партии;
    - Wire 1 … Wire 9 — время подачи проволочных материалов.
    
Во всех файлах столбец key содержит номер партии. В файлах может быть несколько строк с одинаковым значением key: они соответствуют разным итерациям обработки.

----

<h2>План работы</h2>

***1. Загрузка данных***

Загрузка данных и их первичный осмотр.

***2. Исследовательский анализ и предобработка данных***

Исследовательский анализ каждого датафрейма и при необходимости предобработка данных. Выводы об имеющихся признаках: понадобятся ли они для обучения моделей.

***3. Объединение данных***

Объединим выбранные признаки в один датафрейм по ключу.

***4. Исследовательский анализ и предобработка данных объединённого датафрейма***

Исследовательский анализ объединённого датафрейма, визуализация распределения признаков и при необходимости  предобработка данных. Корреляционный анализ. 

***5. Подготовка данных***

Подготовка данных для обучения модели. Разделение данных на две выборки, при масштабировании и кодировании учтем особенности данных и моделей.

***6. Обучение моделей машинного обучения***

Обучим как минимум две модели. Хотя бы для одной из них подберем как минимум два гиперпараметра.

***7. Выбор лучшей модели***

Выберем лучшую модель и проверим её качество на тестовой выборке.

***8. Общий вывод и рекомендации заказчику***

Общий вывод о проделанной работе: описание основных этапов работы, полученных результатов и рекомендации для бизнеса.

---

<h2>Вывод по итогам исследования</h2>

- Выполнила предобработку данных и исследовательский анализ.
- Провела корреляционный анализ
- Обучила следующие модели: 'Linear Regression', 'Decision Tree Regressor', 'CatBoost', 'LightGBM', 'RandomForestRegressor'
- Протестировала данные на лучшей модели
- Провела анализ важности признаков
- Предложены рекомендации заказчику для улучшения предсказаний
