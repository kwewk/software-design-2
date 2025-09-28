# TypeScript Utility Library

Навчальний проєкт із поступової побудови та еволюції бібліотеки на **TypeScript**.  
Мета роботи — відпрацювати семантичне версіонування, налаштування інструментів розробки (ESLint, Prettier, Husky, Commitlint), використання `.env` + `zod`, а також показати приклади зростання складності API.

### Бібліотека покроково демонструє
- роботу з `package.json`, залежностями та npm-скриптами;
- використання змінних середовища через `.env` з валідацією (`zod`);
- основні можливості TypeScript: типи, інтерфейси, класи, generics;
- налаштування інструментів для контролю якості коду (ESLint, Prettier, Husky, Commitlint);
- застосування семантичного версіонування з git-тегами.

Розвиток іде від простих прикладів із `any` — до стабільного API та навіть breaking changes.

---

## Запуск проєкту

```bash
# Склонувати репозиторій
git clone <url>
cd <repo>

# Встановлення залежностей
npm install

# Демонстрація прикладів (src/demo.ts)
npm run demo

# Збірка (створює dist/ з CJS, ESM і .d.ts)
npm run build

# Перевірки
npm run typecheck
npm run lint
npm run format:check
```
---
## Еволюція бібліотеки
Кожен крок відображено у git-історії та тегах релізів (v0.1.0, v0.2.0, …, v2.0.0).
Основні зміни:

**0.1.0** – перші утиліти add, capitalize з типом any, приклади помилок лінтингу.

**0.2.0** – ті самі функції, але з базовими типами (number, string).

**0.3.0** – додано formatNumber з опціями точності (NumberFormatOptions).

**0.4.0** – додано інтерфейс User та generic-функцію groupBy<T>.

**0.5.0** – клас Logger, змінні оточення (.env + zod), formatNumber бере точність з APP_PRECISION.

**1.0.0** – стабілізація API: заборона any, експорти у package.json.

**2.0.0** – breaking change: add тепер приймає масив чисел (number[]).


## Приклади використання
``` ts
import { add, capitalize, formatNumber, groupBy, Logger, type User, config } from '@egor/utils';

// sum (починаючи з v2.0.0) — приймає масив чисел
console.log('sum result ->', add([1, 2, 3])); // 6

// capitalize — робить першу літеру великою
console.log('cap:', capitalize('hello')); // "Hello"

// formatNumber — спочатку дивиться на передані опції, якщо нема — бере з .env
console.log('formatted:', formatNumber(123.456, { precision: 2 })); // "123.46"

// groupBy — згрупуємо масив за ключем name
const people: User[] = [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' },
];
console.log('grouped by name ->', groupBy(people, 'name'));
// { Alice: [{ id: 1, name: 'Alice' }], Bob: [{ id: 2, name: 'Bob' }] }

// Logger — рівень береться з config (валідація через zod)
const logger = new Logger(config.LOG_LEVEL);
logger.info('Додаток запущено');
logger.debug('Детальне повідомлення для відладки');
```

---
## Конфігурація оточення (.env)
Файл .env (у .gitignore):
``` env
APP_PRECISION=3
LOG_LEVEL=debug
```
Валідація змінних здійснюється через zod.

---

## Скриншоти
У цьому розділі наведені демонстрації комітів (локальної роботи husky-хуків). Додаткові скріни (помилки та випралення та інші комміти) наведені в папці images.
- ![First commit](screenshots/0.0.0%20коміт.png)
- ![1.0.0 commit](screenshots/1.0.0%20коміт.png)
- ![2.0.0 commit](screenshots/2.0.0%20коміт.png)

---

## Теги та релізи
- [v0.1.0](https://github.com/kwewk/software-design-2/releases/tag/v0.1.0)
- [v0.2.0](https://github.com/kwewk/software-design-2/releases/tag/v0.2.0)
- [v0.3.0](https://github.com/kwewk/software-design-2/releases/tag/v0.3.0)
- [v0.4.0](https://github.com/kwewk/software-design-2/releases/tag/v0.4.0)
- [v0.5.0](https://github.com/kwewk/software-design-2/releases/tag/v0.5.0)
- [v1.0.0](https://github.com/kwewk/software-design-2/releases/tag/v1.0.0)
- [v2.0.0](https://github.com/kwewk/software-design-2/releases/tag/v2.0.0)
