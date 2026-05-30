# Variables de Entorno — <PROJECT_NAME>

Las variables marcadas como **Required: `true`** deben estar presentes al iniciar la aplicación. Si faltan, la aplicación lanza un error y no arranca.

> **Formato estricto**: ver `examples/environments-example.md` en la skill. Cada variable debe listar Default, Required, y cuando aplique: Valores, Ejemplo, Rango, o notas de Producción.

---

### APLICACIÓN

* **<VAR_NAME>**: <DESCRIPTION>.
  - Default: <DEFAULT_OR_NINGUNO>
  - Required: `<true|false>`
  - Valores: <ENUM_VALUES> *(omitir si no aplica)*
  - Ejemplo: `<EXAMPLE>` *(omitir si no aplica)*
  - Rango válido: `<RANGE>` *(omitir si no aplica)*

---

### AUTH / JWT

* **<VAR_NAME>**: <DESCRIPTION>.
  - Default: <DEFAULT_OR_NINGUNO>
  - Required: `<true|false>`
  - **Producción**: <PRODUCTION_NOTES>

---

### <OTHER_SECTION>

* **<VAR_NAME>**: <DESCRIPTION>.
  - Default: <DEFAULT_OR_NINGUNO>
  - Required: `<true|false>`
