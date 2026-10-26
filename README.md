# Parts Relay locales

Every text of Parts Relay. The core ([PartsRelay/core](https://github.com/PartsRelay/core)) mounts this repository as a git submodule at `resources/lang`, the UI ([PartsRelay/ui](https://github.com/PartsRelay/ui)) at `src/locales`. Neither app keeps texts of its own, so clone them with `--recurse-submodules`.

## Layout

```
<locale>/<namespace>.json
```

- One folder per locale (`en-US`, `it-IT`). Every locale has the same files and the same keys as `en-US`.
- The namespace is the first segment of a key: `t('lookups.list.count')` reads `list.count` from `<locale>/lookups.json`.
- `emails` and `bot` (WhatsApp replies) belong to the core, the other namespaces to the UI.
- Keys are kebab-case.
- No JSON or YAML file at the repository root: the core would load it as a locale.

## Messages

Texts use [ICU MessageFormat](https://formatjs.github.io/docs/core-concepts/icu-syntax), read by `@adonisjs/i18n` in the core and `i18next-icu` in the UI.

- Argument: `Signed in as {email}.`
- Plural: `{count, plural, one {# search} other {# searches}}`
- Select: `{role, select, admin {an admin} other {a viewer}}`
- An apostrophe right before `{`, `}` or `#` starts quoted text: write it twice (`''`).
- The product name is written as is: `Parts Relay`.

## Adding a key

1. Add the key to the namespace file of every locale. A new namespace is a new file in every locale; a new locale is a new folder with every file.
2. Commit and push to `main`.
3. In the app, run `git submodule update --remote <path>`, call `t('namespace.key', values)` and commit the new submodule pointer with the code.

Remove a key when no app uses it any more.
