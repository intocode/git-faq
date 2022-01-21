# Частые вопросы по Git при работе в команде

### В последний коммит попали ненужные файлы. Как удалить?

Находясь на той же ветке, с которого делал коммит выполни следующую команду

```
git reset --soft HEAD~1
```

Эта команда вернет состояние рабочей директории на момент, который был перед самым последним коммитом.

Набери команду `git status` для просмотра текущего состояния. Все файлы, которые были закомичены в последнем коммите должны находиться в режиме **staged** (будут зеленого цвета).

Убери ненужные файлы из **staged** следующей командой:

```
git restore --staged путь-к-файлу
```

Сделай коммит заново (текст коммита также придется повторить).

Если с текущей ветки ранее был открыт pull request, то исправления нужно выгрузить с флагом `-ff`, например: 

```
git push origin my-branch -f
```

### Как я могу посмотреть весь список своих коммитов?

```
git log --author="твой никнейм"
```

Команда покажет все коммиты автора **на текущей ветке**.

### Мой коммит попал в репозиторий, но в нем ошибка. Как его удалить?

**На практике не рекомендуется удалять коммит, который был выгружен и стал доступен другим участникам разработки. Это создает больше проблем, чем решает. Самое лучшее в данном случае – это выгрузить новый коммит с исправлениями. Данный совет актуален практически всегда.**

Если по какой-то причине коммит все же нужно удалить, то ищи ответ [в этом вопросе на Stackoverflow](https://stackoverflow.com/questions/448919/how-can-i-remove-a-commit-on-github).

### Должен ли я добавлять `package-lock.json` в свой коммит?

#### Случай 1

Если твоя работа была связана с добавлением/удалением/обновлением зависимостей, тогда да. Нужно добавить в коммит файлы `package.json` и `package-lock.json`.

#### Случай 2

Допустим, ты не изменял зависимости, а просто установил их командой `npm install`, но файл `package-lock.json` все равно модифицировался. Такое может произойти, если файл `package-lock.json` из репозитория "запаздывает" от установленных ранее зависимостей.

В таком случае лучше закоммитить `package-lock.json` отдельным коммитом, обновить его в репозитории и уведомить об этом других участников разработки.

### Я сделал Pull Request. В нём не было конфликтов, но спустя время они появились. Почему?

Конфликт появился потому что **после** открытия твоего PR на удаленной ветке произошли изменения. К примеру был принят другой PR, затрагивающий тот же самый файл.
