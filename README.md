# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 2» - Подус Сергей

### Задание 1. Создать Deployment приложений backend и frontend

1. Создать Deployment приложения _frontend_ из образа nginx с количеством реплик 3 шт.
2. Создать Deployment приложения _backend_ из образа multitool. 
3. Добавить Service, которые обеспечат доступ к обоим приложениям внутри кластера. 
4. Продемонстрировать, что приложения видят друг друга с помощью Service.
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

------

### Задание 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера

1. Включить Ingress-controller в MicroK8S.
2. Создать Ingress, обеспечивающий доступ снаружи по IP-адресу кластера MicroK8S так, чтобы при запросе только по адресу открывался _frontend_ а при добавлении /api - _backend_.
3. Продемонстрировать доступ с помощью браузера или `curl` с локального компьютера.
4. Предоставить манифесты и скриншоты или вывод команды п.2.

### Ответ

## Задание 1

1. Все манифесты находятся в папке src:

2. Все манифесты находятся в папке src:

![Scrin 1](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube5/pods1.png)

3. Все манифесты находятся в папке src:

4. 

Тестирование curl backend 

```bash

root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_5/src# kubectl exec -n hm5 frontend-deploy-656dc9758b-4pff9 -- curl service-backend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0WBITT Network MultiTool (with NGINX) - backend-deploy-846c869674-v4mwf - 10.1.38.103 - HTTP: 80 , HTTPS: 443 . (Formerly praqma/network-multitool)
100   147  100   147    0     0   143k      0 --:--:-- --:--:-- --:--:--  143k
```

```bash

root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_5/src# kubectl exec -n hm5 frontend-deploy-656dc9758b-4rz6j -- curl service-backend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   147  100   147    0     0   143k      0 --:--:-- --:--:-- --:--:--  143k
WBITT Network MultiTool (with NGINX) - backend-deploy-846c869674-v4mwf - 10.1.38.103 - HTTP: 80 , HTTPS: 443 . (Formerly praqma/network-multitool)
```

```bash
root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_5/src# kubectl exec -n hm5 frontend-deploy-656dc9758b-q2vq7 -- curl service-backend
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   147  100   147    0     0   143k      0 --:--:-- --:--:-- --:--:--  143k
WBITT Network MultiTool (with NGINX) - backend-deploy-846c869674-v4mwf - 10.1.38.103 - HTTP: 80 , HTTPS: 443 . (Formerly praqma/network-multitool)
```

Тестирование curl frontend

```bash

root@User:/mnt/c/Users/serpo/OneDrive/Документы/DZ_docker/kubik/kub_5/src# kubectl exec -n hm5 backend-deploy-846c869674-v4mwf -- curl frontend-service
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   612  100   612    0     0   462k      0 --:--:-- --:--:-- --:--:--  597k
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

## Задание 2 

1. 

![Scrin 2](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube5/ingress.png)

2. 

![Scrin 3](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube5/ingress-2.png)

3. 

![Scrin 4](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube5/nginx.png)

![Scrin 5](https://github.com/Wanderwille/scrinshot/blob/scrin2/kube5/api.png)