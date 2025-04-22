### Порядок сборки

#### dev
Устанавливает dev зависимости в проект ./bootstrap.sh
```bash
npm run bootstrap
```

Запуск проекта ./run.sh
```bash
npm run run $projectname

# custom bundle
npm run run $projectname -- --entry=app/index
```

Сборка ./build.sh
```bash
npm run build
```

Устанавливает dev зависимости в проект
```bash
npm run bootstrap
```

#### CI

0) В TeamCity должны быть выставлены переменные окружения(Environment Variables):
    - env.S3_MDS_ACCESS_TOKEN
    - env.S3_MDS_SECRET_KEY
    - env.CONDUCTOR_TOKEN
    
в процессе выставляется 
    - env.VERSION

Подробнее https://confluence.jetbrains.com/display/TCD65/Build+Script+Interaction+with+TeamCity#BuildScriptInteractionwithTeamCity-AddingorChangingaBuildParameterfromaBuildStep

1) NPM install
```bash
npm config set scripts-prepend-node-path true
npm set progress=false
npm run bootstrap
```

2) увеличение версии в debian/changelog
```bash
./scripts/bump_version
```

3) сборка вебпак
```bash
./scripts/build_static
```

4) сборка пакета с нодой 
```bash
./scripts/build_debian
```

5) выкладываем собранные файлы в S3
```bash
./scripts/release_static
```

6) asd
```bash
./scripts/release_debian
```

