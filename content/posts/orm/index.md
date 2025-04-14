---
title: "O que é mapeamento objeto relacional? (ORM)"
description: "Entenda o conceito de ORM e como ele facilita o desenvolvimento de software"
date: 2024-03-24
categories: ["Desenvolvimento", "Banco de Dados"]
tags: ["ORM", "Banco de Dados", "Desenvolvimento", "Frameworks"]
image: "https://dkrn4sk0rn31v.cloudfront.net/uploads/2019/11/03082200/ORM-CAPA.png"
---

No desenvolvimento de software é muito comum usar linguagens de programação com o paradigma orientado a objetos e em suas bases de dados utilizam banco de dados relacionais. Embora tenha passado muito tempo, os bancos de dados relacionais continuam muito fortes no mercado, então começou-se a usar uma técnica de programação para abstrair a diferença entre esses paradigmas.

ORM é uma camada que mapeia o modelo de objetos (aplicação) e o modelo relacional (base de dados). Onde é abstraída a diferença entre os paradigmas, e o mesmo fará o papel de manager. Você não precisará escrever queries SQL, suas classes ajudarão a persistir os dados e buscá-los. Além de muitos recursos que diferenciam-se entre as ferramentas que utilizam dessa técnica.

## Frameworks que utilizam ORM

Geralmente ORMs encontram-se em Frameworks, mas muitos desenvolvedores costumam desenvolver seu próprio. Uma lista de algumas ferramentas que utilizam ORM:

- Django (Python)
- Laravel (PHP)
- Hibernate (Java)
- Ruby on Rails (Ruby)
- Sequelize (NodeJS)
- NHibernate (C#)

## Exemplo prático com Django

Abaixo uma classe modelo em uma aplicação Django, ela conterá os campos e os comportamentos que serão armazenados. Cada modelo será equivalente a uma tabela na base de dados, e cada atributo é um campo específico e será mapeado para coluna no banco de dados. ID é um campo automático, mas seu comportamento pode ser substituído.

```python
from django.db import models

class Pessoa(models.Model):
    primeiro_nome = models.CharField(max_length=30)
    segundo_nome = models.CharField(max_length=30)
```

SQL equivalente:

```sql
CREATE TABLE pessoa (
    "id" serial NOT NULL PRIMARY KEY,
    "primeiro_nome" varchar(30) NOT NULL,
    "segundo_nome" varchar(30) NOT NULL
);
```

## Conclusão

ORM é um excelente recurso, melhorando a produtividade do desenvolvedor, dando uma boa padronização ao seu projeto e lhe dando uma maior facilidade na manutenção. 