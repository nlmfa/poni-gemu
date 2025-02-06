# Электронный конспект по проекту с использованием Pygame

## 1. Какие особенности библиотека pygame вы изучили в ходе работы над
проектом
В ходе работы над проектом мы изучили несколько ключевых особенностей Pygame:

1. **Работа с графикой**: Pygame предоставляет удобные функции для работы с изображениями и графикой, что позволяет легко загружать и отображать спрайты.
```python
# загружаем в переменные картинки из папки с нашим файлом
back_main_screen = pygame.image.load('zastavka.jpg').convert()
back = pygame.image.load('fon.jpg').convert()
hero = pygame.image.load('strel.png').convert_alpha()
hero1 = pygame.image.load('changeling.png').convert_alpha()
heart1 = pygame.image.load('heart1.png').convert_alpha()
heart2 = pygame.image.load('heart2.png').convert_alpha()
heart3 = pygame.image.load('heart3.png').convert_alpha()
broke1 = pygame.image.load('broke1.png').convert_alpha()
broke2 = pygame.image.load('broke2.png').convert_alpha()
broke3 = pygame.image.load('broke3.png').convert_alpha()
bullet_image = pygame.Surface((10, 5))  # создаем пулю
bullet_image.fill((255, 0, 255))  # фиолетовый цвет пули
```
2. **Звуковые эффекты**: Pygame поддерживает работу со звуком, что добавляет атмосферу в игру.
```python
# загружаем звуки
pow_sound = pygame.mixer.Sound('pow.wav')         # звук попадания
loss_sound = pygame.mixer.Sound('loss.wav')       # звук потери жизни
gameover_sound = pygame.mixer.Sound('gameover.ogg')  # звук проигрыша
space_sound = pygame.mixer.Sound('space.wav')       # звук нажатия пробела
```
3. **Простота использования**: Для новичков Pygame предлагает понятный интерфейс и множество примеров, что облегчает обучение.

## 2. С Что собой представляет «Проект» как структура в Файловой системе на диске
Проект в файловой системе представляет собой каталог, который включает:

1. **Исходный код**: файлы с расширением `.py`, содержащие код игры.
2. **Ресурсы**: папки с изображениями, звуковыми файлами, шрифтами и другими медиафайлами.
3. **Конфигурационные файлы**: файлы README для описания проекта.

## 3. то такое виртуальное окружение? Как и когда его нужно создавать?
Виртуальное окружение — это изолированная среда, в которой можно устанавливать зависимости для конкретного проекта, не затрагивая глобальные настройки Python. Его стоит создавать:

- При начале нового проекта, чтобы избежать конфликтов зависимостей с другими проектами.
- Если требуется использовать разные версии библиотек для разных проектов.

## 4.  В чем особенности использование выбранной вами среды разработки при
работе над созданием игрового проекта?
При работе над игровым проектом с Pygame мы использовали среду разработки Visual Studio Code. Основные особенности:

1. **Поддержка плагинов**: позволяет установить расширения для работы с Python и Pygame, что упрощает процесс разработки.
2. **Отладка**: встроенные инструменты для отладки помогают находить и исправлять ошибки.
3. **Автодополнение кода**: экономит время при написании кода, предлагая подсказки и завершения.

## 5. Выделите приоритеты структуры программного кода. Раскрыть линейную последовательность с примерами, в каком порядке, что за чем следует при
создании игрового проекта на pygame?
При создании игрового проекта на Pygame важно следовать определенной последовательности:

1. **Импорт библиотек**: в начале файла импортируем нужные модули.
```python
# импортируем зависимости и дополнительные модули
import pygame
from sys import exit
import time
import random
```
2. **Инициализация Pygame**: здесь происходит настройка игры, создание окна и загрузка ресурсов.
```python
 включаем модуль pygame
pygame.init()

# загружаем звуки
pow_sound = pygame.mixer.Sound('pow.wav')         # звук попадания
loss_sound = pygame.mixer.Sound('loss.wav')       # звук потери жизни
gameover_sound = pygame.mixer.Sound('gameover.ogg')  # звук проигрыша
space_sound = pygame.mixer.Sound('space.wav')       # звук нажатия пробела

# загружаем музыку
pygame.mixer.music.load('music.wav')  # загружаем фоновую музыку

# объявляем ширину и высоту экрана
width = 800
height = 400
# создаём экран игры
screen = pygame.display.set_mode((width, height))
# устанавливаем количество кадров в секунду
fps = 60
# создаём объект таймера
clock = pygame.time.Clock()

# добавляем счётчики для подсчёта времени в игре — это будут наши очки
start_time = 0
final_score = 0
hit_count = 0  # переменная для подсчета попаданий
lives = 3  # количество жизней
```
3. **Создание классов объектов**: определяем классы для игровых объектов, таких как игрок, враги и элементы интерфейса.
```python
# загружаем в переменные картинки из папки с нашим файлом
back_main_screen = pygame.image.load('zastavka.jpg').convert()
back = pygame.image.load('fon.jpg').convert()
hero = pygame.image.load('strel.png').convert_alpha()
hero1 = pygame.image.load('changeling.png').convert_alpha()
heart1 = pygame.image.load('heart1.png').convert_alpha()
heart2 = pygame.image.load('heart2.png').convert_alpha()
heart3 = pygame.image.load('heart3.png').convert_alpha()
broke1 = pygame.image.load('broke1.png').convert_alpha()
broke2 = pygame.image.load('broke2.png').convert_alpha()
broke3 = pygame.image.load('broke3.png').convert_alpha()
bullet_image = pygame.Surface((10, 5))  # создаем пулю
bullet_image.fill((255, 0, 255))  # фиолетовый цвет пули

# даём название окну игры
pygame.display.set_caption('PONY.EXE Game')

# объявляем переменную-флаг для цикла игры
game = False

# текст с сообщением о столкновении
text_font_collide = pygame.font.Font('prstartk.ttf', 50)
text_collide = text_font_collide.render('GamE oVer!!', False, 'Red')
text_collide_rect = text_collide.get_rect(center=(400, 200))

# текст главного меню
text_font_new_game = pygame.font.Font('prstartk.ttf', 20)
text_newgame_str1 = text_font_new_game.render('If you want to start,', False, 'Red')
text_newgame_rect1 = text_newgame_str1.get_rect(center=(400, 350))
text_newgame_str2 = text_font_new_game.render('press space', False, 'Red')
text_newgame_rect2 = text_newgame_str2.get_rect(center=(400, 375))

# текст для подсчёта очков и попаданий
text_font_score = pygame.font.Font('prstartk.ttf', 15)
text_ts_font = pygame.font.Font('prstartk.ttf', 15)

# функция подсчёта очков и попаданий
def display_score():
    hit_surface = text_font_score.render(f'Hits: {hit_count}', False, 'White')
    hit_rect = hit_surface.get_rect(center=(400, 380))
    screen.blit(hit_surface, hit_rect)


# функция для сброса начальных параметров
def reset_game():
    global hero_rect, hero1_rect, bullets, game, hit_count, lives

    # начальные координаты для героя
    hero_x_pos = 150
    hero_y_pos = 180
    hero_speed = 100  # Начальная скорость героя

    # создаём рамки прямоугольников
    hero_rect = hero.get_rect(center=(hero_x_pos, hero_y_pos))

    # случайные координаты для hero1
    hero1_x_pos = 900
    hero1_y_pos = random.randint(50, 350)  # случайное положение по вертикали
    hero1_rect = hero1.get_rect(center=(hero1_x_pos, hero1_y_pos))

    # сбрасываем состояние игры
    bullets = []  # список пуль
    game = False
    hit_count = 0  # сброс счетчика попаданий
    lives = 3  # сброс жизней
```
4. **Основной игровой цикл**: это бесконечный цикл, который обрабатывает события, обновляет состояние игры.
```python
# запускаем функцию начального состояния игры
reset_game()

# запускаем бесконечный цикл
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            exit()

        if not game and event.type == pygame.KEYDOWN and event.key == pygame.K_SPACE:
            space_sound.play()  # воспроизводим звук при нажатии на пробел
            pygame.mixer.music.play(-1)  # начинаем воспроизводить музыку в цикле
            reset_game()
            game = True
            start_time = pygame.time.get_ticks()

        # проверка на нажатие ЛКМ для выстрела
        if game and event.type == pygame.MOUSEBUTTONDOWN and event.button == 1:
            bullet_rect = bullet_image.get_rect(center=(hero_rect.right, hero_rect.centery))
            bullets.append(bullet_rect)

    if game:
        keys = pygame.key.get_pressed()
        if keys[pygame.K_UP]:
            hero_rect.top -= 2.5
            if hero_rect.top <= 0:
                hero_rect.top = 0
        if keys[pygame.K_DOWN]:
            hero_rect.top += 2.5
            if hero_rect.bottom >= 400:
                hero_rect.bottom = 400

        # размещаем фон на главном экране
        screen.blit(back, (0, 0))
        screen.blit(hero, hero_rect)

        # двигаем hero1 влево
        hero1_rect.left -= 9
        screen.blit(hero1, hero1_rect)

        # если hero1 вышел за пределы экрана, перемещаем его назад
        if hero1_rect.right < 0:
            hero1_rect.left = 800  # ставим hero1 за пределы экрана
            hero1_rect.y = random.randint(0, 289)  # новая случайная позиция по вертикали

        # обработка движения пуль
        for bullet in bullets[:]:
            bullet.left += 10  # двигаем пулю вправо
            if bullet.left > width:  # удаляем пулю, если она вышла за пределы экрана
                bullets.remove(bullet)
            screen.blit(bullet_image, bullet)

            # проверка на столкновение пули с hero1
            if bullet.colliderect(hero1_rect):
                bullets.remove(bullet)  # удаляем пулю
                pow_sound.play()  # воспроизводим звук попадания
                hero1_rect.left = 800  # перемещаем hero1 за пределы экрана
                hero1_rect.y = random.randint(0, 289)  # новая случайная позиция по вертикали
                hit_count += 1  # увеличиваем счетчик попаданий

        # если модель игрока столкнулась с hero1...
        if hero_rect.colliderect(hero1_rect):
            lives -= 1  # уменьшаем количество жизней
            if lives > 0:  # воспроизводим звук потери жизни только если осталось больше одной жизни
                loss_sound.play()
            hero1_rect.left = 800  # перемещаем hero1 за пределы экрана
            hero1_rect.y = random.randint(0, 289)  # новая случайная позиция по вертикали

            # Если жизни закончились, показываем сообщение
            if lives <= 0:
                gameover_sound.play()  # воспроизводим звук проигрыша
                pygame.mixer.music.stop()  # останавливаем фоновую музыку
                screen.blit(text_collide, text_collide_rect)
                final_score = (pygame.time.get_ticks() - start_time) // 1000
                text_ts_text = text_ts_font.render(f'Total time: {final_score} sec', False, 'White')
                hits_text = text_ts_font.render(f'Total hits: {hit_count}', False, 'White')
                text_ts_rect = text_ts_text.get_rect(center=(400, 250))
                hits_rect = hits_text.get_rect(center=(400, 300))
                screen.blit(text_ts_text, text_ts_rect)
                screen.blit(hits_text, hits_rect)

                pygame.display.flip()
                time.sleep(3)
                game = False

        # Отображаем сердца и разбитые сердца
        if lives == 3:
            screen.blit(heart3, (90, 10))
            screen.blit(heart2, (50, 10))
            screen.blit(heart1, (10, 10))
        elif lives == 2:
            screen.blit(broke3, (90, 10))  # показываем разбитое сердце
            screen.blit(heart2, (50, 10))
            screen.blit(heart1, (10, 10))
        elif lives == 1:
            screen.blit(broke2, (50, 10))  # показываем разбитое сердце
            screen.blit(broke3, (90, 10))  # показываем разбитое сердце
            screen.blit(heart1, (10, 10))
        elif lives == 0:
            screen.blit(broke1, (10, 10))  # показываем разбитое сердце
            screen.blit(broke2, (50, 10))  # показываем разбитое сердце
            screen.blit(broke3, (90, 10))  # показываем разбитое сердце

        # выводим на экран финальные очки и попадания
        display_score()

    else:
        screen.blit(back_main_screen, (0, 0))
        screen.blit(text_newgame_str1, text_newgame_rect1)
        screen.blit(text_newgame_str2, text_newgame_rect2)

 pygame.display.update()
    clock.tick(fps)
```

## 6.  Зачем в проекте используются: циклы, условия, данные, структуры данных,
функции? Выделить и пояснить их назначение с особенностью реализации в
проекте? Что можно, или нужно изменить?
1. **Циклы**: основной цикл игры отвечает за постоянное обновление экрана и обработку событий. Например, `while running:`.
2. **Условия**: используются для проверки состояний, например, нажатия клавиш или столкновений между объектами, чтобы определить, что делать в каждом конкретном случае.
3. **Данные**: переменные хранят состояния игры, такие как счет игрока или здоровье.
4. **Структуры данных**: списки и словари помогают организовать и хранить множество объектов, например, для хранения всех врагов в игре.
5. **Функции**: помогают структурировать код и избежать его дублирования. Например, функция для обновления положения объектов или обработки столкновений.
