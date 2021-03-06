# Internationarization

Based on current browser locale the Dashboard can be displayed in one of the supported languages listed below. In case it does not work, make sure that your browser's locale is identified with correct language code.

| Language           | Code |
|--------------------|------|
| English (default)  | en   |
| French             | fr   |
| Japanese           | ja   |
| Korean             | ko   |
| Simplified Chinese | zh   |

## Building localized dashboard

To show localized dashboard, you need to build dashboard binary before.
To build dashboard binary, run `npm run build`. Or to build and run localized dashboard immediately, run `npm run start:prod`.

Note: Building localized dashboard takes time, so development environment, e.g. `npm start`, does not compile localized versions.

## Translation management

All translation data is stored in `i18n/` directory in project's root. It includes `locale_conf.json` configuration file, translation source file `messages.xlf` and localized files for each language, e.g. `fr/messages.fr.xlf` or `ja/messages.ja.xlf`.

## Introducing new localizable text

Localization is handled by [Angular](https://angular.io/guide/i18n).
Add `i18n` attribute into tag surrounding new text in Angular template html files.

### To update translation source file and localized files

Run `npm run fix:i18n`. It will execute `ng xi18n` and `xliffmerge`, they will update `i18n/messages.xlf` and `i18n/[locale]/messages.[locale].xlf` files.

### To translate new localizable text

`xliffmerge` would copy new localizable texts from `<source>` element to `<target>` element with `state="new"` attribute in your language file, i.e. `i18n/[locale]/messages.[locale].xlf`.
Find new localizable texts in `i18n/[locale]/messages.[locale].xlf` file and translate text in the `<target>` element.

## Introducing new language

1. Add your language code, e.g. `fr` or `ja`, into `"languages"` array of `"xfillmergeOptions"` in `package.json` file.
2. Run `npm run fix:i18n`. Then translation file for your language, e.g. `i18n/fr/messages.fr.xlf`, would be generated.
3. Open your language file and translate texts in `<target>` element into your language.

After preparation of new translation file, configure `i18n/locale conf.json` file to build newly localized dashboard as follows:

```
{"translations": [ "en", "fr", "ko", "zh" ]}
```

To add Japanese translation file, add `"ja"` into `"translations"` array in alphabetical order.

```
{"translations": [ "en", "fr", "ja", "ko", "zh" ]}
```

Then you can build your localized dashboard with `npm run build`.

Dashboard team have willing to transfer authority to review/approve for updating your translation file. If your translation team have willing to manage your translation file, add `i18n/[locale]/OWNERS` file and organize your translation team in it.

At last, please create Pull Request and submit it to `kubernetes/dashboard`.

----
_Copyright 2019 [The Kubernetes Dashboard Authors](https://github.com/kubernetes/dashboard/graphs/contributors)_
