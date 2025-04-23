1. В `YREModuleBuilder.podspec` дописать подключение сабспеки. Сабспеки добавляем в алфавитном порядке.

  s.subspec '{{ module_name }}' do |ss|
    ss.dependency 'YREModuleBuilder/Core'

    ss.subspec 'Module' do |sss|
      sss.dependency '{{ yre_module_name }}Module/Module'

      sss.source_files  = 'Sources/{{ module_name }}/Module/**/*.{swift}'
    end

    ss.subspec 'Stub' do |sss|
      sss.dependency '{{ yre_module_name }}Module/Stub'

      sss.source_files  = 'Sources/{{ module_name }}/Stub/**/*.{swift}'
    end
  end

2. Прописать в DevWorkspace в `Podfile`

pod 'YREModuleBuilder/{{ module_name }}/Stub'

3. Добавить в `Podfile` 

    pod 'YREModuleBuilder/{{ module_name }}/Module'

4. Сделать `pod install`
