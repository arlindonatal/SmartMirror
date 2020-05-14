# MMM-Volume

Este módulo é um auxiliar que irá permitir controlar o volume por comando de voz.

## Instalando o Módulo

```
cd ~/MagicMirror/modules
git clone https://github.com/eouia/MMM-Volume
```

## Configurando o Módulo no MagicMirror

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
  module: "MMM-Volume",
  position: "top_left", // It is meaningless. but you should set.
  config: {
    usePresetScript: "ALSA", // "ALSA" is supported by default.
    volumeOnStart: 100,
  }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

- Para ativar o comando fale: alterar volume para 10. A faixa de volume é de 0 a 10.


[Clique aqui](https://github.com/Anonym-tsk/MMM-Volume) para ver as opções do módulo.
