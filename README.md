# Tetrix - Tetris in c

## Descrição

Tetrix é um jogo baseado no clássico [Tetris](https://pt.wikipedia.org/wiki/Tetris) de 1985, está versão implemente um versão que utiliza o terminal com caracteres ASCII para renderizar a vizualização.

## Demo

Você pode acessar a demo neste repositório através do link (em breve).

## Como compilar

Para este projeto se fazer necessário a utilização de algumas dependências.

- Cmake
- ncurses

para compilar o projeto utilize o comando `make` na raiz do projeto.

## Arquitetura

A base da arquitetura se basea em alguns serviços executador modular e assicronamente.

### Modo conceitual

```
  ┌────────┐     ┌───────┐   ┌──────────┐
  │  Input ┼────►│  Core ┼──►│  Render  │
  └────────┘     └───┬───┘   └──────────┘
                     │                   
                     │         ┌────────┐
                     └────────►│  Sound │
                               └────────┘
```

## Serviço de input

O serviço de input 🎮 é um modulo assíncrono que guardar comando do teclado e executa ação dentro do core para ser Renderizado em video. 

```
 ┌────────┐   Comandos    ┌──────┐ 
 │  Input │──────────────►│ Core │ 
 └────────┘               └──────┘ 
```

## Serviço  de Core

Toda a estrutura de dados e execução do jogo é executada por este serviço. Ele aguarda comando do  Serviço de input.

## Serviço de Render

O serviço  de Render utilizar dados recebido (frames buffer) do core para serem revelado no terminal. É responsável por desenhar em formato ASCII art dentro do terminal.

```
 ┌───────┐                                        
 │  Core ├──────┐                                 
 └───────┘      ▼                                 
     ▲     ┌────────┐                             
     │     │  game  │                             
     │     │  state┌┼──────┐                      
     │     └───┬───┼┘      │                      
     └─────────┘   │  ┌────┴─────┐    ┌──────────┐
                   └─►│  render  ├──► │ Terminal │
                      └──────────┘    └──────────┘
```
