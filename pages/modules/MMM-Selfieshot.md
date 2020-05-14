# MMM-Selfieshot

Este módulo permitirá tirar selfie por comando de voz utilizando uma webcam.

## Instalando o Módulo

```
sudo apt-get install fswebcam

cd ~/MagicMirror/modules
git clone https://github.com/eouia/MMM-Selfieshot
cd MMM-Selfieshot
npm install
```

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
  disabled: false,
  module: "MMM-Selfieshot",
  config: {
    debug: false, // You can get more detailed log. If you have an issue, try to set this to true.
    storePath: "./photos", // No need to modify.
    width:1280,
    height:720, // In some webcams, resolution ratio might be fixed so these values might not be applied.
    quality: 100, //Of course.
    device: null, // `null` for default camera. Or,
    // device: "USB Camera" or "/video/video11" <-- See the backend log to get your installed camera name.
    shootMessage: "Sorria!",
    shootCountdown: 5, // 5,4,3,2,1,0 then shutter.
    displayCountdown: true,
    displayResult: true,
    playShutter: true,
    shutterSound: "shutter.mp3",
    useWebEndpoint: "selfie", // This will activate 'https://YOUR_MM_IP_OR_DOMAIN:PORT/selfie [POST]' as web API endpoint.
    resultDuration: 1000 * 2,
    sendTelegramBot: false,
    sendMail: null, // or your email config (option for nodemailer https://nodemailer.com/about/)
  }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

## Comando de Voz

1. Crie um arquivo em:
```
nano ~/MagicMirror/modules/MMM-AssistantMk2/recipes/with-Selfie.js
```

```
var recipe = {
  transcriptionHooks: {
    "HOOKING_SELFIE": {
      pattern: "tirar selfie",
      command: "SELFIE"
    },
  },

  commands: {
    "SELFIE": {
      notificationExec: {
        notification: "SELFIE_SHOOT"
      },
      soundExec: {
        chime: "open"
      }
    }
  }
}

exports.recipe = recipe // Don't remove this line.
```

2. Salve o arquivo "CTRL + O" e feche-o "CTRL + X".


3. Adicione o arquivo "with-Selfie" nos recipes do MMM-AssistantMk2:
```
nano ~/MagicMirror/config/config.js

{
    module: "MMM-AssistantMk2",
    ...
    recipes: ["Reboot-Restart-Shutdown.js", "with-MMM-Spotify.js", "with-Selfie.js"]
    ...
}
```

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

- Para acionar fale: "tirar selfie".

[Clique aqui](https://github.com/BrianHepler/MMM-Selfieshot) para ver as opções do módulo.
