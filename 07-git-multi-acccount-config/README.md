# Gerenciando múltiplas contas do git

Em algum momento você já deve ter se deparado com a necessidade de utilizar mais de um email na configuração do git. Seja por estar fazendo commits em projetos que utilizam um emails diferentes ou por que na mesma máquina você tem projetos feitos para empresas diferentes.

A troca do email normalmente pode ser feita pelo comando

```bash
git config user.email your@email.here
```

Mas, ficar alterando essa configuração manualmente toda vez que precisar fazer um commit em um projeto diferente não é muito produtivo, não é mesmo?

E se eu te disser que é possível realizar uma configuração específica do git para cada diretório?

## A solução

Vamos supor que você organize seus projetos em uma estrutura de diretórios dessa forma:

```
Development/
├── CompanyA
│   ├── project-a-1
│   └── project-a-2
├── CompanyB
│   ├── project-b-1
│   └── project-b-2
├── my-project-1
└── my-project-n
```

Para configurar uma conta diferente para seus projetos pessoais, projetos sob o diretório  `CompanyA` e projetos sob o diretório `CompanyB`, podemos fazer uso da [Inclusão condicional] de configurações no seu arquivo `.gitconfig`

A forma de como vamos trabalhar é deixando no arquivo `.gitconfig` todas as configurações compartilhadas e criar arquivos com configurações específicas para cada diretório.

**.gitconfig**


Seu arquivo `.gitconfig` se parecerá com assim:

```
[user]
    name = Mesaque Francisco
    email = my@personal.email
    signinKey = ......

...

[includeIf "gitdir:~/Development/CompanyA/"]
    path = .gitconfig-company-a

[includeIf "gitdir:~/Development/CompanyB/"]
    path = .gitconfig-company-b
```

**.gitconfig-company-a**


Seu arquivo `.gitconfig-company-a` se parecerá com assim:

```
[user]
    email = ...@companya.com
    signinKey = <diffrent key>
```

**.gitconfig-company-b**


Seu arquivo `.gitconfig-company-b` se parecerá com assim:

```
[user]
    email = ...@companyb.com
    signinKey = <diffrent key>
```

Note que aqui eu utilizei o parâmetro `signinKey` como exemplo de mais coisas podem ser alteradas nesses arquivos, mas poderiam ser, por exemplo, aliases exclusivos para projetos da ComapanyB.

## Estrutura final de arquivos

Imaginando que você esteja em um sistema unix-like, e esteja na sua home, ao listar seus arquivos teríamos essa visão:

```
.
├── Development
│   ├── CompanyA
│   │   ├── project-a
│   │   └── project-b
│   ├── CompanyB
│   │   ├── project-a
│   │   └── project-b
│   ├── my-project-1
│   └── my-project-n
├── .gitconfig
├── .gitconfig-company-a
└── .gitconfig-company-b
```

Para verificar se tudo funcionou corretamente, basta rodar dentro dos diretórios dos projetos o comando

```
git config user.email
```

Esse comando retornará o email atual utilizado para os commits.

[Inclusão condicional]: https://git-scm.com/docs/git-config#_conditional_includes