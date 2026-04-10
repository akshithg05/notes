Many websites support having their text in multiple languages. This is called internationalization.
Internationalization (i18n) in React is the process of designing your application to support multiple languages and cultural conventions (like date, time, and currency formats) without requiring core code changes. This is typically achieved using dedicated libraries, with the most popular being **react-i18next** and **React Intl**.

The text will not be hard coded, it will be dynamic UI.
See how to do that in the LLD test application of Namaste fsd github.


### i18next – `defaultNS`, `interpolation`, and `useTranslation`

- **`defaultNS`**
    - Default namespace (translation group) used by i18next
    - Example: `defaultNS: "common"` → `t("key")` resolves to `common:key`
    - Avoids writing `common:key` everywhere
- **`interpolation`**
    - Used to insert dynamic values into translations
    - Example: `"Hello {{name}}"` → `t("greeting", { name: "Akshith" })`
    - `escapeValue: false` → React already escapes values, so no double escaping
- **`useTranslation("common")`**
    - Hook to access translations in a component
    - `"common"` = namespace being used
    - Returns:
        - `t` → function to get translated strings
        - `i18n` → instance (for language switching, etc.)
- **`useTranslation()` vs `useTranslation("common")`**
    - Both work if `defaultNS = "common"`
    - But:
        - `useTranslation()` → uses default namespace
        - `useTranslation("common")` → explicit (recommended for scalability)

---

### 🧠 Mental Model

- **resources** → all translations
- **namespace (NS)** → grouping (e.g., `common`, `dashboard`)
- **defaultNS** → fallback namespace
- **useTranslation(NS)** → tells component which namespace to use