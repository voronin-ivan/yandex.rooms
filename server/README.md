# Приложение для создания и редактирования информации о встречах сотрудников

Написано для Node.js 8 и использует библиотеки:
* express
* sequelize
* graphql

## Команды
Установка зависимостей:
```
npm install
```
Запуск:
```
npm run dev
```

Сброс данных в базе:
```
npm run reset-db
```

Запуск теста:
```
npm test
```

Запуск линтера:
```
npm run lint
```

## Порядок действий
Сперва я склонировал репозиторий, установил все зависимости и попробовал запустить. Ожидаемо, ничего не вышло :)
Код ошибки привел меня к объявлению sequelize, сразу смутило, что дважды передается null (*models/index.js*). Я подумал, что было бы неплохо почитать документацию по sequelize и graphql, поскольку с ними мне сталкиваться не приходилось. После беглого прочтения понял, что убрав эти аргументы из-за ненадобности в нашем случае, приложение должно заработать, что и произошло.
Далее я решил последовательно выполнять все запросы и мутации, чтобы выявить, что не работает:
* Избавился от лишних передаваемых аргументов и параметра offset: 1 для поиска комнат. (*graphql/resolvers/query.js*);
* Добавил в UserInput avatarUrl и сделал обязательным homeFloor (поскольку в User он является таковым) (*graphql/typeDefs.js*);
* Исправил ф-ю createEvent, где промисы себя плохо чувствовали (*graphql/resolvers/mutation.js*);
* Исправил changeEventRoom, там в качестве новой комнаты передавался id самой самого ивента + забыли про return (*graphql/resolvers/mutation.js*);
* Добавил addUserToEvent, про эту мутацию забыли (*graphql/resolvers/mutation.js*);
* Исправил ошибку, которая не позволяла получить rooms и users встреч, заключалась в отсутствии return (*graphql/resolvers/index.js*);
* Исправил роут к GraphQL IDE (/graph**g**l -> /graph**q**l/);
* Избавился от кучи ненужного кода для роута /, все это можно реализовать одним файлом *index.html*;
* Добавил маленький тест;
* Постарался привести к единому code style (теперь проверка линтером выполняется успешно).