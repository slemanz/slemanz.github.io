+++
authors = ["William Sleman"]
title = "Sete Meses Depois de Me Formar"
date = "2026-03-19"
description = "Sobre o que acontece quando você para de estudar para provas e começa a estudar para si mesmo."
tags = [
    "carreira",
    "embarcados",
    "pessoal",
    "aprendizado",
]
categories = [
    "pessoal",
]
+++

Me formei em Engenharia Elétrica há sete meses. E acho que aprendi mais nesses sete meses do que em qualquer ano isolado da faculdade.

Isso não é uma crítica à universidade. Ela me deu a base, o vocabulário, a forma de pensar. Mas tem algo diferente em aprender quando ninguém está te dando nota. Quando não tem prova semana que vem. Quando o único motivo de você estar lendo um datasheet às 23h é porque você genuinamente quer entender como um controlador de DMA arbitra o acesso ao barramento.

<!--more-->

## A virada

Na faculdade, eu estudava pra passar. Não tenho orgulho disso, mas é honesto. Tinha matérias que eu amava (qualquer coisa relacionada a microcontroladores, projeto de circuitos, sistemas embarcados) e matérias que eu suportava. O sistema te recompensa por ser bom o suficiente em tudo, não por ir fundo nas coisas que importam pra você.

Depois de me formar, isso mudou. Não da noite pro dia, não dramaticamente. Mas aos poucos percebi que minhas noites estavam diferentes. Em vez de assistir algo esquecível, eu estava lendo manuais de referência. Em vez de temer a segunda-feira, eu estava animado pra voltar a um problema de firmware que vinha mastigando no fim de semana.

Comecei a jogar tudo que aprendia no GitHub. Não projetos polidos com READMEs perfeitos, apenas conhecimento bruto. Anotações de drivers, experimentos de arquitetura, implementações de design patterns, exercícios em assembly. Um dump do meu cérebro em forma de código. A ideia era simples: se eu consigo implementar, eu entendo. Se não consigo, não entendo. Sem me enganar.

## Os livros que mexeram comigo

Dois livros me acertaram mais do que eu esperava esse ano.

O primeiro foi *Talent is Overrated*. A ideia central é quase desconfortável: o que chamamos de talento é na maior parte resultado de prática deliberada. Não apenas fazer algo repetidamente, mas fazer com intenção, empurrar os limites do que você consegue fazer, receber feedback, ajustar. As pessoas que admiramos, as que parecem dotadas, geralmente só começaram antes e praticaram de forma mais inteligente.

Isso reconfigurou tudo pra mim. Eu costumava olhar pra engenheiros seniores que conseguiam debugar um problema de timing só pela forma de onda e pensar "nunca vou ser tão bom." Agora eu penso "eles fazem isso há quinze anos, e se eu praticar de forma deliberada, posso chegar lá também." Não é uma garantia. Mas é um caminho, e isso é suficiente.

O segundo foi *How Einstein Ruined Physics*. Apesar do título provocativo, é sobre o perigo da elegância teórica substituir a verdade experimental. Sobre como a física, depois de Einstein, ficou cada vez mais obcecada com frameworks matemáticos bonitos que ninguém conseguia testar. O livro argumenta que o entendimento real vem de se envolver com o mundo físico e bagunçado, não de construir teorias isoladas.

Isso ressoou em mim mais do que qualquer livro-texto de engenharia. Porque sistemas embarcados são o mundo físico e bagunçado. Seu código não roda numa abstração matemática. Roda em silício que tem drift de temperatura, em barramentos que têm atraso de propagação, em fontes de alimentação que têm ripple. Você não pode só teorizar sobre um bootloader. Tem que gravar, ver falhar, ler os registradores de fault e descobrir por que o offset da tabela de vetores estava errado.

Não quero ser o tipo de engenheiro que se esconde atrás de abstrações. Quero ser o tipo que entende o que tem por baixo.

## Como são os dias agora

Acordo, vou trabalhar, projeto ECUs e sensores, escrevo firmware, rodo testes. Volto pra casa, pro apartamento que divido com minha namorada, a pessoa que torna tudo isso sustentável. Ela é a razão pela qual consigo passar uma noite inteira mergulhado num manual de arquitetura ARM sem sentir que estou negligenciando o que importa. Porque ela *é* uma das coisas que importam, e está ali, vivendo as próprias paixões ao lado das minhas.

Tem algo sobre construir uma vida com alguém enquanto se constrói como engenheiro. As duas coisas se alimentam. Estabilidade em casa te dá energia pra empurrar no trabalho. Crescimento no trabalho te dá uma confiança que transborda pra todo o resto.

Depois do jantar, geralmente abro um terminal. Algumas noites estou escrevendo um driver pra um periférico que nunca usei. Outras estou refatorando algo que escrevi mês passado e que agora percebo que estava errado. Às vezes só leio: datasheets, application notes, código de outras pessoas.

E depois faço push pro GitHub. Não porque alguém está olhando. Mas porque colocar lá fora me obriga a ser honesto sobre se eu realmente entendi aquilo.

## A verdade desconfortável

Não estou onde quero estar. Nem perto. Tem engenheiros por aí que conseguem olhar um esquemático e ver na hora o caminho de ruído que eu não veria. Que escrevem um handler de interrupção que eu levaria três tentativas pra acertar. Que têm uma intuição sobre hardware que ainda estou desenvolvendo.

Mas sete meses atrás, eu não conseguia fazer metade do que faço agora. E daqui a sete meses, vou olhar pra hoje da mesma forma.

É isso que a prática deliberada tem de especial. O progresso é lento o suficiente pra você não perceber dia a dia. Mas quando você dá um zoom out e compara o código que escreveu em janeiro com o que escreve em março, a diferença é inegável.

## O que eu sei agora

A universidade me ensinou *o que* as coisas são. Esses sete meses estão me ensinando *por que* elas funcionam.

Sei que um bootloader não é mágica. É um pedaço de código que vive numa região protegida da flash, valida uma imagem e modifica a tabela de vetores antes de pular. Sei disso porque construí um.

Sei que uma arquitetura em camadas não é overhead acadêmico. É a diferença entre um projeto que escala e um que desaba sob o próprio peso. Sei disso porque já passei pelos dois.

Sei que ler o datasheet não é opcional. É o trabalho. O periférico não liga pras suas suposições. Ele faz exatamente o que o manual de referência diz que faz, e quando algo dá errado, a resposta sempre está lá.

E sei que nada disso veio de talento. Veio de sentar, todo dia, e fazer o trabalho.

---

Sete meses. Não é muito tempo. Mas é tempo suficiente pra saber que estou no caminho certo.

Não porque alguém me disse. Porque eu sinto.
