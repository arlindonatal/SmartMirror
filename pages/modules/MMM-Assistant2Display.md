# MMM-Assistant2Display

Este módulo é um auxiliar do [MMM-AssistantMk2](/pages/modules/MMM-AssistantMk2.md). Ele será acionado após o Google Assistant retornar um resultado, seja foto, vídeo, link. Também tem a opção de cast, que você poderá transmitir um vídeo do youtube do seu celular.

## Instalando o Módulo

```
cd ~/MagicMirror/modules
git clone https://github.com/bugsounet/MMM-Assistant2Display.git
cd MMM-Assistant2Display
npm install

```

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
  module: "MMM-Assistant2Display",
  position: "middle_center",
  config: {
    debug:true,
    useYoutube: true, 
    links: { 
      useLinks: true, 
      displayDelay: 30 * 1000,
      scrollStep: 25,
      scrollInterval: 1000,
      scrollStart: 1000,
      scrollActivate: false,
      verbose: false
    },
    photos: {
      usePhotos: true,
      displayDelay: 10 * 1000,
    },
    briefToday: {
      useBriefToday: false
    },
    cast: {
      useCast: true,
      castName: "Espelho", //nome que irá aparecer no compartilhamento do youtube
      port: 8569
    },
    screen: { // desligamento automático da tela
      useScreen: true,
      delay: 5 * 60 * 1000, // 5min
      turnOffDisplay: true,
      ecoMode: true,
      displayCounter: false,
      text: "Desligando a tela em:",
      detectorSleeping: false,
      governorSleeping: false,
      rpi4: false
    },
  }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

[Clique aqui](https://github.com/bugsounet/MMM-Assistant2Display) para ver as opções do módulo.
