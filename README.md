# Monitoramento de Hardware no Linux (MangoHud + GOverlay)

**Foco:** Linux Mint / Ubuntu | **Hardware:** AMD/Intel/Nvidia
**Objetivo:** Ter métricas (FPS, Temp, VRAM) que iniciam escondidas e aparecem ao apertar um botão.

-----

### Passo 1: Instalar o Motor (MangoHud)

Vamos instalar a versão nativa do repositório. Ela é estável e permite que qualquer aplicativo (Steam, Lutris, AppImage) a enxergue sem barreiras.

Abra o terminal e rode:

```bash
sudo apt update && sudo apt install mangohud -y
```

-----

### Passo 2: Instalar a Interface (GOverlay via AppImage)

**Atenção:** Não use a versão da Loja (Flatpak) nem o `apt` para o GOverlay no Mint, pois faltam bibliotecas visuais (Qt6Pascal). A solução robusta é o **AppImage**.

1.  Crie uma pasta para organizar seus portáteis:
    ```bash
    mkdir -p ~/Apps
    ```
2.  Baixe a versão mais recente do **GOverlay AppImage** no GitHub:
      * [Link de Releases do GOverlay](https://github.com/benjamimgois/goverlay/releases)
      * *Baixe o arquivo terminado em `.AppImage`.*
3.  Mova para a pasta e dê permissão de execução:
    ```bash
    mv ~/Downloads/Goverlay*.AppImage ~/Apps/Goverlay.AppImage
    chmod +x ~/Apps/Goverlay.AppImage
    ```
4.  Execute:
    ```bash
    ~/Apps/Goverlay.AppImage
    ```

-----

### Passo 3: Configuração "Estilo Afterburner"

Com o GOverlay aberto, configure para ter o comportamento de "Ligar/Desligar":

1.  **Verificação:** Olhe no canto inferior esquerdo. Deve estar verde: **`All dependencies OK`**.
2.  **Global Enable:** Ligue a chave (Deixe Verde).
3.  Vá na aba **Visual**:
      * **Métricas:** Marque *CPU Temp, GPU Temp, GPU Load, VRAM, RAM, FPS, Frametime*.
      * **HUD Toggle Key:** Defina como `Shift_R+F12` (Shift Direito + F12).
          * *Dica de Eng.:* Evite teclas simples como F3 ou F12, pois jogos usam para funções internas.
      * **Hide HUD by default:** **MARQUE** esta caixa `[x]`. (Isso faz o jogo abrir limpo).
4.  Clique em **Save** (Botão verde).

-----

### Passo 4: Ativar na Steam (O Comando Universal)

Para garantir compatibilidade com jogos teimosos (Unreal Engine 5, jogos que reiniciam o driver gráfico), usaremos a Variável de Ambiente em vez do comando wrapper.

1.  Na Steam, clique com o botão direito no jogo \> **Propriedades**.
2.  Em **Opções de Inicialização** (Launch Options), cole:

<!-- end list -->

```bash
MANGOHUD=1 %command%
```

  * **Se usar Gamemode (Otimizador de CPU):**
    ```bash
    gamemoderun MANGOHUD=1 %command%
    ```

-----

### Passo 5: Ativar no Heroic / Lutris (Epic & GOG)

Esses launchers já têm integração nativa.

1.  Vá nas configurações do jogo dentro do Heroic.
2.  Marque a caixa **Enable MangoHud**.
3.  Pronto (ele vai ler a configuração que você salvou no GOverlay automaticamente).

-----

### Como usar

1.  Abra o jogo.
2.  Ele iniciará **sem métricas** na tela.
3.  Aperte **Shift Direito + F12** para monitorar a temperatura.
4.  Aperte novamente para esconder e imergir no jogo.
