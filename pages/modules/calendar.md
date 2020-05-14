# Calendar

Este módulo exibe o calendário baseado em uma fonte [ICS](https://en.wikipedia.org/wiki/ICalendar) que é uma padronização para armazenar o calendário de forma dinâmica e poder servir para outras fontes.

## Configurando a Fonte do Calendário

Nas configurações originais o calendário exibirá os feriados dos EUA. Para configurar para retornar os feriados do Brasil será necessário alterar o arquivo config.js do MagicMirror:

```
nano ~/MagicMirror/config/config.js
```

Altere a url para: http://www.supercalendario.com.br/ics/2020:
```
{
    module: "calendar",
    header: "Agenda",
    position: "top_left",
    config: {
        calendars: [
            {
                symbol: "calendar-check",
                url: "http://www.supercalendario.com.br/ics/2020"
            }
        ]
    },
}
```

É possível também integrar com sua agenda do google. Para isso será necessário acessar [Google Calendar](https://calendar.google.com/) e seguir os passos abaixo:

1. Clicar na agenda que deseja exibir.
2. Integrar Agenda.
3. Copiar: Endereço secreto no formato iCal (não compartilhar com ninguem esse link, pois terá acesso a sua agenda).
4. Adicionar no aquivo config.js:
```
{
    module: "calendar",
    header: "Agenda",
    position: "top_left",
    config: {
        calendars: [
            {
                symbol: "calendar-check",
                url: "http://www.supercalendario.com.br/ics/2020"
            },
            {
                symbol: "minha-agenda-google",
                url: "LINK_AGENDA_GOOGLE" //alterar pelo ics da agenda do google
            },
        ]
    },
}
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".


[Clique aqui](https://docs.magicmirror.builders/modules/calendar.html) para ver as opções do módulo calendar.
