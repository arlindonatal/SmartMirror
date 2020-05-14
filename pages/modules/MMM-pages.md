# MMM-pages

Este é um módulo um auxiliar para organizar os demais módulos em páginas.

## Instalando o Módulo

```
cd ~/MagicMirror/modules
git clone https://github.com/edward-shen/MMM-pages.git
npm install
```

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
    module: 'MMM-pages',
    config: {
      modules:
      [
        [ "calendar", "weatherforecast", "newsfeed", "compliments", "currentweather", "MMM-Spotify"],
        ["MMM-GooglePhotos"]
      ],
      fixed: ["clock", "MMM-Volume", "MMM-Assistant2Display", "MMM-AssistantMk2",  "MMM-page-indicator",
        "MMM-Selfieshot", "WallberryTheme", "MMM-Remote-Control", "updatenotification", "alert"
        ],
      rotationTime : 1 * 60 * 1000,
      delayTime : 5 * 60 * 1000
    }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

[Clique aqui](https://github.com/edward-shen/MMM-pages) para ver as opções do módulo.

## MMM-page-indicator

O MMM-page-indicator funciona junto com o MMM-pages, ele irá exibir o indicador da página atual.

```
cd ~/MagicMirror/modules
git clone https://github.com/edward-shen/MMM-page-indicator.git
npm install
```

```
nano ~/MagicMirror/config/config.js
```

```
{
  module: 'MMM-page-indicator',
  position: 'bottom_bar',
  config: {
    pages: 2, //Número  de páginas
  }
},
```

[Clique aqui](https://github.com/edward-shen/MMM-page-indicator) para ver as opções do módulo.

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```
