# ubuntu24-pos-intalacao
script basico de pos instalação para minha necessidade com duolingo, spotify e user filho bloqueado de redes sociais
Este repositório vai conter:

✅ O script pos_instalacao.sh com:

Instalação de apps (Chrome, Spotify, Duolingo Web, VLC, GIMP, LibreOffice, Calibre, Foliate)

Criação da conta filho com bloqueio de redes sociais

Ativação de Flatpak e repositórios

Leitores de livros com acesso a conteúdo gratuito


Segue abaixo o codigo:

#!/bin/bash

echo "🔄 Atualizando sistema..."
sudo apt update && sudo apt upgrade -y

echo "🌐 Instalando Google Chrome e Spotify..."
wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb -y
rm google-chrome-stable_current_amd64.deb
sudo snap install spotify

echo "📚 Instalando leitores de livros e apps úteis..."
sudo apt install -y \
  gimp \
  vlc \
  libreoffice \
  gnome-tweaks \
  git \
  curl \
  flatpak \
  timeshift \
  calibre \
  foliate \
  ubuntu-restricted-extras

echo "🧩 Ativando Flathub e instalando Duolingo via WebApp (Chrome)..."
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flathubrepo

mkdir -p ~/.local/share/applications
cat <<EOF > ~/.local/share/applications/duolingo.desktop
[Desktop Entry]
Name=Duolingo
Exec=google-chrome --app=https://www.duolingo.com
Icon=web-browser
Terminal=false
Type=Application
Categories=Education;
EOF

echo "👶 Criando conta restrita para seu filho..."
sudo adduser filho
sudo usermod -aG audio,video filho

echo "🚫 Bloqueando redes sociais para a conta filho..."
cat <<EOF | sudo tee -a /etc/hosts

# BLOQUEIOS PARA CONTA DO FILHO
127.0.0.1 facebook.com www.facebook.com
127.0.0.1 instagram.com www.instagram.com
127.0.0.1 tiktok.com www.tiktok.com
127.0.0.1 twitter.com www.twitter.com
127.0.0.1 discord.com www.discord.com
127.0.0.1 reddit.com www.reddit.com
127.0.0.1 pinterest.com www.pinterest.com
127.0.0.1 youtube.com www.youtube.com
EOF

sudo chattr +i /etc/hosts

echo "✅ Tudo finalizado! Reinicie para aplicar todos os efeitos.”



Pos copiar codigo:

**Como usar o script — abra o terminal e digite:

chmod +x pos_instalacao.sh

./pos_instalacao.sh



1. Explicação de cada parte:

Instalações padrão: Chrome, Spotify…

Criação de usuário filho e bloqueio via hosts


2. Dicas de pós-instalação:

Verificar se o contas funcionam

Como editar bloqueios no futuro (removendo o chattr)

Instalações opcionais: Steam, Discord, VSCode
**

