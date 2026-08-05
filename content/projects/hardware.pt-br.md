+++
title = "Galeria de Hardware"
slug = "hardware"
description = "Uma olhada em algumas das placas e protótipos que projetei e construí."
date = "2026-03-01"
build = {list = "never", render = "always"}
+++

Uma olhada em algumas das placas e protótipos que projetei e construí, do conceito no esquemático ao hardware funcionando.

Isso é o que mais gosto de fazer: ver algo sair de um esquemático na tela para uma placa física que realmente faz o que deveria fazer.

---

<!-- 
COMO ADICIONAR UMA NOVA PLACA AQUI:

1. Coloque as fotos em static/images/hardware/
   Exemplo: static/images/hardware/ecu-top.jpg

2. Copie o bloco "Nina Project" abaixo e troque o título,
   o caminho da imagem e a descrição.

3. Cada seção funciona bem com 1-3 fotos.
-->

### Nina Project: Dispositivo de Aquisição de Dados

![Render 3D da placa Nina, com o módulo u-blox NINA-B306, o header SWD, a porta micro-USB e o conector de expansão](/images/nina-project.png)

Projeto completo de hardware para um dispositivo de aquisição de dados baseado no u-blox NINA-B306 (nRF52840). Projetado no KiCad, do esquemático à placa final: regulação de potência, header de debug SWD, conectores USB e de expansão, tudo numa placa que cabe no bolso.

O firmware que roda nela está no [repositório do Nina Project](https://github.com/slemanz/nina-project).

---

### Mais placas em breve

Tem mais coisa na bancada: placas de aquisição de sensores, protótipos de ECU e os setups de debug por trás deles. As fotos entram aqui conforme cada uma fica pronta.

---

> *"O hardware é o instrumento; o firmware é a música."*

Quer ver o código por trás dessas placas? Volte para [Projetos](/pt-br/projects/) ou visite meu [GitHub](https://github.com/slemanz).
