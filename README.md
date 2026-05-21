
# Практическая работа №12: Типы активностей. Шаблоны Android Studio. Сохранение настроек с SharedPreferences

**Выполнил:**  
Саньков Андрей Александрович  
Группа: ИНС-б-о-24-1  
Направление: 09.03.02 «Информационные системы и технологии»

---

## Цель работы

Изучить различные типы шаблонов активностей, предоставляемых Android Studio. Научиться создавать многоэкранные приложения с использованием разных видов окон. Освоить механизм сохранения простых пользовательских настроек с помощью SharedPreferences.

---

## Ход работы

### Задание 1. Создание проекта и подготовка

Создан новый проект MultiWindowApp с пустой активностью.

![](media/1.png)

**Рисунок 1** — Создание проекта

### Задание 2. Добавление активностей по шаблонам
Создадим три активности:

SettingsActivity (шаблон Settings Activity) — экран настроек.

GameActivity (Empty Activity) — экран игры.

RecordsActivity (Empty Activity) — экран рекордов.

### 2.1 SettingsActivity
SettingsActivity — создана с использованием шаблона Settings Activity.
Автоматически сгенерированы файлы: класс SettingsActivity, разметка activity_settings.xml и файл настроек res/xml/root_preferences.xml.
Настройки будут сохраняться в SharedPreferences с именем файла по умолчанию.

Файл настроек res/xml/root_preferences.xml:

```xml
<PreferenceScreen xmlns:app="http://schemas.android.com/apk/res-auto">
    <EditTextPreference
        app:key="player_name"
        app:title="Имя игрока"
        app:summary="Введите ваше имя"
        app:useSimpleSummaryProvider="true" />
    <ListPreference
        app:key="difficulty"
        app:title="Сложность"
        app:summary="Выберите уровень сложности"
        app:entries="@array/difficulty_entries"
        app:entryValues="@array/difficulty_values"
        app:defaultValue="medium"
        app:useSimpleSummaryProvider="true" />
    <SwitchPreference
        app:key="sound_enabled"
        app:title="Звук"
        app:summary="Включить звуковые эффекты"
        app:defaultValue="true" />
</PreferenceScreen>
![](media/2.png)
```

**Рисунок 2** —  Создание класс SettingsActivity






