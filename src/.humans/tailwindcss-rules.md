# tailwindcss rules

## Tailwind Core

- Использовать классы Tailwind CSS для стилизации HTML. Перед добавлением собственных классов проверять и использовать существующие соглашения Tailwind в проекте.
- Предлагать вынос повторяющихся шаблонов в компоненты, соответствующие соглашениям проекта (например, Blade, JSX, Vue и т.д.).
- Продумывать размещение классов, их порядок, приоритет и значения по умолчанию:
  удалять избыточные классы, аккуратно добавлять классы на родительские или дочерние элементы, логически группировать элементы, чтобы минимизировать дублирование.
- При необходимости можно использовать инструмент `search-docs` для получения точных примеров из официальной документации.

### Отступы (Spacing)
- При выводе списков элементов использовать утилиты `gap` для задания отступов, **не использовать margin**.

```html
<div class="flex gap-8">
    <div>Superior</div>
    <div>Michigan</div>
    <div>Erie</div>
</div>
```

### Тёмная тема (Dark Mode)
- Если существующие страницы и компоненты поддерживают тёмную тему, новые страницы и компоненты **обязаны** поддерживать её аналогичным образом, как правило с использованием префикса `dark:`.

---

## Tailwind 4

- Всегда использовать Tailwind CSS версии 4 — не применять устаревшие (deprecated) утилиты.
- `corePlugins` не поддерживается в Tailwind v4.
- В Tailwind v4 конфигурация является CSS-first и выполняется через директиву `@theme` — отдельный файл `tailwind.config.js` не требуется.

```css
@theme {
  --color-brand: oklch(0.72 0.11 178);
}
```

- В Tailwind v4 Tailwind подключается через обычный CSS `@import`, а не через директивы `@tailwind`, использовавшиеся в v3:

```diff
- @tailwind base;
- @tailwind components;
- @tailwind utilities;
+ @import "tailwindcss";
```

---

### Заменённые утилиты
- В Tailwind v4 удалены устаревшие утилиты. Не использовать deprecated-варианты — применять их актуальные замены.
- Значения opacity по‑прежнему задаются числовыми значениями.

| Устаревшая утилита | Замена |
|--------------------|--------|
| bg-opacity-* | bg-black/* |
| text-opacity-* | text-black/* |
| border-opacity-* | border-black/* |
| divide-opacity-* | divide-black/* |
| ring-opacity-* | ring-black/* |
| placeholder-opacity-* | placeholder-black/* |
| flex-shrink-* | shrink-* |
| flex-grow-* | grow-* |
| overflow-ellipsis | text-ellipsis |
| decoration-slice | box-decoration-slice |
| decoration-clone | box-decoration-clone |
