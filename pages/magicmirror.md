# MagicMirror
 
  ![MagicMirror](/img/magicmirror.png?raw=true "MagicMirror")

  MagicMirror² é uma plataforma de espelho inteligente modular de código aberto. Com uma lista crescente de módulos instaláveis, o MagicMirror² permite converter seu corredor ou espelho do banheiro em seu assistente pessoal. MagicMirror² foi criado pelo [criador do MagicMirror original](http://michaelteeuw.nl/tagged/magicmirror) com a incrível ajuda de uma crescente [comunidade de colaboradores](https://github.com/MichMich/MagicMirror/graphs/contributors).

## Pré-requisitos
- Raspberry Pi 2+ (com [raspbian instalado](/pages/raspberry.md))
- Node 10+ (caso não tenha instalado)

## Instalação

Abra o terminal se realize os passos a seguir.

### Node

1. Faça download do node 10x:
```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
```
2. Instale o nodejs:
```
sudo apt install -y nodejs
```

### MagicMirror
1. Faça o clone do repositório do gitHub do MagicMirror:
```
cd ~
git clone https://github.com/MichMich/MagicMirror
```

2. Acesse o diretório do MagicMirror:
```
cd MagicMirror/
```

3. Instale a aplicação:
```
npm install
```

4. Faça uma cópia do exemplo do arquivo de configuração:
```
cp config/config.js.sample config/config.js
```

5. Iniciar o MagicMirror:
```
npm run start
```

### Auto inicializar o MagicMirror

Para iniciar automaticamente o MagicMirror ao ligar seu Raspberry será necessário instalar o [PM2](https://pm2.keymetrics.io/).

1. Instalar o PM2:
```
sudo npm install -g pm2
```
2. Ativar inicialização no boot:
```
pm2 startup
```
3. Será exibido um comando para que seja executado, caso não exiba execute:
```
sudo su -c "env PATH=$PATH:/usr/bin pm2 startup linux -u pi --hp /home/pi"
```
4. Acesse o root:
```
cd ~
```
5. Crie o seguinte arquivo:
```
sudo nano mm.sh
```
6. Adicione as seguintes linhas no arquivo:
```
cd ~/MagicMirror
DISPLAY=:0 npm start
```
7. Salve pressionando CTRL-O e CTRL-X para sair
8. Dê permissão ao arquivo:
```
chmod +x mm.sh
```
9. Inicie o MagicMirror com o PM2
```
pm2 start mm.sh
```
10. Você pode inicializar ouvindo o arquivo de configurações, assim qualquer mudança que ocorrer no arquivo será recarregado (opcional):
```
pm2 start mm.sh --watch ~/MagicMirror/config/config.js
```
11. Salve as configurações no PM2
```
pm2 save
```
12. Reiniciar o Raspberry:
```
sudo reboot
```
