# WallberryTheme

Este módulo irá reestilizar o MagicMirror, alterando a fonte, cores e alterando o background usando imagens do Unsplash.com.

## Instalando o Módulo

```
cd ~/MagicMirror/modules
git clone https://github.com/delightedCrow/WallberryTheme.git
cd WallberryTheme
npm install
```

Obs: Crie uma conta em Unsplash.com e gere uma aplicação e copie a API_KEY.

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
    module: "WallberryTheme",
    position: "fullscreen_below", // Required Position
    backgroundOpacity: 0,
    brightImageOpacity: 0,
    addBackgroundFade: ["top"],
    config: {
      unsplashAccessKey: "XXX", // API do UNSPLASH
      collections: "" // Altere para as collections que achar melhor acesse Unsplash.com, acesse a collections e copie apenas o código da url.
    }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

[Clique aqui](https://github.com/delightedCrow/WallberryTheme) para ver as opções do módulo.
