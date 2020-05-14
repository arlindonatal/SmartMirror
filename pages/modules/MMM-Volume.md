# MMM-Remote-Control

Este módulo é um auxiliar que irá funcionar como um controle remoto, desta forma poderá controlar o MagicMirror através do celular ou outro computador.

## Instalando o Módulo

```
cd ~/MagicMirror/modules # adapt directory if you are using a different one
git clone https://github.com/Jopyth/MMM-Remote-Control.git
cd MMM-Remote-Control
npm instal
```

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

No início do arquivo altere os seguintes dados:

```
address : '0.0.0.0',
//defina sua faixa de ip que terá acesso ao controle
ipWhitelist: ["127.0.0.1", "::ffff:127.0.0.1", "::1", "::ffff:192.168.0.42", "::ffff:192.168.0.50"],"
```

Adicione o módulo no final:
```
{
  module: 'MMM-Remote-Control',
  // uncomment the following line to show the URL of the remote control on the mirror
  // , position: 'bottom_left'
  // you can hide this module afterwards from the remote control itself
  config: {
  //     customCommand: {},  // Optional, See "Using Custom Commands" below
  //     customMenu: "custom_menu.json", // Optional, See "Custom Menu Items" below
  //     showModuleApiMenu: true, // Optional, Enable the Module Controls menu
      apiKey: "",         // Optional, See API/README.md for details
  }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

- Para acessa digite no navegador: http://IP_DO_RASPBERRY:8080/remote.html

[Clique aqui](https://github.com/Jopyth/MMM-Remote-Control) para ver as opções do módulo.
