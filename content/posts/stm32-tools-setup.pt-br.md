+++
authors = ["William Sleman"]
title = "Instalando as Ferramentas para Desenvolvimento Bare-Metal com STM32"
date = "2026-11-12"
draft = false
description = "Instalação passo a passo de todas as ferramentas do curso STM32 Embedded Fundamentals, no Windows e no Linux."
tags = [
    "firmware",
]
categories = [
    "sistemas embarcados",
]
+++

Este é o guia de instalação do meu curso **STM32 Embedded Fundamentals**. Ele cobre todas
as ferramentas que usamos, no Windows e no Linux, e como conferir que cada uma funciona.

<!--more-->

Mantenho esta página atualizada. Se alguma página de download mudou e algo aqui não bate,
me avise (link de contato no topo) que eu corrijo.

{{< notice info >}}
O curso é em inglês, então mantive em inglês os termos que você vai ver nas aulas e nas
ferramentas: PATH, toolchain, build, probe, firmware. Os nomes de menus do Windows estão
como aparecem num Windows em português.
{{< /notice >}}

## O que você vai instalar

| # | Ferramenta | Para que serve |
|---|------------|----------------|
| 1 | Git (Git Bash no Windows) | Um terminal com os mesmos comandos no Windows e no Linux |
| 2 | GCC | Compila C para o seu PC |
| 3 | Make | Roda o build |
| 4 | Arm GNU Toolchain 12.3.Rel1 | Compila C para o chip (`arm-none-eabi-gcc`) |
| 5 | Python | Scripts auxiliares usados mais adiante no curso |
| 6 | VS Code | O editor (qualquer editor serve) |
| 7 | PuTTY | Terminal serial |
| 8 | STM32CubeProgrammer | Driver USB do ST-Link e atualização de firmware do probe (só Windows) |
| 9 | J-Link Software | Só se você tiver um J-Link |
| 10 | OpenOCD | Grava o chip, com o ST-Link ou com o J-Link |

**Já tem alguma dessas ferramentas?** Uma IDE, por exemplo, muitas vezes já instala o GCC
ou o Make. Se você já tem a ferramenta e a versão é a mesma listada aqui ou mais nova, pode
pular. Se depois aparecer um erro muito diferente do que aparece nos vídeos, instale a mesma
versão que eu uso e tente de novo. Erro faz parte do aprendizado, e se você resolver um por
conta própria, aprendeu mais do que a aula ensinava.

## Duas ideias antes de começar

**O PATH.** É uma lista de pastas. Quando você digita um comando, o terminal procura o
programa em cada uma dessas pastas. Se ele não estiver em nenhuma, você recebe
`command not found`. Para a maioria das ferramentas abaixo, você adiciona a pasta `bin`
da ferramenta ao PATH.

**Reabra o terminal.** Um terminal que já estava aberto não enxerga o PATH novo. Depois de
cada mudança no PATH, feche o terminal e abra outro.

---

## Windows

O padrão para todas as ferramentas: baixar → extrair ou instalar → adicionar a pasta `bin`
ao PATH → fechar e reabrir o Git Bash → conferir com `--version`.

Ferramentas pequenas vão em `C:\tools`. **Nada de espaços no caminho**: algumas ferramentas
de build quebram com `C:\Program Files\...`.

### Como editar o PATH no Windows

Você vai fazer isso várias vezes, sempre do mesmo jeito:

1. Menu Iniciar → digite `variáveis` → abra **Editar as variáveis de ambiente do sistema**.
2. Clique em **Variáveis de Ambiente…**.
3. Em **Variáveis de usuário**, selecione **Path** → **Editar**.
4. **Novo** → cole a pasta → **OK** → **OK** → **OK**.
5. Feche o Git Bash e abra de novo.

![A janela "Editar a variável de ambiente": as pastas do curso no topo, e o botão Novo](/images/stm32-tools/win-path-edit.png)

### 1. Git for Windows (Git Bash)

1. Vá em [git-scm.com](https://git-scm.com/) → **Download for Windows** → instalador 64-bit.
2. Rode o instalador. Os padrões estão bons, exceto:
   - **Select Components**: se aparecer **Add a Git Bash Profile to Windows Terminal**,
     marque.
   - **Choosing the default editor used by Git**: escolha **Notepad** (o padrão é o Vim,
     que é difícil de sair se você nunca usou).

**Abra o Git Bash dentro do Windows Terminal.** O Windows Terminal tem fonte melhor, abas e
copiar/colar fácil. Ele já vem no Windows 11; no Windows 10, instale pela Microsoft Store.

1. Abra o **Terminal** → **Configurações** (`Ctrl+,`) → **Inicialização**.
2. **Perfil padrão**: **Git Bash** → **Salvar**.
3. Feche e reabra o Terminal: agora ele já abre no Git Bash. Fixe na barra de tarefas.

Daqui para frente, "Git Bash" quer dizer esta janela.

```bash
git --version
```

### 2. GCC (MinGW-w64 8.1.0)

1. Baixe
   [x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z/download).
2. Extraia em `C:\`. Você fica com `C:\mingw64\bin\gcc.exe`.
   O Windows 11 recente abre `.7z` direto; senão, instale o [7-Zip](https://www.7-zip.org/).
3. Adicione `C:\mingw64\bin` ao PATH e reabra o Git Bash.

{{< notice warning >}}
Não use o botão verde grande "Download Latest Version" da página do projeto MinGW-w64:
aquilo é o código-fonte, não o compilador.
{{< /notice >}}

```bash
gcc --version     # gcc.exe (x86_64-posix-seh-rev0, Built by MinGW-W64 project) 8.1.0
```

### 3. Make (GnuWin32 3.81)

1. Vá em [gnuwin32.sourceforge.net/packages/make.htm](https://gnuwin32.sourceforge.net/packages/make.htm).
2. Na linha **Complete package, except sources**, clique em **Setup** e rode o instalador
   com os padrões.
3. Adicione `C:\Program Files (x86)\GnuWin32\bin` ao PATH e reabra o Git Bash.

Use o Setup, não o zip só com os binários: falta DLL nele e o `make` não abre. O espaço em
`Program Files` não atrapalha aqui, porque ele só aparece no PATH; nossos Makefiles nunca
apontam para essa pasta.

```bash
make --version    # GNU Make 3.81
```

### 4. Arm GNU Toolchain 12.3.Rel1

1. Baixe
   [arm-gnu-toolchain-12.3.rel1-mingw-w64-i686-arm-none-eabi.zip](https://developer.arm.com/-/media/Files/downloads/gnu/12.3.rel1/binrel/arm-gnu-toolchain-12.3.rel1-mingw-w64-i686-arm-none-eabi.zip)
   (o zip, não o instalador `.exe`).
   Ele também está na [página de downloads da Arm](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads),
   em 12.3.Rel1 → Windows → AArch32 bare-metal target (arm-none-eabi).
2. Crie `C:\tools` e extraia o zip lá, para ficar assim:
   `C:\tools\arm-gnu-toolchain-12.3.rel1-mingw-w64-i686-arm-none-eabi\bin\arm-none-eabi-gcc.exe`.
   O zip já tem essa pasta dentro. No **Extrair Tudo…**, deixe o destino só como
   `C:\tools`: o Windows sugere uma pasta com o nome do zip, e você acaba com o nome
   repetido duas vezes.
3. Adicione essa pasta `bin` ao PATH e reabra o Git Bash.

```bash
arm-none-eabi-gcc --version   # arm-none-eabi-gcc (Arm GNU Toolchain 12.3.Rel1 (Build arm-12.35)) 12.3.1 20230626
```

### 5. Python

1. Vá em [python.org](https://www.python.org/downloads/) → baixe o Python 3 mais recente.
2. Na primeira tela do instalador, marque **Add python.exe to PATH** → **Install Now**.

![Primeira tela do instalador do Python, com "Add python.exe to PATH" marcado](/images/stm32-tools/win-python-path.png)

A caixa vem **desmarcada**. Não pule.

```bash
python --version
```

{{< notice tip >}}
Se digitar `python` abrir a Microsoft Store, o Python não está no PATH. Procure por
**Gerenciar aliases de execução de aplicativo**, desligue as duas entradas do Python e rode
o instalador de novo com a caixa marcada.
{{< /notice >}}

### 6. VS Code

1. Vá em [code.visualstudio.com](https://code.visualstudio.com/) → **Download for Windows**
   (User Installer).
2. Em **Select Additional Tasks**, deixe **Add to PATH** marcado.
3. Reabra o Git Bash e instale as extensões:

```bash
code --version
code --install-extension ms-vscode.cpptools
code --install-extension ms-python.python
code --list-extensions
```

Eu também uso a extensão do Vim (`vscodevim.vim`). Se você não conhece Vim, não instale:
ela muda o que cada tecla faz, e não faz parte do curso.

### 7. PuTTY

1. Vá em [putty.org](https://www.putty.org/) → página de download → **MSI (Windows Installer)**,
   64-bit x86 → instale com os padrões.
2. Abra pelo menu Iniciar e confira que **Connection type** tem a opção **Serial**.

Desta vez não tem PATH.

### 8. STM32CubeProgrammer (driver do ST-Link)

Não gravamos com ele no curso (quem faz isso é o OpenOCD), mas ele instala o driver USB do
ST-Link e consegue atualizar o firmware do probe, o que alguns clones precisam.

1. Vá em [st.com/en/development-tools/stm32cubeprog.html](https://www.st.com/en/development-tools/stm32cubeprog.html)
   → **Get Software** → **STM32CubePrg-Win64**. A ST pede uma conta gratuita ou um e-mail.
2. Descompacte e rode `SetupSTM32CubeProgrammer_win64.exe` com os padrões. Aceite a
   instalação do driver do ST-Link quando ele perguntar.
3. Adicione `C:\Program Files\STMicroelectronics\STM32Cube\STM32CubeProgrammer\bin` ao
   PATH e reabra o Git Bash. O instalador não faz isso por você: sem este passo, o
   `STM32_Programmer_CLI` dá `command not found` mesmo com o programa instalado.

```bash
STM32_Programmer_CLI --version   # STM32CubeProgrammer version: 2.23.0
```

### 9. J-Link Software (só se você tiver um J-Link)

1. Vá em [segger.com/downloads/jlink](https://www.segger.com/downloads/jlink/) →
   **J-Link Software and Documentation Pack** → instalador Windows 64-bit → padrões.
2. Adicione `C:\Program Files\SEGGER\JLink_V<versão>` ao PATH (por exemplo
   `JLink_V844a`) e reabra o Git Bash.

```bash
JLink.exe
```

Ele mostra a versão (`SEGGER J-Link Commander V8.44a` ou mais nova) e, sem probe
conectado, `Cannot connect to J-Link`. É o esperado. Digite `exit`.

### 10. OpenOCD (xPack 0.12.0-7)

1. Vá em [github.com/xpack-dev-tools/openocd-xpack/releases](https://github.com/xpack-dev-tools/openocd-xpack/releases/tag/v0.12.0-7)
   → **Assets** → `xpack-openocd-0.12.0-7-win32-x64.zip`.
2. Extraia em `C:\tools`, para ficar com `C:\tools\xpack-openocd-0.12.0-7\bin\openocd.exe`.
3. Adicione `C:\tools\xpack-openocd-0.12.0-7\bin` ao PATH e reabra o Git Bash.

```bash
openocd --version   # xPack Open On-Chip Debugger 0.12.0+dev-02228-ge5888bda3-dirty (2025-10-04-22:44)
```

---

## Linux (Ubuntu)

A maioria das ferramentas vem do `apt`. O toolchain da Arm é instalado na mão, para você
ter exatamente a 12.3.Rel1. Abra um terminal (`Ctrl+Alt+T`) e vá uma ferramenta por vez.

### 1. Git

```bash
sudo apt update
sudo apt install git
git --version
```

### 2. GCC e Make

Os dois vêm no `build-essential`:

```bash
sudo apt install build-essential
gcc --version
make --version
```

### 3. Arm GNU Toolchain 12.3.Rel1

Baixe
[arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi.tar.xz](https://developer.arm.com/-/media/Files/downloads/gnu/12.3.rel1/binrel/arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi.tar.xz)
e extraia em `~/opt/tools`:

```bash
mkdir -p ~/opt/tools
cd ~/Downloads
tar xf arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi.tar.xz -C ~/opt/tools
ls ~/opt/tools/arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi/bin
```

Adicione a pasta `bin` dele ao PATH. No Linux, o PATH fica no `~/.bashrc`, que o bash lê
toda vez que um terminal abre:

```bash
nano ~/.bashrc
```

Adicione esta linha no final, salve (`Ctrl+O`, `Enter`) e saia (`Ctrl+X`):

```bash
export PATH="$HOME/opt/tools/arm-gnu-toolchain-12.3.rel1-x86_64-arm-none-eabi/bin:$PATH"
```

Feche o terminal, abra outro e confira:

```bash
arm-none-eabi-gcc --version
```

### 4. Python

O Python 3 já vem no Ubuntu. Instale o pip:

```bash
sudo apt install python3-pip
python3 --version
```

No Linux o comando é `python3`, não `python`.

### 5. VS Code

Baixe o `.deb` em [code.visualstudio.com](https://code.visualstudio.com/) e depois:

```bash
cd ~/Downloads
sudo apt install ./code_*.deb
code --version
code --install-extension ms-vscode.cpptools
code --install-extension ms-python.python
```

### 6. PuTTY

```bash
sudo apt install putty
sudo usermod -aG dialout $USER
```

A porta serial pertence ao grupo `dialout`. O segundo comando coloca o seu usuário nele;
só vale depois que você **sair da sessão e entrar de novo** (logout/login).

### 7. ST-Link

Nada a instalar: o OpenOCD conversa direto com o ST-Link.

### 8. J-Link Software (só se você tiver um J-Link)

Baixe o **Linux 64-bit DEB installer** em
[segger.com/downloads/jlink](https://www.segger.com/downloads/jlink/) e depois:

```bash
cd ~/Downloads
sudo apt install ./JLink_Linux_*_x86_64.deb
JLinkExe
```

Digite `exit` para sair. O pacote também instala as regras udev, então o J-Link funciona
sem `sudo`.

### 9. OpenOCD

```bash
sudo apt install openocd
openocd --version
```

O pacote instala as regras udev dos probes, então você grava sem `sudo`. A versão 0.11 ou
mais nova serve para o curso (o Ubuntu 22.04 traz a 0.11, o 24.04 traz a 0.12).

---

## Git: chave SSH para o GitHub

Você não precisa de conta para baixar os exemplos do curso, mas para dar push no seu
próprio trabalho no GitHub você precisa provar quem é. Uma chave SSH resolve isso uma vez,
e você nunca mais digita senha. Os comandos são os mesmos no Git Bash e no Linux.

**1. Diga ao Git quem você é** (isso vai em todo commit):

```bash
git config --global user.name "Seu Nome"
git config --global user.email "voce@exemplo.com"
```

**2. Crie a chave.** Use o mesmo e-mail da sua conta do GitHub. Aperte `Enter` para aceitar
o arquivo padrão e depois digite uma passphrase (ou deixe vazia):

```bash
ssh-keygen -t ed25519 -C "voce@exemplo.com"
```

Isso cria dois arquivos em `~/.ssh/`: `id_ed25519` é a chave **privada** (nunca
compartilhe) e `id_ed25519.pub` é a chave **pública**, a que você entrega ao GitHub.

**3. Copie a chave pública:**

```bash
cat ~/.ssh/id_ed25519.pub
```

Selecione a linha inteira (começa com `ssh-ed25519`) e copie.

**4. Adicione no GitHub:** **Settings** → **SSH and GPG keys** → **New SSH key** → cole →
**Add SSH key**.

**5. Teste:**

```bash
ssh -T git@github.com
```

Na primeira vez ele pergunta `Are you sure you want to continue connecting?`: digite `yes`.
Você deve ver `Hi <seu-usuario>! You've successfully authenticated...`. Daqui para frente,
clone com a URL **SSH** (`git@github.com:...`), não com a HTTPS.

Mais detalhes (passphrase com `ssh-agent`, várias chaves, problemas comuns) no guia
oficial, em português: [Conectar ao GitHub com SSH](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh).

---

## Conferência final

Abra um terminal **novo** e rode tudo:

**Windows (Git Bash)**

```bash
git --version
gcc --version
make --version
arm-none-eabi-gcc --version
python --version
code --version
STM32_Programmer_CLI --version
openocd --version
```

**Linux**

```bash
git --version
gcc --version
make --version
arm-none-eabi-gcc --version
python3 --version
code --version
openocd --version
```

Além disso, o PuTTY (abre e tem **Serial**) e, se você tiver, o J-Link (`JLink.exe` /
`JLinkExe`, depois `exit`).

### O que você deve ver

| Ferramenta | Windows | Linux |
|------------|---------|-------|
| `arm-none-eabi-gcc` | 12.3.Rel1 | 12.3.Rel1 |
| `gcc` | 8.1.0 | a da sua distro (11.4.0 no Ubuntu 22.04) |
| `make` | 3.81 | a da sua distro (4.3 no Ubuntu 22.04) |
| `python` / `python3` | 3.x | 3.x |
| `openocd` | 0.12.0 (xPack) | 0.11 ou mais nova |
| `STM32_Programmer_CLI` | 2.x | — |

### Se algo der errado

- **`command not found`**: a pasta `bin` da ferramenta não está no PATH, ou o terminal já
  estava aberto quando você mudou o PATH. Confira a pasta, feche e reabra o terminal.
- **`python` abre a Microsoft Store**: veja a dica no passo 5.
- **Versão errada** (por exemplo, outro `arm-none-eabi-gcc` de uma instalação antiga):
  rode `which arm-none-eabi-gcc` para ver qual o terminal encontra primeiro.

Tudo mostrando versão? Você está pronto para a próxima aula.
