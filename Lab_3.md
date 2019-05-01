# Big Data Lab 3. Зчитування даних з WEB.
В цій лабораторній роботі необхідно зчитати WEB сторінку з сайту IMDB.com зі
100 фільмами 2017 року виходу за посиланням
«http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature». Необхідно створити data.frame «movies» з наступними даними:
номер фільму (rank_data), назва фільму (title_data), тривалість (runtime_data).
Для виконання лабораторної рекомендується використати бібліотеку «rvest».
CSS селектори для зчитування необхідних даних: rank_data: «.text-primary»,
title_data: «.lister-item-header a», runtime_data: «.text-muted .runtime». Для
зчитування url використовується функція read_html, для зчитування даних по CSS
селектору – html_nodes і для перетворення зчитаних html даних в текст -
html_text. Рекомендується перетворити rank_data та runtime_data з тексту в
числові значення. При формуванні дата фрейму функцією data.frame
рекомендується використати параметр «stringsAsFactors = FALSE».
В результаті виконання лабораторної роботи необхідно відповісти на 

```R
html = read_html("http://www.imdb.com/search/title?count=100&release_date=2017,2017&title_type=feature")
rank_data <- html_text(html_nodes(html,'.text-primary'))
rank_data = as.numeric(rank_data)
title_data <- html_text(html_nodes(html,'.lister-item-header a'))
runtime_data <- html_text(html_nodes(html,'.text-muted .runtime'))
runtime_data = as.numeric(gsub(" min", "", runtime_data))
movies <- data.frame(Rank = rank_data, Title = title_data, Runtime = runtime_data, stringsAsFactors = FALSE)
```
1. Виведіть перші 6 назв фільмів дата фрейму.
    ```R
    head(movies, 6)$Title
    ```
    ```cmd
    [1] "Тор: Рагнарок"                   "Людина-павук: Повернення додому" "Вартовi Галактики 2"            
    [4] "Unicorn Store"                   "1+1: Нова iсторiя"               "Найвеличнiший шоумен"           
    ```
2. Виведіть всі назви фільмів с тривалістю більше 120 хв.
    ```R
    subset(movies, Runtime > 120)$Title
    ```
    
    ```cmd
     [1] "Тор: Рагнарок"                            "Людина-павук: Повернення додому"         
     [3] "Вартовi Галактики 2"                      "1+1: Нова iсторiя"                       
     [5] "Диво-Жiнка"                               "Зорянi вiйни: Епiзод 8 - Останнi Джедаi" 
     [7] "Воно"                                     "Той, хто бiжить по лезу 2049"            
     [9] "Пiрати Карибського моря: Помста Салазара" "Форма води"                              
    [11] "Call Me by Your Name"                     "Джон Уiк 2"                              
    [13] "Чужий: Заповiт"                           "Красуня i Чудовисько"                    
    [15] "Логан: Росомаха"                          "Король Артур: Легенда меча"              
    [17] "Форсаж 8"                                 "Мати!"                                   
    [19] "Трансформери: Останнiй лицар"             "The Shack"                               
    [21] "Kingsman: Золоте кiльце"                  "Гра Моллi"                               
    [23] "Валерiан i мiсто тисячi планет"           "Пострiл в безодню"                       
    [25] "Метелик"                                  "Примарна нитка"                          
    [27] "Вороги"                                   "Brawl in Cell Block 99"                  
    [29] "Вбивство священного оленя"                "Only the Brave"                          
    [31] "Темнi часи"                               "Saban's Могутнi рейнджери"               
    [33] "Сiм сестер"                               "Усi грошi свiту"                         
    [35] "The Glass Castle"                         "Вiйна за планету мавп"                   
    [37] "Дружина доглядача зоопарку"              
    ```
3. Скільки фільмів мають тривалість менше 100 хв.
    ```R
    nrow(movies[movies$Runtime < 100, ])
    ```
    
    ```cmd
    [1] 15
    ```
