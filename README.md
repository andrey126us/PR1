# Практическая работа №8: Ресурсы. Работа с медиа-элементами

**Выполнил:**  
Саньков Андрей Александрович  
Группа: ИНС-б-о-24-1  
Направление: 09.03.02 «Информационные системы и технологии»

---

## Цель работы

Изучить способы добавления и отображения графических ресурсов, научиться работать с аудио- и видеофайлами в Android-приложениях, освоить управление воспроизведением медиа-контента.

---

## Ход работы

### Задание 1. Подготовка ресурсов

Создан проект `MediaLab`. В папку res/drawable добавлены 3 изображения (image.png). В папку res/raw добавлены аудиофайл `audio_sample.mp3` и видеофайл `video_sample.mp4`.

![Структура ресурсов](media/1.png)

**Рисунок 1** — Добавленные медиафайлы в `res/raw` и `res/drawable`

---

### Задание 2. Слайд-шоу из изображений

В `activity_main.xml` размещены `ImageView` и три кнопки: «Предыдущее», «Следующее», «Слайд-шоу». В `MainActivity` реализована логика переключения изображений и автоматическая смена каждые 2 секунды с помощью `Timer`.

**Код MainActivity.java (фрагмент):**

```
private int[] images = {R.drawable.image1, R.drawable.image2, R.drawable.image3, R.drawable.image4};
private int currentIndex = 0;
private Timer slideshowTimer;

private void showNextImage() {
    currentIndex = (currentIndex + 1) % images.length;
    imageView.setImageResource(images[currentIndex]);
}

private void toggleSlideshow() {
    if (slideshowTimer != null) {
        slideshowTimer.cancel();
        slideshowTimer = null;
    } else {
        slideshowTimer = new Timer();
        slideshowTimer.schedule(new TimerTask() {
            @Override
            public void run() {
                runOnUiThread(() -> showNextImage());
            }
        }, 0, 2000);

    }
}
```
![Структура ресурсов](media/2.png)

**Рисунок 2** —  Главный экран с изображением и кнопками управления

### Задание 3. Воспроизведение видео
Создана `VideoActivity` с разметкой, содержащей VideoView, SeekBar для громкости и кнопку «Воспроизвести». Реализовано управление громкостью через AudioManager, добавлены стандартные элементы управления (MediaController).
```
public class VideoActivity extends AppCompatActivity {
    private VideoView videoView;
    private SeekBar volumeSeekBar;
    private AudioManager audioManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_video);

        videoView = findViewById(R.id.videoView);
        volumeSeekBar = findViewById(R.id.volumeSeekBar);
        audioManager = (AudioManager) getSystemService(Context.AUDIO_SERVICE);

        // Настройка громкости через SeekBar
        int maxVolume = audioManager.getStreamMaxVolume(AudioManager.STREAM_MUSIC);
        volumeSeekBar.setMax(maxVolume);
        volumeSeekBar.setProgress(audioManager.getStreamVolume(AudioManager.STREAM_MUSIC));

        volumeSeekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
                audioManager.setStreamVolume(AudioManager.STREAM_MUSIC, progress, 0);
            }
            // ... пустые методы onStartTrackingTouch, onStopTrackingTouch
        });

        // Медиаконтроллер для управления воспроизведением
        MediaController mediaController = new MediaController(this);
        mediaController.setAnchorView(videoView);
        videoView.setMediaController(mediaController);

        // Установка источника видео из res/raw
        String videoPath = "android.resource://" + getPackageName()
                + "/" + R.raw.video_sample;
        videoView.setVideoURI(Uri.parse(videoPath));

        // Запуск по кнопке
        findViewById(R.id.btnPlayVideo).setOnClickListener(v -> videoView.start());
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        videoView.stopPlayback(); // освобождение ресурсов
    }
}
```

![Структура ресурсов](media/3.png)

**Рисунок 3** —  Главный экран с изображением и кнопками управления



