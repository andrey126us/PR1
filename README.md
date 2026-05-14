# Практическая работа №9: Работа с меню в Android

**Выполнил:**  
Саньков Андрей Александрович  
Группа: ИНС-б-о-24-1  
Направление: 09.03.02 «Информационные системы и технологии»

---

## Цель работы

Изучить способы создания и обработки событий от различных типов меню в Android: главного меню (OptionsMenu) и контекстного меню (ContextMenu). Научиться динамически изменять интерфейс приложения с помощью пунктов меню.

---

## Ход работы

### Задание 1. Создание проекта и подготовка интерфейса

Создан проект `MenuLab`. В `activity_main.xml` размещены `ImageView` (для отображения картинок) и поясняющий `TextView`. В папку `res/drawable` добавлены три изображения: `image1.png`, `image2.png`, `image3.png`.

**Скриншот интерфейса:**  

![](media/1.png)

**Рисунок 1** — Интрефейс главной страницы

---

### Задание 2. Создание OptionsMenu (главное меню) – смена изображения

**Описание:**  
Создан файл `res/menu/main_menu.xml` с тремя пунктами для выбора изображения. В `MainActivity` переопределены `onCreateOptionsMenu()` и `onOptionsItemSelected()`. При выборе пункта меняется картинка в `ImageView`.

**Фрагмент кода `main_menu.xml`:**
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:id="@+id/action_img1" android:title="Изображение 1" />
    <item android:id="@+id/action_img2" android:title="Изображение 2" />
    <item android:id="@+id/action_img3" android:title="Изображение 3" />
</menu>
```
