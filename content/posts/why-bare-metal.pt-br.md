+++
authors = ["William Sleman"]
title = "Por Que Escrevo Firmware Bare-Metal"
date = "2026-03-01"
description = "Sobre escolher entender o hardware ao invés de se esconder dele."
tags = [
    "embarcados",
    "bare-metal",
    "firmware",
    "filosofia",
]
categories = [
    "sistemas embarcados",
]
+++

Existe uma frase que penso com frequência: *"Se você deseja fazer uma torta de maçã do zero, primeiro precisa inventar o universo."* É do Carl Sagan, e embora ele estivesse falando de cosmologia, acho que se aplica igualmente bem a sistemas embarcados.

<!--more-->

Quando comecei a trabalhar com microcontroladores, a primeira coisa que todos me disseram foi para usar uma HAL. Usar a IDE. Gerar o código. Clicar nos botões. E funciona. Não vou fingir que não funciona. Mas eu nunca senti que entendia o que estava acontecendo.

Então fui pelo outro caminho. Comecei a ler manuais de referência. Escrevi meu próprio código de startup. Configurei a árvore de clock manualmente. Configurei UART escrevendo diretamente nos registradores. Demorou mais, mas quando algo dava errado, eu sabia *exatamente* onde procurar.

É isso que o bare-metal tem de especial: não é sobre ser difícil pelo prazer de ser. É sobre remover as camadas entre você e o hardware para que você possa raciocinar sobre o que está acontecendo. Quando seu bootloader não pula para a aplicação, você precisa entender a tabela de vetores. Quando sua transferência DMA corrompe dados, você precisa saber sobre alinhamento de memória. Nenhuma abstração de HAL vai te ensinar isso.

Não sou contra frameworks ou HALs. Eles têm seu lugar, especialmente em ambientes de produção com prazos apertados. Mas acredito que para usá-los bem, primeiro você precisa entender o que eles estão fazendo por você. E a única forma de chegar lá é fazer você mesmo pelo menos uma vez.

Por isso a maioria dos meus projetos começa com um Makefile, um linker script e um arquivo `.c` em branco. Não porque gosto de sofrer, mas porque gosto de entender.
