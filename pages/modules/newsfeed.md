#News Feed

O módulo newsfeed é um módulo padrão do MagicMirror. Este módulo exibe notícias baseado em um RSS feed.

- Para configurar para exibir o feed de notícias de sua preferência altere o config.js:

```
nano ~/MagicMirror/config/config.js
```

- Altere o trecho a seguir informando a url do feed RSS:
```
{
    module: "newsfeed",
    position: "bottom_bar",
    config: {
        feeds: [
            {
                title: "Noticias Brasil",
                url: "https://g1.globo.com/rss/g1/brasil" //ALTERAR AQUI O FEED
            }
        ],
        showSourceTitle: true,
        showPublishDate: true,
        broadcastNewsFeeds: true,
        broadcastNewsUpdates: true
    }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

[Clique aqui](https://docs.magicmirror.builders/modules/newsfeed.html) para ver as opções do módulo.
