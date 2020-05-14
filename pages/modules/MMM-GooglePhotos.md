# MMM-GooglePhotos

Este módulo permitirar exibir fotos da sua conta do Google Photos. Além disso, irá funcionar integrado com [MMM-Selfieshot](/pages/modules/MMM-Selfieshot.md) e irá fazer upload automáticamente das fotos tiradas por Selfie.

## Instalando o Módulo

```
git clone https://github.com/eouia/MMM-GooglePhotos.git
cd MMM-GooglePhotos
npm instal
```

## Permissão ao Google Photos

- Mesmo passos realizados em [MMM-AssistantMk2](/pages/modules/MMM-AssistantMk2.md) em "Configurar o Google Assistant":
  * Acesse: (API e Serviços > Ativar Apis e Serviços);
  * Busque por "Google Photos API" e ative.
  * Realize o download da credencial e salve do diretório do módulo MMM-GooglePhotos, com o nome credentials.json.
  * Caso não encontre acesse: [Cloud Platform Console](https://console.cloud.google.com/) (Seu projeto > APIs & Serviços > Credenciais).
  * Copie também o token.json do diretório MMM-AssistantMk2 para MMM-GooglePhotos
  ```
    cp ~/MagicMirror/modules/MMM-AssistantMk2/token.json ~/MagicMirror/modules/MMM-GooglePhotos/
  ```  

## Configurando o Módulo no MagicMirror

Para criar o album automáticamente no Google Photos execute:

```
node create_uploadable_album.js MyMagicMirrorAlbum
```

```
nano ~/MagicMirror/config/config.js
```

Adicione o módulo no final:
```
{
  module: "MMM-GooglePhotos",
  position: "bottom_center",
  config: {
  albums: [], // Set your album name. like ["My wedding", "family share", "Travle to Paris"]
  updateInterval: 1000 * 60, // minimum 10 seconds.
  sort: "random", // "old", "random"
  uploadAlbum: 'MyMagicMirrorAlbum', // Only album created by `create_uploadable_album.js`.
  //	condition: {
  //		fromDate: null, // Or "2018-03", RFC ... format available
  //		toDate: null, // Or "2019-12-25",
  //		minWidth: null, // Or 400
  //		maxWidth: null, // Or 8000
  //		minHeight: null, // Or 400
  //		maxHeight: null, // Or 8000
  //		minWHRatio: null,
  //		maxWHRatio: null,
  //		// WHRatio = Width/Height ratio ( ==1 : Squared Photo,   < 1 : Portraited Photo, > 1 : Landscaped Photo)
  //	},
  showWidth: 800, // These values will be used for quality of downloaded photos to show. real size to show in your MagicMirror region is recommended.
  showHeight: 600,
  timeFormat: "DD/MM/YYYY HH:mm", // Or `relative` can be used.
  }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

- Se tudo funcionou bem, reinicie o MagicMirror:
```
pm2 mm restart
```

[Clique aqui](https://github.com/eouia/MMM-GooglePhotos) para ver as opções do módulo.
