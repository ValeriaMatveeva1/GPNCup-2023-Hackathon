# GPNCup 2023 Hackathon

## Условие кейса
Имеется 5 городов, в которых продают каждый из 3-х видов продукта. Необходимо составить расписание цен на 90 дней в каждом из городов на каждый из продуктов таким образом, чтобы совокупная прибыль была максимальной. Помимо этого, есть правила установления цены:
* одна цена на товар должна держаться больше, чем 3 дня (то есть нельзя установить цену на один день, а на следующий день ее сменить);
* запрещается изменение цены больше, чем на 1 за раз (то есть нельзя резко изменить цену с 3 на 4.50, но можно с 3 на 4, а затем через 3 дня поднять до 4.5);
* если цена на 20% выше, чем у конкурентов, налагается большой штраф за установление слишком высокой цены.

Исходные данные (в формате .parquet):
* данные о транзакциях;
* данные о ценах конкурентов;
* данные о погоде;
* данные о себестоимости.

## Описание решения
* EDA и предобработка данных (заполнение пропусков, обработка аномальных значений);
* агрегация данных, объединение и группировка таблиц;
* анализ временных рядов и их компонент, построение прогнозов факторов для дальнейшего прогнозирования продаж (с помощью библиотеки Prophet);
* формирование зависимости спроса и цены;
* формирование экземпляров для каждого города и продукта (с помощью dataclass'ов) для решения оптимизационной задачи с разбиением по городам и продуктам;
* формулировка задачи оптимизации как задачи Longest Path Problem и ее решение с помощью динамического программирования.

С более подробным описанием можно ознакомиться в папке ```docs/GPN Cup 2023.pdf```

## Результаты работы и сравнение
*Сверхзадача*: показать, насколько больше будет прибыль, если менять цену, относительно того, какая бы была прибыль при использовании постоянной цены. В качестве baseline'а было предложено брать последнюю зафиксированную цену в городе на каждый из продуктов.
При использовании динамического ценообразования (по алгоритму LPP DP), совокупная прибыль будет примерно на 185 тысяч больше, чем при выставлении постоянной цены, а в среднем заработок будет больше на 12 тысяч. 

## Структура проекта
```data``` - исходные данные + результат (в файле ```price_schedule_df.parquet```)

```docs``` - оформленный отчет по решению в форматах .docx и .pdf

```notebooks``` - решение в формате .ipynb
