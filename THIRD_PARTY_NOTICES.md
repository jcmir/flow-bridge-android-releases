# Сторонние компоненты — проверка HOLD

Объём материалов, которые необходимо предоставить получателям лицензируемых компонентов, отдельно описан в [SOURCE_AVAILABILITY.md](SOURCE_AVAILABILITY.md). Наличие извлечённых текстов лицензий не подтверждает доступность соответствующих исходников.

Уведомления ниже относятся к APK 0.3.1 (build 10), SHA256 `a213b43e19c9b60b8b69ee041cc8039066a1df6edd984178ced9ab0b270cfd8a`. Содержимое native-библиотек, Gecko omni.ja и META-INF (кроме подписи) побайтно совпадает с ранее проверенным build 9. Сохранены извлечённые лицензии и метаданные версий.

## GeckoView и встроенные зависимости

GeckoView — Mozilla и другие участники. Локальная зависимость: `org.mozilla.geckoview:geckoview-arm64-v8a:157.0.20261005135250`. Основная лицензия Mozilla-кода — MPL 2.0; включённые компоненты имеют дополнительные условия.

Полный поставляемый в APK текст уведомлений сохранён без редактирования: [Gecko license.html](third-party/gecko/chrome/toolkit/content/global/license.html). Он включает MPL и уведомления встроенных компонентов. Дополнительно сохранены поставляемые лицензии PDF.js CMaps и шрифтов в `third-party/gecko/chrome/pdfjs/content/web/`.

В `buildconfig.html` внутри `assets/omni.ja` APK указана ревизия Mozilla: `737ec77d798755890b062aab541a90d6c75afd19`, ссылка [исходное дерево Mozilla](https://hg.mozilla.org/releases/mozilla-release/rev/737ec77d798755890b062aab541a90d6c75afd19). Ревизия соответствует тегу Firefox 157.0.1. Доступен [официальный архив исходников](https://archive.mozilla.org/pub/firefox/releases/157.0.1/source/firefox-157.0.1.source.tar.xz), проверка описана в [SOURCE_AVAILABILITY.md](SOURCE_AVAILABILITY.md).

[MPL 2.0, разделы 3.2–3.4](https://www.mozilla.org/en-US/MPL/2.0/) требует предоставить получателям доступ к соответствующему исходному коду покрываемых MPL компонентов и сохранить уведомления. Для larger work возможно отдельное лицензирование собственных материалов, при соблюдении MPL для покрываемой части. Точный источник native Gecko и путь получения исходников подтверждены. Полнота bundled notices и условия отдельных компонентов проверяются отдельно. Это не разрешение публиковать собственный закрытый код Flow Bridge.

## AndroidX, Kotlin и kotlinx.coroutines

Версионные маркеры, прочитанные непосредственно из APK: [inventory](third-party/apk-component-versions.json). Они подтверждают присутствие соответствующих маркеров, но не являются полным SBOM. Маркер arch.core содержит строку Gradle вместо номера версии; он требует отдельного разрешения по dependency graph.

Сохранены без изменения три текста Apache 2.0 из `META-INF/androidx/annotation/annotation/`, `META-INF/androidx/collection/collection/` и `META-INF/androidx/lifecycle/lifecycle-common/` в [third-party/apk](third-party/apk/). Текст [лицензии kotlinx.coroutines 1.9.0](third-party/kotlinx-coroutines-1.9.0-LICENSE.txt) проверен в upstream: Apache 2.0 с уведомлением JetBrains. Полный состав Kotlin runtime и notices ещё требует проверки по разрешённым зависимостям финальной сборки.

[Apache 2.0, раздел 4](https://www.apache.org/licenses/LICENSE-2.0.txt) предусматривает предоставление лицензии, сохранение применимых уведомлений, обозначение изменений и перенос применимых NOTICE, если они поставляются. Одного упоминания Apache 2.0 недостаточно для подтверждения выполнения всех условий каждого артефакта.

## Происхождение GeckoView в финальном APK

AAR `org.mozilla.geckoview:geckoview-arm64-v8a:157.0.20261005135250` совпал с контрольной суммой Mozilla Maven. Все 13 native-библиотек AAR и `assets/omni.ja` совпадают с финальным APK побайтно. В этих файлах локальных изменений не выявлено. Сопоставление преобразованного Java-кода в DEX и состава всех транзитивных библиотек отдельно не завершено.

### LGPL в точном arm64 APK

SoundTouch и Mozilla FFVPX распространяются с [текстом LGPL 2.1](third-party/LGPL-2.1.txt). Соответствующее дерево с изменениями Mozilla доступно в [официальном архиве Firefox 157.0.1](https://archive.mozilla.org/pub/firefox/releases/157.0.1/source/firefox-157.0.1.source.tar.xz). Сохранённые уведомления Mozilla входят в [license.html](third-party/gecko/chrome/toolkit/content/global/license.html).

| Компонент | Доказательство и исходники |
|---|---|
| SoundTouch | libxul.so объявляет DT_NEEDED liblgpllibs.so и импортирует RLBoxSoundTouch. liblgpllibs.so экспортирует соответствующие символы. В Mozilla vendoring указан SoundTouch f738b1132ec1fd56efc90367898244cf52d9e6a5, LGPL-2.1. [Метаданные и исходный путь media/libsoundtouch](https://hg.mozilla.org/releases/mozilla-release/raw-file/737ec77d798755890b062aab541a90d6c75afd19/media/libsoundtouch/moz.yaml). |
| FFmpeg (Mozilla FFVPX) | В libmozavcodec.so экспортируются avcodec_version, avcodec_configuration и avcodec_license, а бинарник содержит N-118248-g252fc2e047 и LGPL 2.1 or later. ELF ссылается на libmozavutil.so. Соответствующий код находится в media/ffvpx официального дерева Mozilla. [Текст LGPL в точной ревизии](https://hg.mozilla.org/releases/mozilla-release/raw-file/737ec77d798755890b062aab541a90d6c75afd19/media/ffvpx/COPYING.LGPLv2.1). |
| Graphite2 и Libav | Сводный Gecko notice упоминает эти проекты. В точном дереве Mozilla Graphite2 1.3.15 отмечен LGPL-2.1. В проверенных экспортируемых символах APK присутствие Graphite2 отдельно не установлено. Сводное уведомление не доказывает, что отдельная копия Libav вошла в данный APK. [Graphite2 vendoring](https://hg.mozilla.org/releases/mozilla-release/raw-file/737ec77d798755890b062aab541a90d6c75afd19/gfx/graphite2/moz.yaml). |

Для обоих компонентов выбран путь **§6(d) LGPL 2.1** для скачиваемого выпуска. Рядом с APK должен быть доступен комплект из §6(a): точные исходники библиотек с изменениями Mozilla и материалы, достаточные для получения работающего приложения с изменённой библиотекой. Официальный архив и точные ссылки приведены в [SOURCE_AVAILABILITY.md](SOURCE_AVAILABILITY.md). Исходники закрытой части можно заменить пригодными объектными материалами, если их достаточно для этой операции.

§6(b) для этого APK не подтверждён. Gecko загружает .so, поставляемые внутри APK. Наличие динамических зависимостей не показывает, что приложение работает с совместимой библиотекой, установленной пользователем отдельно. Изменение подписанного пакета требует отдельной подписи для тестовой копии.

APK также содержит маркеры Google Play services base 18.7.2, basement 18.9.0, fido 21.3.1 и tasks 18.3.2. Из четырёх AAR соответствующих версий сохранены исходные third_party_licenses.txt и индекс third_party_licenses.json. [Notices Google Play services](third-party/google-play-services/). Индексы и тексты из upstream не означают, что каждая перечисленная библиотека присутствует в финальном DEX. Декларации POM не заменяют сверку с содержимым DEX.

## Оставшееся условие LGPL

Для §6(d) отсутствует испытанный комплект пересборки связанного произведения. Нужны точные параметры сборки и ABI библиотек arm64, необходимые объектные или исходные материалы использующей части и инструкция упаковки и подписи копии пользовательским ключом. На изолированном arm64 Android нужно подтвердить запуск Gecko и фактический вызов изменённых SoundTouch и FFVPX. После проверки комплект должен быть доступен рядом с APK на тех же условиях скачивания. Исходный релизный APK можно сохранить. [LGPL 2.1, §6](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html).
