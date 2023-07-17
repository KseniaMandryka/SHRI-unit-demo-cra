# Infrastructure

@ksn_mn

```
# склонируйте репозиторий
git clone git@github.com:KseniaMandryka/SHRI-unit-demo-cra.git

# установите зависимости
npm ci

# создайте ветку
git checkout -b *branch name*

# создайте новый файл/внесите изменение в текущие файлы в src
```

Автоматизация настроена через GitHub Actions.

1. Настроен линтер commitlint для соответствия сообщений о коммитах формату conventional commits (*.github/workflows/commitlint.yml*).
```
git add .
git commit -m *conventional commits styles*
git push origin *branch name*
```
При сообщении коммита соответствующем conventional commits styles, в Actions вы увидете успешный вызов workflow Commitlint.

2. Настроен автоматический запуск проверок в CI для пулл реквестов, запускаются автотесты и линтер для кода (*.github/workflows/ci-pr.yml*).
Проверка запускается автоматом на каждый коммит в PR. Результат виден на странице PR. Ограничение на мерж изменений настроены.
```
git add .
git commit -m *conventional commits styles*
git push origin *branch name*
```
При сообщении коммита соответствующем conventional commits styles, в Actions вы увидете успешный вызов workflow CI.

3. Настроен релизный процесс. Релиз запускается автоматически при появлении в git нового релизного тега v<число> (*.github/workflows/commitlint.yml*). Формируется changelog, создается issue с пометкой RELEASE, которые обновляются при вызове с тем же тегом. Перед релизом для проверки коммита запускается Commitlint, во время релиза запускаются автотесты CI. Добавляется ссылка на результаты автотестов.
При успешно пройденных проверках, приложение деплоится на gh-pages.
В репозитории добавлено два тега для примера v1, v2, а также два ишью Release v1, Release v2.
```
git tag *release tag*
git push origin *branch name* --tag *release tag*
```
В Actions вы увидете успешный вызов workflow Commitlint и Release. Новый ишью создан, приложение задеплоено.

4. Секреты хранятся защищенно.


## About app
В этом репозитории находится пример приложения с тестами:

- [e2e тесты](e2e/example.spec.ts)
- [unit тесты](src/example.test.tsx)

Для запуска примеров необходимо установить [NodeJS](https://nodejs.org/en/download/) 16 или выше.

Как запустить:

```sh
# установить зависимости
npm ci

# запустить приложение
npm start
```

Как запустить e2e тесты:

```sh
# скачать браузеры
npx playwright install

# запустить тесты
npm run e2e
```

Как запустить модульные тесты:

```sh
npm test
```
