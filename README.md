# CorporationX

Это проект над которым я работал вместе со своей командой из 8 человек. Писали проект на микросервисной архитектуре. Т.к. над проектом работали разные команды, то для изучения всего кода моей команды необходимо смотреть сервисы в ветке kraken-master-stream6. Фичи реализованные мной будут указаны ниже.

# My features

## 1. Создание и настройка скилов пользователя
SkillHub позволяет пользователям добавлять, настраивать и делиться своими навыками с другими. Это помогает раскрыть потенциал, рассказать о своих умениях и расширить возможности для сотрудничества. Проект включает:
-	Создание навыков: уникальные навыки добавляются в базу и становятся доступными всем пользователям.
-	Управление навыками: просматривай список своих навыков и получай рекомендации от других пользователей.
-	Приобретение предложенных навыков: если навык рекомендован минимум 3 пользователями, он может быть добавлен в ваш профиль.
-	[SkillController.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26808/src/main/java/school/faang/user_service/controller/SkillController.java)
- [SkillMapper.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26808/src/main/java/school/faang/user_service/mapper/SkillMapper.java)
- [SkillService.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26808/src/main/java/school/faang/user_service/service/SkillService.java)
- [SkillServiceTest.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26808/src/test/java/school/faang/user_service/service/SkillServiceTest.java)

## 2. Внедрение CI pipeline для user_service
В рамках задачи настроен CI-пайплайн для репозитория user_service с использованием GitHub Actions. CI предоставляет автоматизированные процессы для тестирования кода при каждом пулл-реквесте, что обеспечивает стабильность и качество разработки. 
- [ci.yml](https://github.com/CorporationX/user_service/blob/feature-BJS2-26837/.github/workflows/ci.yml)

## 3. Добавление системы альбомов постов
PostAlbum добавляет возможность пользователям организовывать посты в альбомы для упрощения работы с контентом и тематических подборок. Основной функционал:
-	Создание альбомов: пользователи могут создавать альбомы с уникальными для них названиями и описаниями.
-	Добавление и удаление постов: пользователи управляют содержимым своих альбомов, добавляя или удаляя посты.
-	Избранные альбомы: пользователи могут добавлять альбомы в избранные для быстрого доступа.
-	Фильтрация и поиск: расширенные возможности фильтрации и поиска по собственным или всем альбомам в системе.
-	Редактирование и удаление: возможность обновления информации об альбоме или удаления ненужных.

  Система позволяет эффективно управлять контентом, упрощает поиск и организацию постов, а также улучшает пользовательский опыт благодаря гибкому функционалу.
- [AlbumController.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26856/src/main/java/faang/school/postservice/controller/AlbumController.java)
- [Album.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26856/src/main/java/faang/school/postservice/model/Album.java)
- [PostRepository.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26856/src/main/java/faang/school/postservice/repository/PostRepository.java)
- [AlbumService.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26856/src/main/java/faang/school/postservice/service/AlbumService.java)

## 4. Добавление аватара пользователя 
Разработал функционал управления аватарами пользователей с использованием Minio и Amazon S3 API. Реализовал загрузку с валидацией размера файла (до 5 Мб), автоматическую обработку изображений для создания двух версий (1080 px и 170 px), сохранение данных в PostgreSQL через embedded entity, а также безопасное удаление аватаров из хранилища и базы. Обеспечил отказоустойчивость и оптимизацию работы с графикой.
- [UserService.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26872/src/main/java/school/faang/user_service/service/user/UserService.java)
- [S3ServiceImpl.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26872/src/main/java/school/faang/user_service/service/s3/S3ServiceImpl.java)
- [UploadAvatarToS3.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26872/src/main/java/school/faang/user_service/service/s3/UploadAvatarToS3.java)
- [application.yaml](https://github.com/CorporationX/user_service/blob/feature-BJS2-26872/src/main/resources/application.yaml)

## 5. Публикация постов по расписанию
Реализовал функционал планирования и автоматической публикации постов. Добавил возможность указывать дату и время публикации через поле scheduledAt в PostDto. Настроил регулярный запуск публикации запланированных постов с использованием Spring Scheduler. Разработал многопоточный механизм публикации с помощью пула потоков, что позволяет обрабатывать большое количество постов параллельно, минимизируя задержки. Обновил логику PostService для управления статусами публикации, интегрировал с PostRepository для оптимальной работы с базой данных. Написал unit-тесты для проверки корректности работы всех компонентов.
- [ScheduledPostPublisher.java](https://github.com/CorporationX/post_service/blob/feature-BJS2-26895/src/main/java/faang/school/postservice/scheduled/ScheduledPostPublisher.java)

## 6. Уведомление о подписке
Реализовал функционал отправки и обработки уведомлений о подписке между пользователями. Настроил взаимодействие между сервисами через Redis Pub/Sub. В user_service создал отправитель событий FollowerEventPublisher, который публикует данные о подписке, включая идентификаторы подписчика и пользователя, на которого подписались. В notification_service разработал обработчик событий FollowerEventListener, который слушает события из Redis и отправляет уведомления пользователям. Настроил генерацию сообщений с помощью MessageBuilder, обеспечив кастомизацию содержания уведомлений через конфигурацию messages.yaml. Обеспечил интеграцию всех компонентов с учетом предпочтений пользователей по способу получения уведомлений.
- [FollowerEventListener.java](https://github.com/CorporationX/notification_service/blob/feature-BJS2-26949/src/main/java/faang/school/notificationservice/publis/listener/follower/FollowerEventListener.java)
- [RedisConfig.java](https://github.com/CorporationX/notification_service/blob/feature-BJS2-26949/src/main/java/faang/school/notificationservice/config/redis/RedisConfig.java)
- [FollowerEventAspect.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26949/src/main/java/school/faang/user_service/publis/aspect/FollowerEventAspect.java)
- [FollowerEventPublisher.java](https://github.com/CorporationX/user_service/blob/feature-BJS2-26949/src/main/java/school/faang/user_service/publis/publisher/FollowerEventPublisher.java)

## 7. Отправка сообщений в Telegram
Реализовал интеграцию с Telegram для отправки нотификаций через собственного Telegram-бота. Настроил TelegramService, который отвечает за отправку сообщений пользователям. Бот создан и зарегистрирован с использованием официального API Telegram, а конфигурация для взаимодействия с ботом добавлена в application.yaml. TelegramService интегрирован в notification_service и реализует интерфейс NotificationService, обрабатывая входящие сообщения и отправляя их пользователям в соответствии с их Telegram ID. Обеспечено покрытие функционала unit-тестами для гарантии стабильности и корректности работы.
- [TelegramBotService.java](https://github.com/CorporationX/notification_service/blob/feature-BJS2-26950/src/main/java/faang/school/notificationservice/service/TelegramBotService.java)
- [NotificationServiceApp.java](https://github.com/CorporationX/notification_service/blob/feature-BJS2-26950/src/main/java/faang/school/notificationservice/NotificationServiceApp.java)

## 8. News Feed
Реализация killer-feature News Fead News Feed - фича которая включает в себя формирования ленты новостей, для каждого пользователя

Формирование ленты постов в Redis: Лента постов каждого пользователя должна сохраняться в кэше Redis для быстрого доступа и повышения производительности.

Обработка конкурентного доступа: Использование Optimistic Lock для управления конкурентным доступом к данным в Redis и предотвращения коллизий при обновлении.

Интеграция с Kafka: Подключение к Kafka для обработки событий (публикация постов, комментарии, просмотры, лайки) и формирования ленты на основе этих данных.

Разогреватель фида: Реализация механизма предварительной генерации ленты (news feed) для всех пользователей при первом запуске приложения.

Эндпоинты для получения постов: Создание API для получения пачек постов из пользовательской ленты, соответствующих текущему состоянию news feed.
- [AbstractKafkaProducer.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/producer/AbstractKafkaProducer.java) | [KafkaPostProducer.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/producer/KafkaPostProducer.java)
- [KafkaPostPublishConsumer.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/listener/KafkaPostPublishConsumer.java)
- [NewsFeedRedisRepository.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/repository/NewsFeedRedisRepository.java)  
- [NewsFeedController.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/controller/NewsFeedController.java) | [NewsFeedService.java](https://github.com/CorporationX/post_service/blob/news-feed-team2-developer/src/main/java/faang/school/postservice/service/NewsFeedService.java)
