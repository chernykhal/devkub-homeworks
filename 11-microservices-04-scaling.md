
# Решение домашнего задания к занятию "11.04 Микросервисы: масштабирование"

## Задача 1: Кластеризация

Для решения подойдет Kubernetes:
1. Поддержка разных систем контейнеризации;
2. Маршрутизация через kube-proxy и virtual ip. Каждому сервису присваивается доменное имя совпадающее с именем самого сервиса;
3. Возможность горизонтально масштабировать сервисы, увеличивая количество реплик pod'ов;
4. С помощью Kubernetes Horizontal Pod Autoscaler кубер горизонтально масштабирует сервисы, в зависимости от нагрузки и min max количества реплик;
5. Kubernetes позволяет разделить кластер на индивидуальные зоны(namespaces). GlobalNetworkPolic и NetworkPolicy разграничивает доступ внутри кластера, исходящий и входящий трафик. Отвечать за маршрутизацию можно с помощью ingress контроллера.
6. Возможность хранения чувствительных данных с помощью внутреннего объекта secret. Vault для множества функционала по хранению секретов. Env для установки переменных сред.
