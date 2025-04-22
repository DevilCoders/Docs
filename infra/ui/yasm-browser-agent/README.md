# Yasm browser agent: push app metrics to Golovan

## Installation and Usage

### ES6 via npm

```
npm install @yandex-infracloud-ui/yasm-browser-agent
```

### Configuration & modules

```
import Stats from '@yandex-infracloud-ui/yasm-browser-agent;

Stats.config({
    ajax: true,
    exceptions: true,
		// ...other modules
}).install();

Stats.setUser('jondoe');
Stats.setTag('ui_version', '1.0.0');
```
