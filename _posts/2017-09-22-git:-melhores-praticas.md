---
layout: post
title: "Git: Melhores práticas"
date: 2017-09-22 00:02:24
image: 'http://res.cloudinary.com/victorpre/image/upload/v1506043766/blogposts/gitlogo.png'
description: 'Entendendo como se beneficiar da sua ferramenta de versionamento'
main-class: 'jekyll'
tags:
  - git
twitter_text: 'Boas práticas utilizando git'
introduction: 'Algumas boas práticas ao utilizar sua ferramenta de versionamento. Nomeando commits e branchs'
---

## Por que versionar o código de seu projeto?

  Versionamento é algo importantíssimo quando estamos falando de desenvolvimento de software. Uma ferramenta de versionamento bem organizada
torna muito mais fácil a comparação de arquivos, realização de mesclagem de ramos (*merge*) ou até *rollbacks* de emergência no ambiente de produção.

  Primeiramente, o ramo principal `master` nunca deveria ser seu branch de trabalho.

> Mas por que?

  Simplesmente não faça isso. É extramente mais complicado manter seu código organizado desta maneira. Em um projeto *open-source* por exemplo,
seria muito mais difícil para pessoas de fora entenderem quais funcionalidades entraram e em qual versão do projeto elas entraram.
Será muito mais difícil identificar e dar *rollback* em um bug que foi inserido no seu software quando todos seus commits foram no mesmo branch.
Mesmo que seu projeto não seja *open-source*, quando novos desenvolvedores entram no projeto, um processo precisa existir:

  Imagine um time com 3 ou mais pessoas trabalhando e *commitando* no mesmo *branch*: isso pode desencadear diversos conflitos! É mais difícil controlar
e garantir o funcionamento de seu sistema como um todo, pois as modificações de outros podem interferir nas suas, isso sem falar que, se todos
estão mandando tudo direto para o `master`, não há um processo sólido de de revisão de código (*code review*).

### Nomeando suas branches

  Primeiramente, quando trabalhando em uma nova funcionalidade, o desenvolvedor deveria originar seu branch à partir de um ambiente estável, geralmente
o `master`, com um nome que realmente descreve sobre o que é aquela funcionalidade sendo desenvolvida.

  De nada ajuda e não faz sentido para os desenvolvedores que não estão trabalhando naquele branch se ele foi nomeado, por exemplo, baseado em um código 
identificador/id de ferramentas de gerenciamento tais como [Jira](https://www.atlassian.com/software/jira), [Trello](https://trello.com/), etc..

  Um bom nome em seu branch ajuda desenvolvedores revisarem o código quando existem várias branches em seu repositório local, um exemplo ao executarmos
o comando `git branch`:

{% highlight bash  %}
$ git branch
  .
  .
  TASK-316
  TASK-322
  TASK-340
  TASK-341
  TASK-345
  TASK-348
  TASK-380
  TASK-387
  .
  .
{% endhighlight %}
*Qual o propósito destes branchs?*


  Algumas simples regras podem ser seguidas ao originar seu novo branch:

<ul class="browser-default">
<li> O nome deve ser simples conciso, que represente sua tarefa;</li>
<li> Um único idioma deve ser utilizado;</li>
<li> Não utilize códigos que não tem sentido quando sem contexto;</li>
<li> Começar com letras minúsculas;</li>
<li>Palavras separadas por hífens <code class="highlighter-rouge">-</code>.</li>
</ul>

  Além disso, algumas *tokens* podem ser definidas em seu projeto que vão sempre preceder os nomes de seus ramos:

|    Nome do Branch     |               Descrição                |
| :----------------: | :--------------------------------------: |
| `feature-< name >` | Quando desenvolvendo uma nova funcionalidade ou melhoria |
|   `bug-< name >`   | Quando há um bug que necessita de correção e mesclagem |
| `hotfix-< name >`  | Quando há a necessidade de uma ação imediata em um comportamento indesejado no sistema |

  Por exemplo, se você está desenvolvendo uma nova funcionalidade implementando `User Portal`, um bom nome para seu branch poderia ser:

{% highlight bash  %}
$ git checkout master && git pull
$ git checkout -b 'feature-user-portal'
$ git push -u origin 'feature-user-portal'
{% endhighlight %}

### Mensagens de commit

> *Por que alguém deveria escrever mensagens de commit fáceis de entender?*

Enquanto estava escrevendo este artigo, procurando alguns exemplos de mensagens de commit não muitos boas e então me deparei com [este site](http://www.commitlogsfromlastnight.com/).
 **Não** ~~commita~~ cometa este mesmo erro.

 Um commit bem escrito, conciso e consistente é fundamental quando utilizando `git log` and claro, esta é uma ferramente muito importante e poderosa
 quando trabalhando com versionamento de código. Além disso, é uma ótima maneira de comunicar modificações para outros desenvolvedores e para seu futuro eu também 
 (quem nunca fez algo e depois não lembrava o porque de ter feito? :thinking: )

 Em um projeto grande e de longo termo, o seu sucesso é fortemente dependente de sua **manutenabilidade** e por essa razão é muito importante
 para aqueles que mantém o projeto conseguirem utilizar efetivamente o log do projeto.

 Entendendo commits de outros e seus pull requests torna muito mais fácil de entender quando existe uma descrição (mesmo que breve) do que foi feito.

### Revisão de código (*code review*)
