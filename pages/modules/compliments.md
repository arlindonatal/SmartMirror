# Compliments

Este módulo irá exibir de forma aleatória cumprimentos de saudações conforme o horário. Para configurar os cumprimentos é necessário alterar o arquivo:

```
nano ~/MagicMirror/modules/default/compliments/compliments.js
```
```
...
compliments:
        anytime: [
                "Ola!"
        ],
        morning: [
                "Bom dia!",
                "Tenha um bom dia!",
                "Dormiu bem?"
        ],
        afternoon: [
                "Oi, boa tarde!",
                "Oi!",
                "Tenha um bom dia!"
        ],
        evening: [
                "Ola, boa noite!",
                "Espero que seu dia tenha sido bom!",
                "Boa noite!"
        ],
        "....-01-01": [
                "Feliz ano novo!"
        ]
},
...
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

[Clique aqui](https://docs.magicmirror.builders/modules/compliments.html) para ver as opções do módulo compliments.