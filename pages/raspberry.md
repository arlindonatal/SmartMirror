# Raspberry
 
  ![Raspberry](/img/raspberry3.png?raw=true "Raspberry")

 O Raspberry Pi é um mini computador, que permite rodar pequenos programas em Python ou Java, baseado em Linux. Neste tutorial vou explicar como configurar o Raspberry Pi instalando o Raspbian que é o SO baseado no Debian (linux).

 # Preparando o cartão SD

- Em um outro computador, formate o cartão de memória em FAT ou FAT32. Utilize o [SD Formatter](https://www.sdcard.org/downloads/formatter/) ou outro software de sua preferência.

- Acesse o site do [Raspberry Pi](www.raspberrypi.org) em Download escolha a opção Raspbian e faça o download da imagem.

- Baixe o [Etcher](https://www.balena.io/etcher/) e use-o para copiar a imagem para o SD.

- Após finalizar a copia da imagem, plugue o SD no Raspberry e ligue para iniciar o SO. (Conecte o mouse, teclado e o monitor HDMI).

# Configuração

- Ao iniciar o sistema, acesse o terminal e digite os seguintes comandos abaixo para atualizar os pacotes/dependências:

```
sudo apt-get update
sudo apt-get upgrade
sudo rpi-update
```

## Acesso remoto (opcional)
- Acessar via VNC ou SSH (é opcional, caso contrário ignore esse passo e continue direto no raspberry):
```
sudo raspi-config
```
- 5 Interfacing Options > SSH (ativa o acesso SSH) e VNC (acesso ao client remoto VNC).
- Descubra o ip do raspberry acessando if-config para poder acessar pelo VNC ou SSH.
- SSH (caso não alterou a senha padrão é "raspberry"):
```
ssh pi@IP-DO-RASPBERRY
```
- VNC: Baixar o [VNC Viewer](https://www.realvnc.com/pt/connect/download/viewer/) e acessa com ip do raspberry, usuario: "pi" e senha: "raspberry".

## Instalação de pacotes necessários
```
sudo apt-get install git xinit libxss1 libnss3 xinit xserver-xorg lxde-core lightdm -y
```

## Esconder cursor do mouse: (opcional)
```
sudo apt-get install unclutter
```

## Alterar boot: (opcional)
```
sudo raspi-config
```
- Acesse a opção "Boot Options" e altere para "Desktop" or "Desktop Autologin"