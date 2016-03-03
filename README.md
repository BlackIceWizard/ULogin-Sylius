# uLogin for Sylius

Tested up to: 0.15*  
Stable tag: 1.0.1 
License: GPLv2  

**uLogin** — это инструмент, который позволяет пользователям получить единый доступ к различным Интернет-сервисам без необходимости повторной регистрации,
а владельцам сайтов — получить дополнительный приток клиентов из социальных сетей и популярных порталов (Google, Яндекс, Mail.ru, ВКонтакте, Facebook и др.)

Данный fork является адаптацией оригинального плагина ([ulogin-Symfony] (https://github.com/ulogin/ulogin-Symfony)) для работы с Sylius. Причина адаптации - оригинальный банл работает с [FOSUserBundle](https://github.com/FriendsOfSymfony/FOSUserBundle), который был выпилен из последних версий Sylius!  


## Установка

1) Скопировать файлы в /src/

2) Добавить в app/AppKernel.php строку: 
```
new Ulogin\AuthBundle\UloginAuthBundle(),
```
3) Добавить в app/autoload.php строку: 
```
$loader->add('Ulogin', __DIR__.'/../src');
```
4) Добавить в app/config/routing.yml строки:
```
ulogin:
       resource: "@UloginAuthBundle/Resources/config/routing.xml"
```
5) В своем .twig шаблоне добавить вызов:
```
    {{ include('UloginAuthBundle::widget.html.twig', { "uLoginID": "123456", "label": "Войти с помощью:" }) }}
```

где 
`uLoginID` - ID виджета из личного кабинета на сайте http://ulogin.ru
`label` - текст около виджета. Необязательный параметр. Может быть передана пустая строка, тогда надписи не будет.
Удобнее всего этим вызовом заменить отображение социальных иконок Sylius в файле: `src/Sylius/Bundle/WebBundle/Resources/views/Frontend/User/login.html.twig`

6) Выполнить консольную команду:
```
 app/console doctrine:schema:update --force --env=prod
```

это необходимо, чтобы создать сводную таблицу `UloginUser` в базе данных



## Дополнительная информация

Чтобы создать свой виджет для входа на сайт достаточно зайти в Личный Кабинет (ЛК) на сайте http://ulogin.ru/lk.php,
добавить свой сайт к списку "Мои сайты" и на вкладке "Виджеты" добавить новый виджет. Вы можете редактировать свой виджет самостоятельно.
**Важно**: Для успешной работы плагина необходимо включить в обязательных полях профиля поле Еmail в Личном кабинете uLogin.