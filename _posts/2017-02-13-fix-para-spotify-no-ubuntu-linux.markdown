---
title: Fix para Spotify no Ubuntu Linux
layout: post
categories: tips
---
Companheiro diário em praticamente qualquer atividade na nossa vida, o **Spotify** é preferência para a maioria das pessoas que amam músicas.

A versão para linux ainda não é estável mas ainda podemos ter felicidade musical 24h por dia.

Um problema que vez por outra ocorre comigo, é o Spotify abrir em modo fullscreen escondendo a barra de opções, tornando inviável minimizar, arrastar e fechar, além de sobrepor sobre outras aplicações. E não adianta apertar f11, crtl+f ou qualquer comando que ative/remova o modo fullscreen.

Segue uma solução bem simples para esse problema no **Ubuntu Linux**. 

Com o **Spotify** fechado acesse a pasta <span class="text-featured">~/.config/spotify/window_position.prefs</span> e delete o arquivo <span class="text-featured">window_position.prefs</span>.

Após isso abra novamente seu Spotify e pronto, tudo funcionando corretamente.

Um jeito ainda melhor de fazer isso é criar um *alias* que acesse a pasta e apague o arquivo.

**Abra o arquivo de configuração do seu usuário como root:**<br>
`$ sudo nano ~/.bashrc`

**Adicione essa função**<br>
```function fixSpotify () {  
sudo killall spotify && echo "Spotify Killed" && \
sudo rm ~/.config/spotify/window_position.prefs && echo "Window preferences deleted" && \
sudo apt moo
}```

**Grave as informações no bash**<br>
`$ source ~/.bashrc`

**Quando o problema aparecer novamente execute no temrinal**<br>
`$ fixSpotify`

Não se preocupe pois nenhuma informação sua será perdida nesse processo, ok!

E caso queira acompanhar minhas playlists, fique a vontade para ver meu <a class="text-featured text-featured--link" href="https://open.spotify.com/user/rafaelnogueira1" target="_blank" title="Siga meu perfil no Spotify">perfil no Spotify</a>.