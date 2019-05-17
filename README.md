# Atividade prática

Desenvolva uma aplicação que realize as operações de CRUD para a entidade `Integrante` e `Banda`. 
A funcionalidade precisa estar disponível com UI (interface para o usuário) com um template usável.
As demais informações podem ser inseridas via `script sql`.

```java
class Integrante{
    private int id;
    private String nome;
    private LocalDate dataDeNascimento;
    private CPF cpf = new CPF("");
}
class Banda{
    private int id;
    private String localDeOrigem;
    private String nomeFantasia;
    private List<Integrante> integrantes;
}
```

## Metodologia

Esta atividade prática está planejada para ser executada em equipes com três ou quatro pessoas. Toda a atividade deverá ser executada o intervalo das aulas e quando o tempo se esgotar as equipes devem fazer a entrega da respectiva atividade. Cada equipe deve fazer o __fork__ deste projeto e implementar sua própria solução. 

Caso surja alguma dúvida no desenvolvimento, falar de imediato via [Slack](https://ifpb-dac-20191.slack.com/messages/CHZGZMM17/). 
> Lembrete: Não guardem dúvidas, elas são como as dívidas. Acumulam-se e nos prejudicam :)
 

## Requisitos

* **RF01** - Implementar os métodos acessores para as classes `Integrante` e `Banda`; 
* **RF02** - Implementar a classe de acesso aos dados; 
* **RF03** - Na pasta __banda__, criar as páginas `edit.xhtml` e `list.xhtml` para o arquivo de template `template.xhtml`; 
* **RF04** - Criar um Conversor para a classe `Integrante`; 
* **RF05** - Adicionar um `selectOneMenu` na página `edit.xhtml` da pasta __banda__. 
Deve ser possível selecionar um `Integrante` e associar sua instância ao atributo `integrantes` da classe `Banda` 
* **RF06** - Criar as páginas para edição e listagem da entidade `Integrante`; 
* **RF07** - Criar uma página que permita realizar uma busca por `CPF`; 
* **RF08** - Criar uma página que permita realizar uma busca por `localDeOrigem`; 
* **RF09** - Realizar o deploy da aplicação no Docker usando uma das __images__ do [Payara](https://hub.docker.com/u/payara). 


## Script do banco

O `script` para criação do banco.

```
CREATE TABLE integrante(
	id serial PRIMARY KEY,
	nome VARCHAR(50),
        dataDeNascimento DATE,
	CPF VARCHAR(15)
);

CREATE TABLE banda(
	id SERIAL PRIMARY KEY,
	localDeOrigem VARCHAR(100),
	nomeFantasia VARCHAR(100)
);
CREATE TABLE integrante_banda(
	id_banda int,
	id_integrante int,
	FOREIGN KEY (id_banda) REFERENCES banda(id) ON DELETE RESTRICT,
	FOREIGN KEY (id_integrante) REFERENCES integrante(id) ON DELETE RESTRICT,
	PRIMARY KEY(id_banda,id_integrante)
);
```