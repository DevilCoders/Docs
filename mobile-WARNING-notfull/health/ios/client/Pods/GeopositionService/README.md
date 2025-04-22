# GeopositionService

## Назначение

- Обертка над LocationManager позволяющая использовать данные пропозиции в удобном формате по всему проекту.
- Оповещение классов пользователей о изменении локации.
- Сохранение старой локации пользователя приложения.
- Расчет расстояний между локациями.

## Подключение

- В .podfile проекта указать ссылки на спецификации

	```
        source 'https://stash.desktop.dev.yandex.net/scm/mcp/mobile-cocoa-pod-specs.git'
        source 'https://github.com/CocoaPods/Specs.git'
        source 'https://bb.yandex-team.ru/scm/med/ios-pods.git'
	```
- Выключить проверку на статические транзитивные фреймворки
	
	```
		pre_install do |installer|

			# workaround for transitive dependencies with static libraries https://github.com/CocoaPods/CocoaPods/issues/3289
			Pod::Installer::Xcode::TargetValidator.send(:define_method, :verify_no_static_framework_transitive_dependencies) {}
        end
	```
- Добавить post-install обработчик для транзитивных фреймворков

	```
		post_install do |installer|

			# workaround for transitive dependencies with static libraries (https://github.com/CocoaPods/CocoaPods/issues/2926#issuecomment-255821325)
			project = installer.pods_project
	
			installer.aggregate_targets.each do |target|
				project.build_configurations.each do |build_configuration|
					configFilePath = target.xcconfig_path(build_configuration.name)
					configFile = File.read(configFilePath)
					configFile = configFile.gsub(/-framework "AppsFlyer" /, '')
					File.open(configFilePath, 'w') { |file| file << configFile }
				end
			end
		end
	```
- Собственно, подключить сам под
	
	```
		pod 'GeopositionService', '~> 1.1.2'
	```

- Установить NSLocationWhenInUseUsageDescription в Info.plist
- Установить NSLocationUsageDescription в Info.plist

## Changelog

    **1.3.0**
    - Обновление зависимостей. Поддержка iOS 11

    **1.2.0**
    - Обновление зависимостей. Поддержка iOS 11

    **1.1.2**
    - Рефакторинг

    **1.1.1**
    - Подключен YMUtils

    **1.1.0**
    - Миграция на Swift 3
    
    **1.0.0**
    - Первичная реализация

## Авторы

Nezhelskoy Aleksey, a-nezhelskoy@yandex-team.ru
Viktor Liubchenko,  v-liubchenko@yandex-team.ru
Aleksandr Zhilenko, a-zhilenko@yandex-team.ru
Roman Kuznetsov,    nix-kuznetsov@yandex-team.ru
Nezhelskoy Iliya,   nezhelskoy@yandex-team.ru

## License

Proprietary
