# MMM-AssistantMk2

Este módulo é um dos principais do projeto, pois ele irá embarcar o Google Assistente no MagicMirror.

## Instalando o Módulo

```
cd ~/MagicMirror/modules

git clone https://github.com/bugsounet/MMM-AssistantMk2

cd MMM-AssistantMk2

npm install
```

- Siga todos os passos da instalação, ao final será questionado para se utiliza o MMM-Hotword ou o MMM-Snowboy, escolha o MMM-Snowboy e siga todas as instruções.

## Configurar o Google Assistant

Para configurar o Google Assistant serão necessários seguir vários passos. É importante que siga na orgem para evitar problemas.

1. Crie um projeto em [Actions Console](https://console.actions.google.com/)
2. Ative o Google Assistant API para o seu projeto em [Cloud Platform Console](https://console.cloud.google.com/). 
    * Selecione o projeto na barra superior;
    * Acesse: (API e Serviços > Ativar Apis e Serviços);
    * Busque por "Google Assistant API" e ative.
3. Retorne para [Actions Console](https://console.actions.google.com/) e siga as instruções conforme documentação: [Register the Device Model](https://developers.google.com/assistant/sdk/guides/service/python/embed/register-device)
    * Importante: Realize o download da credencial e salve do diretório do módulo MMM-AssistantMk2, com o nome credentials.json.
    * Caso não encontre acesse: [Cloud Platform Console](https://console.cloud.google.com/) (Seu projeto > APIs & Serviços > Credenciais).

4. Acesse o terminal (não por SSH)
```
cd ~/MagicMirror/modules/MMM-AssistantMk2
node auth_and_test.js
```
  * Se tiver algum erro relacionado a versão do node, execute: npm rebuild.
  * Após a execução será exibido um link e abrirá o browser (caso não abra, copie o link e abra em um browser no próprio raspberry e não feche o terminal);
  * Acesse sua conta e dê permissão ao projeto, após isso será gerado um token, copie e cole no terminal e pressione enter;
  * Se tudo deu certo será solicitado para fazer uma pergunta, então informe: "Hello, How is the weather today?", se deu a responsta correta, está tudo funcionando.
  * No diretório do módulo MMM-AssistantMk2 foi gerado um arquivo token.json, copie para o diretório profiles da seguinte forma:

```
mv token.json ./profiles/default.json.js
```
  * Caso queira adicionar mais um profile, faça os passos anteriores para a outra conda do google que deseja adicionar e copie o token para pasta profile com outro nome, por ex:
```
mv token.json ./profiles/mom.json
```

## MMM-Snowboy

O [MMM-Snowboy](https://github.com/bugsounet/MMM-Snowboy) será responsável por ativar o Google Assistant a partir de um comando de voz, que já vem integrado ao MMM-AssistantMk2. Atualmente ele atende os seguintes comandos:

* smart_mirror: 0.5
* jarvis: 0.7
* computer: 0.6
* snowboy: 0.5
* subex: 0.6
* neo_ya: 0.7
* hey_extreme: 0.6
* view_glass: 0.7
* alexa: 0.6

Escolha qual será a palavra de ativação e informe abaixo nas configurações do módulo MMM-AssistantMk2.

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
    module: "MMM-AssistantMk2",
    position: "top_center",
    config: {
    debug: false,
    ui: "Simple",
    assistantConfig: {
        latitude: -5.7781622, //LATITUDE DA SUA LOCALIZAÇÃO
        longitude: -35.203284, //LONGITUDE DA SUA LOCALIZAÇÃO
    },
    micConfig: {
        recorder: "arecord",
        device: "plughw:1",
    },
    //OS RECIPES SÃO EXTENSÕES PARA PODER EXECUTAR
    //UM COMANDO BASEADO EM UM PADRÃO QUANDO FALADO
    recipes: ["Reboot-Restart-Shutdown.js"]
    profiles: {
        "default": {
        profileFile: "default.json",
        lang: "pt-BR"
        }
    },
    useA2D: true,
    A2DStopCommand: "stop",
    useSnowboy: true,
    snowboy: {
        audioGain: 2.0,
        Frontend: true,
        Model: "alexa",
        Sensitivity: 0.6 //Copie a numeração ao lado da palavra nas configurações do MMM-Snowboy
    },
    }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```
- Ative o Google Assistant falando a palavra que configurou no snowboy e pergunte "Que horas são?"

- Obs: O Google Assistant seguirá o idioma das suas preferências da conta. Caso você informe que fala mais de uma língua, ele irá reconhecer.

## Comandos Customizados

Caso queira configurar algum comando que o Google Assistant não suporte ou integrar com outro módulo através de notificações, é possível definir os [recipes](https://github.com/bugsounet/MMM-AssistantMk2/wiki/Recipes), nele será possível configurar um padrão quando for falado disparar um comando ou notificação.

* Por padrão o MMM-AssistantMk2 já possui alguns recipes pré-definidos:
```
cd ~/MagicMirror/modules/MMM-AssistantMk2/recipes
```
* Você pode editar o "pattern" (será o comando que irá falar).
* No exemplo abaixo eu editei o Reboot-Restart-Shutdown.js para atender os comandos em português e adicionei dois novos comandos para desligar e ligar o monitor:

```
...
transcriptionHooks: {
    "AMK2_REBOOT": {
      pattern: "reiniciar espelho",
      command: "AMK2_REBOOT"
    },
    "AMK2_RESTART": {
      pattern: "recarregar espelho",
      command: "AMK2_RESTART"
    },
    "AMK2_SHUTDOWN": {
      pattern: "desligar espelho",
      command: "AMK2_SHUTDOWN"
    },
    "AMK2_MONITOR_OFF": {
      pattern: "desligar monitor",
      command: "AMK2_MONITOR_OFF"
    },
    "AMK2_MONITOR_ON": {
      pattern: "ligar monitor",
      command: "AMK2_MONITOR_ON"
    },
  },

commands: {
 ...

 "AMK2_MONITOR_OFF": {
      soundExec: {
        chime: "close",
      },
      shellExec: {
        exec: "vcgencmd display_power 0"
      }, 
    },
    "AMK2_MONITOR_ON": {
      soundExec: {
        chime: "open",
      },
      shellExec: {
        exec: "vcgencmd display_power 1"
      }, 
    },
...    

```

* Caso queira usar algum recipe é necessário adicionar no config.js o nome do arquivo do recipe que deseja utilizar:
```
{
    module: "MMM-AssistantMk2",
    ...
    recipes: ["Reboot-Restart-Shutdown.js"]
    ...
}
```