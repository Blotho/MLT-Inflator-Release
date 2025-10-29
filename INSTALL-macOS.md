# Установка MLT Inflator на macOS

## Быстрая установка

### 1. Распакуйте архивы

**VST3:**
- Распакуйте `MLT-Inflator-macOS-VST3.zip`
- Переместите папку `MLT Inflator.vst3` в `/Library/Audio/Plug-Ins/VST3/`

**AU:**
- Распакуйте `MLT-Inflator-macOS-AU.zip`
- Переместите файл `MLT Inflator.component` в `/Library/Audio/Plug-Ins/Components/`

### 2. Запустите DAW

- Откройте вашу DAW (Ableton Live, Logic Pro, Reaper и др.)
- Выполните сканирование плагинов
- Добавьте MLT Inflator на канал

---

## Решение проблем с безопасностью macOS

### Способ 1: Через настройки системы (рекомендуется)

Ваш Mac заблокирует плагин при первом запуске.

**Шаги:**
1. Откройте **Системные настройки** → **Конфиденциальность и безопасность**
2. Нажмите **«Всё равно открыть»** (кнопка появится после попытки загрузки)
3. Перезапустите DAW
4. Добавьте плагин на канал
5. Нажмите **«Открыть»** в диалоговом окне

---

### Способ 2: Через терминал (если способ 1 не сработал)

Этот метод снимает карантин и подписывает плагин локально.

**Для VST3:**

```bash
sudo xattr -cr "/Library/Audio/Plug-Ins/VST3/MLT Inflator.vst3"
sudo xattr -r -d com.apple.quarantine "/Library/Audio/Plug-Ins/VST3/MLT Inflator.vst3"
sudo codesign --force --sign - "/Library/Audio/Plug-Ins/VST3/MLT Inflator.vst3"
```

**Для AU:**

```bash
sudo xattr -cr "/Library/Audio/Plug-Ins/Components/MLT Inflator.component"
sudo xattr -r -d com.apple.quarantine "/Library/Audio/Plug-Ins/Components/MLT Inflator.component"
sudo codesign --force --sign - "/Library/Audio/Plug-Ins/Components/MLT Inflator.component"
```

**Что делают эти команды:**
- `xattr -cr` — очищает все расширенные атрибуты
- `xattr -r -d com.apple.quarantine` — снимает карантин
- `codesign --force --sign -` — создаёт локальную подпись

Введите пароль администратора когда потребуется.

---

### Способ 3: Универсальная функция (для продвинутых пользователей)

Создайте функцию в терминале для быстрой разблокировки:

```bash
function prep() {
    sudo xattr -cr "$1"
    sudo xattr -r -d com.apple.quarantine "$1"
    sudo codesign --force --sign - "$1"
}
```

**Использование:**

```bash
prep "/Library/Audio/Plug-Ins/VST3/MLT Inflator.vst3"
```

Или перетащите файл прямо в терминал после команды `prep ` (с пробелом).

---

## Проверка установки

После установки проверьте:

**VST3:**
```bash
ls -la "/Library/Audio/Plug-Ins/VST3/MLT Inflator.vst3"
```

**AU:**
```bash
ls -la "/Library/Audio/Plug-Ins/Components/MLT Inflator.component"
```

Если файлы отображаются — установка прошла успешно.

---

## Совместимость

✅ macOS 10.15 (Catalina) и выше  
✅ Intel Mac (x86_64)  
✅ Apple Silicon (M1/M2/M3, arm64)  
✅ Universal Binary (работает на всех Mac)

---

## Поддержка

Если возникли проблемы:
- 📱 Telegram: https://t.me/Melody_Token
- 🌐 Сайт: https://melodytoken.ru/

---

© 2025 Blotho / Melody Token

