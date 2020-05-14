# Currentweather 
Exibe o clima atual da sua cidade. Para isso será necessário configurar uma fonte que contenha informações climáticas. O próprio MagicMirror sugere utilizar o [OpenWeather](https://openweathermap.org/). Então, será necessário acessar o site e realizar o cadastro para obter um API_KEY, pois através dela será possível realizar consultas:

1. Acesse [OpenWeather](https://openweathermap.org/) e cadastre-se.
2. Clique em API.
3. Escolha a opção "Current Weather Data" clicando em "Subscribe".
4. Clique em: Free > Get API Key
5. Ao gerar a API clique em API keys e copie a chave gerada "key" e guarde.
6. Baixe o arquivo: http://bulk.openweathermap.org/sample/city.list.json.gz
7. Descompacte, abra e localize sua cidade e copie o código e guarde.
8. Altere o config.js:

```
nano ~/MagicMirror/config/config.js
```

9. Altere o trecho a seguir informando a sua cidade,  o código e a API KEY:
```
{
    module: "currentweather",
    position: "top_right", //POSIÇÃO NA TELA
    config: {
        location: "NOME_DA_SUA_CIDADE", //ALTERAR
        locationID: "CODIGO_DA_SUA_CIDADE", //ALTERAR
        appid: "API_KEY" //ALTERAR
    }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

[Clique aqui](https://docs.magicmirror.builders/modules/currentweather.html) para ver as opções do módulo Currentweather.

# Weatherforecast

O módulo weatherforecast é um módulo padrão do MagicMirror, assim como o Currentweather. Este módulo exibe as condições climáticas da sua cidade durante a semana. Por padrão o Weatherforecast também utiliza o [OpenWeather](https://openweathermap.org/), então caso ainda não tenha uma API_KEY, realize os passo acima.

- Altere o trecho a seguir informando a sua cidade, o código e a API KEY:

```
{
    module: "weatherforecast",
    position: "top_right", //POSIÇÃO NA TELA
    header: "Clima/Tempo", //TEXTO QUE SERÁ EXIBIDO NO MAGICMIRROR
    config: {
        location: "NOME_DA_SUA_CIDADE",
        locationID: "CODIGO_DA_SUA_CIDADE", //ALTERAR
        appid: "API_KEY" //ALTERAR
    }
},
```

Salve o arquivo "CTRL + O" e feche-o "CTRL + X".

[Clique aqui](https://docs.magicmirror.builders/modules/weatherforecast.html) para ver as opções do módulo Weatherforecast.