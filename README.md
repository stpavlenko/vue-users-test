## Техническое задание

- Создайте таблицу и кнопку, вызывающую модальное окно с формой.
- Сохраняйте данные из формы в таблицу. Данные должны сохраняться в LocalStorage при обновлении страницы.
- Добавьте в форму select с выбором родителя (любого из уже сохранённых пользователей).
- Добавьте в таблицу поддержку вложенных уровней. Глубина вложенности должна быть неограниченной, то есть родителем
  может быть любой существующий пользователь.
- Добавьте сортировку данных в таблице по клику на заголовок колонки; сортировка должна работать по подуровням.

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

https://stpavlenko-vue-users-test.netlify.app/
