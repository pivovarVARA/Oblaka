# Лабораторная работа №4

### Команда  
- Кунгурова Василиса К34201  
- Кормщикова Варвара К34201  

### Задание
Сделать мониторинг сервиса, поднятого в кубере (использовать, например, prometheus и grafana). Показать хотя бы два рабочих графика, которые будут отражать состояние системы
### Ход работы
Поставили Chocolatey для установки helm и затем установили Helm -  пакетный менеджер для Kubernetes:
![minikube](./img/img1.jpg)
Установили Prometheus:
![minikube](./img/img2.jpg)
Откроем Prometheus в браузере:
![minikube](./img/img3.jpg)
Получем следующий результат:
![minikube](./img/img12.jpg)
Устанавливаем grafana:
![minikube](./img/img5.jpg)
При установке нам выпала заметка, что для входа стоит использовать логин admin и пароль, который можно получить, выполнив команду:
```
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
но на Windows base64 не работает, поэтому использовали следующую команду

```
$adminPassword = kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}"
$adminPasswordDecoded = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($adminPassword))
echo $adminPasswordDecoded
```
Получили пароль:

![minikube](./img/img6.jpg)

Теперь выполним команду ```minikube service grafana-np```

![minikube](./img/img7.jpg)
И также откроется интерфейс Grafana:
![minikube](./img/img8.jpg)
Войдем с помощью логина admin  и выданного нам пароля:
![minikube](./img/img9.jpg)
Создаем соединение с prometheus:
![minikube](./img/img10.jpg)
#### Настройка Дашборда
Чтобы создать dashboard, мы перешли на вкладку Dashboards, выбрали создать новый dashboard и далее import. В данном поле можно выбрать готовый шаблон из тех, что представлены на официальном сайте Grafana Labs. Мы выбрали готовый шаблон, указав уникальный ID = 1860.
![minikube](./img/img11.jpg)


### Вывод
Был успешно настроен мониторинг сервиса, запущенного в Kubernetes, с использованием Prometheus и Grafana. Было настроено отображение графиков для отслеживания нагрузки
