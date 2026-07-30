+++
title = "Projetos"
slug = "projects"
+++

Aqui estão alguns dos projetos em que tenho trabalhado. Todos bare-metal, todos do zero.

---

### [Galeria de Hardware →]({{< ref "projects/hardware" >}})

Fotos de placas, protótipos e setups de debug que projetei e construí. Do esquemático ao hardware funcionando.

---

### [Blinky to Bootloader](https://github.com/slemanz/blinky-to-bootloader)

![O projeto rodando em uma STM32F411 black pill, com o LED, o ST-Link e a fiação da UART na protoboard](/images/blinky-to-bootloader.png)

O que começou como um simples LED piscando evoluiu para uma aplicação completa no STM32F411 com arquitetura de 5 camadas e bootloader via UART para atualização de firmware. Tudo bare-metal, tudo Makefile.

**Stack:** C, ARM Cortex-M4, STM32F411, Makefile, Python (ferramenta DFU)

---

### [RA4M1 Sandbox](https://github.com/slemanz/RA4M1-sandbox)

Ambiente de desenvolvimento bare-metal para o Renesas RA4M1 (Arduino UNO R4 Minima). Sem framework Arduino, sem CMSIS: manipulação direta de registradores, debug com J-Link, separação limpa de camadas.

**Stack:** C, Renesas RA4M1, Makefile, J-Link/Ozone

---

### [Nina Project](https://github.com/slemanz/nina-project)

Hardware e firmware para um dispositivo de aquisição de dados baseado no u-blox NINA-B306 (nRF52840). Ciclo completo de desenvolvimento, do esquemático à placa funcionando com firmware.

**Stack:** C, nRF52840, KiCad, Makefile

---

### [Advanced Embedded C](https://github.com/slemanz/advanced-embedded-c)

Repositório de estudo cobrindo design patterns, padrões otimizados, estruturas de dados, build systems, bootloader, safety, tratamento de falhas e TDD, tudo aplicado a C embarcado.

**Tópicos:** Design Patterns, FSM, TDD, Build Systems

---

### [Design Pattern Dump](https://github.com/slemanz/design-pattern-dump)

Implementações práticas de design patterns e máquinas de estado finitas para sistemas embarcados em C, rodando em hardware real.

**Stack:** C, STM32, Makefile

---

### [F411 Sandbox](https://github.com/slemanz/F411-sandbox)

Sandbox de desenvolvimento ativo para o STM32F411, onde testo novos drivers, periféricos e ideias antes de integrar em projetos maiores.

**Stack:** C, STM32F411, Makefile

---

Mais projetos no meu [GitHub](https://github.com/slemanz).
