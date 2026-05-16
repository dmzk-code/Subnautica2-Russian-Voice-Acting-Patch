# Subnautica 2 Russian Voice Patch v2

Неофициальный патч русской озвучки для **Subnautica 2**.  
Патч заменяет английские FMOD voiceover-банки на русскую многоголосную озвучку и добавляет пропущенные системные предупреждения, включая короткие PDA-алерты вроде кислорода, еды, воды, здоровья, глубины и температуры.

> Патч не связан с Unknown Worlds, Krafton или официальной локализацией игры. Используйте его только с легальной копией Subnautica 2.

## Что сделано

- Полная замена найденных речевых потоков в целевых FMOD-банках на русскую озвучку.
- Добавлены пропущенные предупреждения PDA, включая `30 секунд` кислорода.
- Сохранены оригинальные звуковые эффекты, глитчи, сигналы, шумы и не-речевые элементы.
- Использована многоголосная TTS-озвучка: системные/PDA-реплики и отдельные персонажные/технические сообщения звучат разными голосами.
- Исправлены строки, где русская локализация игры фактически содержала английский текст.
- Добавлен установщик с автоматическим backup оригинальных `.bank` файлов.

## Покрытие v2

Патч пересобирает 8 банков:

```text
Subnautica2/Content/FMOD/Desktop/ambient_PDA.bank
Subnautica2/Content/FMOD/Desktop/arrival_sequence.bank
Subnautica2/Content/FMOD/Desktop/base_general.bank
Subnautica2/Content/FMOD/Desktop/pda.bank
Subnautica2/Content/FMOD/Desktop/st_dialogue_protovoid.bank
Subnautica2/Content/FMOD/Desktop/trident.bank
Subnautica2/Content/FMOD/Desktop/voiceover_BlackBoxes_EN.bank
Subnautica2/Content/FMOD/Desktop/voiceover_PDA_EN.bank
```

Статистика сборки v2:

| Тип | Количество |
| --- | ---: |
| Всего обработано аудиопотоков | 1895 |
| Речевых потоков | 1793 |
| Не-речевых эффектов сохранено оригинальными | 102 |
| Ручных правок ключевых фраз | 111 |

## Установка

1. Скачайте архив `Subnautica2-RussianVoicePatch-v2.zip` из Releases.
2. Распакуйте архив в папку игры, где находится `Subnautica2.exe`.
3. Запустите PowerShell из корня игры.
4. Выполните:

```powershell
powershell -ExecutionPolicy Bypass -File .\RussianVoicePatch\Install-RussianVoicePatch.ps1 -PayloadRoot .\RussianVoicePatch\payload_v2
```

Установщик перед заменой создаёт backup оригиналов:

```text
RussianVoicePatch/backups/<дата-время>/
```

## Проверка перед установкой

Чтобы увидеть, какие файлы будут заменены, без фактической установки:

```powershell
powershell -ExecutionPolicy Bypass -File .\RussianVoicePatch\Install-RussianVoicePatch.ps1 -PayloadRoot .\RussianVoicePatch\payload_v2 -DryRun
```

## Частые ошибки

Если PowerShell пишет, что `Install-RussianVoicePatch.ps1` не существует, значит архив распакован не в корень игры или команда запущена не из папки с `Subnautica2.exe`.

Если PowerShell пишет, что `payload_v2` не найден, проверьте имя папки внутри `RussianVoicePatch`. В старом архиве v2 payload мог быть упакован как `payload`. Для такого архива используйте:

```powershell
powershell -ExecutionPolicy Bypass -File .\RussianVoicePatch\Install-RussianVoicePatch.ps1 -PayloadRoot .\RussianVoicePatch\payload
```

## После обновления игры

Steam может вернуть оригинальные `.bank` файлы после обновления или проверки целостности. В этом случае просто повторите установку:

```powershell
powershell -ExecutionPolicy Bypass -File .\RussianVoicePatch\Install-RussianVoicePatch.ps1 -PayloadRoot .\RussianVoicePatch\payload_v2
```

## Откат

Есть два варианта:

- Скопировать оригинальные файлы обратно из последнего backup-каталога в `Subnautica2/Content/FMOD/Desktop/`.
- Либо выполнить проверку целостности файлов игры в Steam.

## Пересборка архива

Если нужно снова упаковать готовые patch-файлы в один архив:

```powershell
powershell -ExecutionPolicy Bypass -File .\RussianVoicePatch\Pack-RussianVoicePatch.ps1 -PayloadRoot .\RussianVoicePatch\payload_v2 -ArchivePath .\Subnautica2-RussianVoicePatch-v2.zip
```

## Пересборка FMOD-банков

Для разработчиков и ручной доработки озвучки:

```powershell
powershell -ExecutionPolicy Bypass -File .\RussianVoicePatch\Build-RussianVoiceBanksV2.ps1
```

Готовые банки появятся в:

```text
RussianVoicePatch/payload_v2/Subnautica2/Content/FMOD/Desktop/
```

## Структура проекта

```text
RussianVoicePatch/
  payload_v2/                       # готовые .bank файлы патча v2
  v2/                               # отчёты, манифесты и служебные файлы сборки
  manual_voice_overrides_v2.csv     # ручные правки коротких и важных фраз
  Install-RussianVoicePatch.ps1     # установка/backup
  Pack-RussianVoicePatch.ps1        # упаковка архива
  Build-RussianVoiceBanksV2.ps1     # пересборка банков v2
tools/
  *.exe / *.py                      # локальные инструменты извлечения, синтеза и сборки FMOD
```

## Известные ограничения

- Это TTS-озвучка, а не студийная запись актёров.
- Длинные сюжетные реплики на русском иногда занимают больше времени, чем оригинальные английские слоты, поэтому отдельные сцены желательно проверять в игре.
- Некоторые имена, термины и лорные названия могут требовать ручной литературной вычитки.

## Рекомендации

Если нашли фразу, которая звучит слишком быстро, слишком медленно, неестественно или не совпадает с текстом, приложите к issue:

- название события/банка, если известно;
- место в игре, где фраза звучит;
- что именно произносится сейчас;
- как лучше озвучить по-русски.

## Благодарности

Патч сделан как фанатская доработка русской версии игры для более комфортного прохождения.  
Оригинальная игра, аудио, персонажи, мир и все связанные материалы принадлежат их правообладателям.
