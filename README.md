# frontend-test-task

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run dev
```

### Compiles and minifies for production
```
npm run build
```

# Тестовое задание Front-End

Здесь находится описание тестового задания на позицию Front-End-разработчика в KazanExpress.\
Если вы нашли его случайно - попробуйте сделать! Авось и вас к себе возьмём. 😉

[RU](README.md) | [EN](README_EN.md)

## Задача

Создать одностраничное TODO-приложение с использованием Vue.js,\
с возможностью ведения/импорта/экспорта проектов.

Приложение может быть имплементировано в одном из уровней сложности:

- [**Easy**](#easy) - на данный момент решения этой сложности не принимаются;
- [**Medium**](#medium) - **Easy** с дополнительными усложнениями, минимально-оцениваемый функционал;
- [**Hard**](#hard) - **Medium** с дополнительными усложнениями;

каждый из которых имеет опциональные задания с более высокой оценкой.

## Подробные требования задачи

Ниже приведены подробные требования к приложению, разделённые по сложности.\
Каждая последующая сложность включает в себя **все** требования предыдущей как обязательные.

- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) `выполнено`
- ![#1589F0](https://via.placeholder.com/15/fbec5d/000000?text=+) `в разработке`
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) `не выполнено`

---

### **Easy**

- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Каждая новая вкладка в бразуере с приложением - отдельный проект со своим списком задач;\
  Система переключения проектов **в пределах одной вкладки считается нарушением** этого требования!
- ![#1589F0](https://via.placeholder.com/15/fbec5d/000000?text=+) Редактируемое название проекта в качестве заголовка страницы;
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Список с задачами:
  - Добавление новой задачи в список;
  - Удаление любой задачи из списка;
  - Возможность пометить любую задачу сделанной и возможность убрать эту пометку (mark as done/not done);
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Вся информация (название проекта, список задач, состояние задач) должна сохраняться при перезагрузке страницы;

Опционально:
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Возможность добавлять подзадачи в любую задачу (с потенциально бесконечной глубиной);
- ![#1589F0](https://via.placeholder.com/15/fbec5d/000000?text=+) Поле ввода для поиска/фильтрации задач в списке (фильтр должен сохраняться после перезагрузки страницы);
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Возможность редактирования названия задачи после её создания;

---

### **Medium**

Все требования [**easy**](#easy), включая опциональные.
А также:

- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=-) Возможность перемещать любые задачи (со всем списком подзадач) из любого открытого проекта в любой другой открытый проект;
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Нельзя использовать `LocalStorage`, `Cookies`, `IndexedDB` и `WebSQL` хранилища;\
  Если ваше приложение пишет *хоть что-нибудь* в одно из этих хранилищ - **требование считается невыполненным**!\
  Это касается и библиотек, которые используют эти типы хранилищ: например - `vuex-multi-tab-state`.
- ![#1589F0](https://via.placeholder.com/15/fbec5d/000000?text=+) Экспорт проекта в файл / импорт проекта из файла;
  - Имя сохраняемого файла должно соответствовать названию проекта.
- ![#1589F0](https://via.placeholder.com/15/fbec5d/000000?text=+) Drag-n-drop для перемещения задач в списке;
- ![#1589F0](https://via.placeholder.com/15/fbec5d/000000?text=+) Сохранение текущего фильтра для возможности его быстрого применения потом;
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Итоговое приложение должно весить не более **200 KB** (сумма всех загружаемых файлов, исключая картинки);

Опционально:
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Наличие CSS-анимаций для drag-n-drop и фильтрации задач;
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Использовать TypeScript для 100% кодовой базы (исключая вёрстку и стили);
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Использовать [Vue Composition API](https://vue-composition-api-rfc.netlify.com/) или [vue@next](https://www.npmjs.com/package/vue/v/next);
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Использовать ESLint/TSLint для контроля качества кода (приветствуется использование настройки [KazanExpress/TSLint](https://github.com/KazanExpress/tslint));
- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Использовать сборщик/бандлер (например, [webpack](https://webpack.js.org/)) для сборки приложения в SPA;

---

### **Hard**

Все требования [**medium**](#medium), включая опциональные, а также:

- ![#c5f015](https://via.placeholder.com/15/c5f015/000000?text=+) Итоговое приложение должно весить не более **100 KB** (сумма всех загружаемых файлов, исключая картинки);
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Drag-n-drop с поддержкой тач-скрина;
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=-) Масштабируемость на мобильные устройства до 320*480px (iPhone 4);
- Возможность быстрого просмотра и редактирования описания у любой задачи;

Опционально:
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=-) [SSR](https://google.com/search?q=SSR+(web+development));
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=-) [PWA](https://google.com/search?q=PWA+(web+development));
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=-) Опция фильтрации задач по RegExp;
<!-- - Если в двух вкладках открыт один и тот же проект (например, совершён импорт из одного и того же файла),\
  **все** действия в этих вкладках/проектах должны синхронизироваться без задержки.\
  Включая (но не ограничиваясь):
  - Название проекта;
  - Список, состояния, описания, порядок и названия всех задач\
    (например, при добавлении задачи в одной вкладке - она должна появиться и в другой);
  - Список сохранённых фильтров; -->
- ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=-) Возможность добавлять/удалять именованные списки для задач, между которыми их можно перетаскивать (как в trello);
