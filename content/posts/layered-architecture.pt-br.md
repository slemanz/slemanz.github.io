+++
authors = ["William Sleman"]
title = "Como Estruturo Meus Projetos Embarcados"
date = "2026-03-15"
description = "Um olhar prático sobre a arquitetura de 5 camadas que uso em firmware bare-metal."
tags = [
    "embarcados",
    "arquitetura",
    "firmware",
    "C",
]
categories = [
    "sistemas embarcados",
]
+++

Todo projeto de firmware que começo segue a mesma estrutura. Não porque sou rígido, mas porque depois de projetos suficientes, você aprende que uma arquitetura limpa te economiza mais tempo do que custa.

<!--more-->

## O problema

A maioria dos projetos embarcados começa pequena. Um único `main.c`, algumas escritas em registradores, um LED piscando. Mas aí as features vão aparecendo: comunicação UART, uma interrupção de timer, uma leitura de ADC, um parser de protocolo. Quando você percebe, seu arquivo de 200 linhas tem 2000 e tudo depende de tudo.

Já estive nessa situação. E a solução que adotei é uma **arquitetura de 5 camadas**:

```
┌────────────────┐
│      APP       │
├────────────────┤
│     COMMON     │
├────────────────┤
│   INTERFACE    │
├────────────────┤
│    DRIVERS     │
├────────────────┤
│    HARDWARE    │
└────────────────┘
```

## As camadas

**App**: a lógica da aplicação. É a única camada que sabe o que o produto *faz*. Ela chama a camada common para serviços, mas nunca toca um registrador diretamente.

**Common**: serviços compartilhados como protocolos de comunicação, BSP (Board Support Package) e utilitários. Essa camada fornece APIs abstratas que a app consome.

**Interface**: a ponte entre Common e Drivers. É o que torna possível trocar de microcontrolador sem reescrever o projeto inteiro. A interface define *o que* precisa acontecer; os drivers definem *como*.

**Drivers**: implementações específicas do hardware. Todo o código a nível de registrador fica aqui: GPIO, UART, SPI, timers. É a camada que lê datasheets.

**Hardware**: o MCU físico e seus periféricos. Não é código, mas é a coisa com a qual seu código conversa.

## Por que funciona

O ponto principal é que **cada camada só conversa com a camada diretamente abaixo**. A app nunca chama uma função de driver. Um driver nunca inclui um header da app. Isso torna cada camada independentemente testável e substituível.

Quando portei meu projeto [Blinky to Bootloader](https://github.com/slemanz/blinky-to-bootloader) para um MCU diferente, só precisei reescrever a camada de Drivers. Tudo acima (a lógica do bootloader, o protocolo UART, o processo de DFU) ficou exatamente igual.

Esse é o retorno. Os 30 minutos extras que você gasta configurando a estrutura te economizam dias quando o projeto cresce.
