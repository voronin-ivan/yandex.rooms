# Яндекс.Переговорки
Тестовое задание #3 для ШРИ 2018

### Технологии
- Node.js + express
- GraphQL
- React
- Flux

### Использование

#### Установка

```sh
$ npm install
```

#### Сборка клиентской части

```sh
$ npm run build
```

#### Запуск (development)

```sh
$ npm run dev
```

#### Запуск (production)

```sh
$ npm start
```

### Описание интерфейса
После загрузки приложения мы попадаем на страницу со встречами, которые проходят в текущий день. Чтобы ознакомиться со списком встреч, проходящих в другой день, необходимо выбрать нужную дату с помощью календаря или стрелочек. Ограничения - 1.5 месяца до текущей даты и 1.5 месяца после (что равняется 3м месяцам, как и сказано в ТЗ).

При клике на свободный слот мы попадаем на форму создания встречи, куда автоматически будут подставлены данные о ее времени и выбранной комнате. Однако, это справедливо лишь для тех свободных слотов, где время начала встречи является актульным на данный момент. Недоступен переход на форму создания встречи еще и в том случае, если свободный слот < 15 минут. К примеру: встреча заканчивается в 15:50, а следующая начинается в 16:00. Между ними нельзя создать встречу, поскольку я выбрал минимально допустимую длительность встречи равную 15 минутам.

При клике на уже существующее событие, появляется информационное окно, где можно ознакомиться с данными встречи. Здесь случайным образом показывается участник события и, если встреча еще не прошла, ее можно отредактировать.

Если время конца события совпадает с началом следующего, то добавляется border для их разделения. В макете это не предусмотрено, однако я посчитал, что это будет хорошо с точки зрения UX.

В форме добавления/редактирования заявки кнопка действия (добавить/сохранить) имеет состояние disabled в том случае, если какое-либо из полей не заполнено. При этом кнопка является кликабельной, при клике будут показаны все ошибки, которые необходимо исправить для отправки формы.

Алгоритм подбора комнаты для встречи работает следующим образом: сначала идет провёрка свободных мест на указанное время по всем комнатам, которые подходят нам по количеству участников. Если свободные места в комнатах найдены, то они представляются нам для выбора, при этом отсортированы они по принципу прохождения всеми участниками минимального количества этажей. Если же свободных мест нет, то происходит поиск ближайшего свободного места (здесь уже нет этажной сортировки) и изменение времени встречи на ближайшее доступное. При невозможности найти свободное место для встречи, показывается информационное сообщение об этом и предложение попробовать указать другие параметры.

Некоторый функционал, указанный в тз, урезан из-за нехватки времени на реализацию. Так, например, алгоритм подбора переговорок лишился возможности переносить встречи в другие комнаты, а в форме поле выбора участников сделано не с помощью подсказок к вводимому значения, а обычным селектом.

#### [Видео-демонстрация](https://youtu.be/-isXSJbVUeU)