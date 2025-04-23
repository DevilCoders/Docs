# Toloka Templates Starter

Starter project for developing your next excellent Yandex.Toloka template.

## Getting Started

Clone this repo:

```
git clone ssh://git@bb.yandex-team.ru/assessment/toloka-templates-starter.git
```

Install dependencies:

```
npm i
```

### Running

Start Toloka Templates Server using next command:

```
npm run server
```

Create config of your Toloka project for deployment using:

```
npm run download
```

Deploy changes to your project using:

```
npm run deploy
```

Convert ES6 -> ES5:

```
npm run build
```

### Configure

Starter can handle 2 configs:

- tts.config.js, read more at [toloka-temalates-server](https://bb.yandex-team.ru/projects/ASSESSMENT/repos/toloka-templates-server/browse)
- ttd.config.js, read more at [toloka-templates-deploy](https://bb.yandex-team.ru/projects/ASSESSMENT/repos/toloka-templates-deploy/browse)

## Built With

* [toloka-templates-kit](https://bb.yandex-team.ru/projects/ASSESSMENT/repos/toloka-templates-kit/browse) - tool for developing templates for Yandex.Toloka

## Developers

* **German Volkov** - *TTK developer, initial work* - [@volkov97](https://staff.yandex-team.ru/volkov97)
* **Alexander Verkhoglyad** - *Yandex.Toloka developer, PR reviews* - [@hexode](https://staff.yandex-team.ru/hexode)
