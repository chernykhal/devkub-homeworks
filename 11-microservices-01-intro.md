# Решение домашнего задания к занятию "11.01 Введение в микросервисы"

## Задача 1: Интернет Магазин

Если требования бизнеса растут, в связи с тем, что число клиентов также растет, в таком случае переход к микросервисам целесообразен.
1. Потребители(покупатели) станут получать больше обновлений, так как частота новых релизов возрастет
2. Поддержка продукта станет легче, каждая команда будет отвечать за свою функциональность(каталог, корзина итд)
3. Масштабируемость. Увеличить отказоустойчивость.

Но есть и цена такого перехода:
1. Мониторинг и логирование. Придется уделить много внимания системам управления и мониторинга.
2. Тестирование и деплой. Внесение интеграционных тестов, дополнительно все это несет за собой траты.
3. База данных. В то время как монолит работает с одной базой, микросервисы должны работать с каждой отдельной базой, не допуская возможность работы микросервиса с базой через другой микросервис.
4. Документация. Необходимо актуализировать документацию не только по информации о каждом сервисе, но также и по стилю написания этих сервисов(роуты, названия репозиториев, тесты, работа с авторизацией в каждом сервисе итд)
5. Безопасность. наладить идентификацию, аутентификацию, авторизацию во всех сервисах
 
