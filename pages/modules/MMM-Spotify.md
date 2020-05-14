# MMM-Spotify

O MMM-Spotify irá controlar o Spotify (buscar música, play, pause, próxima, anterior, etc.)

## Instalando o Módulo

```
cd ~/MagicMirror/modules
git clone https://github.com/eouia/MMM-Spotify
cd MMM-Spotify
npm install
```

## Configurando a conta do Spotify

É necessário ter uma conta premium.

1. Acesse https://developer.spotify.com;
2. DASHBOARD > Create an app
3. Após criado a conta, clique em "Edit Settings"
4. Adicione em Redirect URIs : http://localhost:8888/callback
5. Copie o Client ID e Client Secret

## Configurando a Autorização

```
cd ~/MagicMirror/modules/MMM-Spotify
cp spotify.config.json.example spotify.config.json
nano spotify.config.json
```

- Altere as informações com os dados da sua conta e client id e client secret gerado:
```
[
  {
      "USERNAME": "USERNAME", //ALTERAR
      "CLIENT_ID" : "YOUR_CLIENT_ID", //ALTERAR
      "CLIENT_SECRET" : "YOUR_CLIENT_SECRET", //ALTERAR
      "AUTH_DOMAIN" : "http://localhost",
      "AUTH_PATH" : "/callback",
      "AUTH_PORT" : "8888",
      "SCOPE" : "user-read-private playlist-read-private streaming user-read-playback-state user-modify-playback-state",
      "TOKEN" : "./token.json" 
  }
]
```

Obs: É possível adicionar várias contas, para isso só repetir para configurar a outra conta no Spotify Developer e copiar o trecho acima para a nova conta.

- Gerar autorização
```
cd ~/MagicMirror/modules/MMM-Spotify
node first_auth.js
```

Será aberta uma página para autorizar o acesso ao spotify. Realize o login e permita o acesso.

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
  module: "MMM-Spotify",
  position: "top_left",
  config: {
    style: "mini", // "default" or "mini" available
    control: "default", //"default", "hidden" available
    updateInterval: 1000,
    onStart: {
      deviceName: "Espelho" // nome exibido no spotify
    }, // disable onStart feature with `null`
    deviceDisplay: "Ouvindo em:"
  }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

## RASPOTIFY

Por padrão o Spotify não será possível ouvir música direto do Raspberry. Desta forma, será necessário configurar o [Raspotify](https://github.com/dtcooper/raspotify), que irá conectar ao Sportify e reproduzir as músicas.

```
curl -sL https://dtcooper.github.io/raspotify/install.sh | sh
```

Após a instalação altere o arquivo de configurações:
```
nano /etc/default/raspotify
```

Altere a linha a baixo e substitua para o nome que seja que seja exibido no spotify:
```
# Device name on Spotify Connect
DEVICE_NAME="raspotify"
```

## Comando por voz

Adicione o arquivo "with-MMM-Spotify.js" nos recipes do MMM-AssistantMk2:
```
{
    module: "MMM-AssistantMk2",
    ...
    recipes: ["Reboot-Restart-Shutdown.js", "with-MMM-Spotify.js"]
    ...
}
```

Caso deseje alterar os comandos, edite o arquivo "with-MMM-Spotify.js" e altere o "pattern":
```
nano ~/MagicMirror/modules/MMM-AssistantMk2/recipes/with-MMM-Spotify.js
```

Ex:

```
  ...
  
  "SEARCH_SPOTIFY": {
    pattern: "tocar (.*) no spotify",
    command: "SEARCH_SPOTIFY"
  },
  "START_SPOTIFY" : {
    pattern : "spotify play",
    command: "START_SPOTIFY"
  },
  "STOP_SPOTIFY" : {
    pattern : "spotify parar",
    command: "STOP_SPOTIFY"
  },
  "PAUSE_SPOTIFY" : {
    pattern: "spotify pausar",
    command: "STOP_SPOTIFY"
  },
  "NEXT_SPOTIFY" : {
    pattern: "spotify seguinte",
    command: "NEXT_SPOTIFY"
  },
  "PREVIOUS_SPOTIFY": {
    pattern: "spotify anterior",
    command: "PREVIOUS_SPOTIFY"
  },
  "SHUFFLE_SPOTIFY": {
    pattern: "spotify surfar",
    command: "SHUFFLE_SPOTIFY"
  },
  "REPEAT_SPOTIFY": {
    pattern: "spotify repetir",
    command: "REPEAT_SPOTIFY"
  },
  "TRANSTO_SPOTIFY": {
    pattern: "spotify transferir para (.*)",
    command: "TRANSTO_SPOTIFY"
  },
  "VOLUME_SPOTIFY": {
    pattern: "spotify volume (.*)",
    command: "VOLUME_SPOTIFY"
  }
 ...   
```

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

## Atenção

Obs: Caso tenha algum erro relacionado a chamada do socket na inicialização do módulo altere o seguinte arquivos:

```
nano ~/MagicMirror/js/socketclient.js
```
Altere a linha:
```
self.socket = io("/" + self.moduleName, {
    path: window.location.pathname + "socket.io"
});
```
Para:
```
self.socket = io("/" + self.moduleName);
```

[Clique aqui](https://github.com/bugsounet/MMM-Spotify) para ver as opções do módulo.
