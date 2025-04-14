---
title: "Selenium Python em Headless no Chrome"
description: "Como executar o Selenium com Python em modo headless no Google Chrome"
date: 2020-04-15
categories: ["Desenvolvimento", "Python"]
tags: ["Python", "Web Scraping", "Selenium", "Webdriver", "Automação"]
---

Em muitos cenários ao utilizar Selenium para web scraping com Python você não pode executar o webdriver com seu padrão. Este abre uma janela com a interface gráfica, como na execução em servidores onde não tem a disponibilidade desse recurso.

Headless é uma opção para executar seus testes sem a necessidade de abrir o browser em um ambiente gráfico, essa função executa o serviço em background, onde toda manipulação acontece por debaixo dos panos. Por sua vez Google Chrome webdriver disponibiliza esse recurso, mas em algumas das suas versões se encontram com problemas ao serem usadas. Nesse tutorial disponibilizarei a versão e o método no qual consegui executar meus projetos.

O link para [ChromeDriver na versão 2.41](https://chromedriver.storage.googleapis.com/index.html?path=2.41%2F), lembrando que as ferramentas usadas são Python 3x e Selenium 3.

## Exemplo

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

chrome_options = Options()
chrome_options.add_argument("--headless")
chrome_options.add_argument("--no-sandbox")
chrome_options.add_argument("--disable-dev-shm-usage")

driver = webdriver.Chrome(
    options=chrome_options,
    executable_path='./chromedriver'
)
```

No exemplo acima é feito a importação do módulo de webdrive da biblioteca selenium juntamento com com a classe Options. Seguindo os passos, primeiramente é feito a instância da classe e o preenchimento dos argumentos necessários para usarmos o webdrive em modo Headless.

Por fim é feito a instância do webdrive do Google Chrome, passando no primeiro parâmetro a instância da classe com as configurações necessárias e no segundo parâmetro o caminho no qual está localizado o o binário do chromedriver baixado pelo link disponibilizado.

## Conclusão

Em busca de diversos webdrives disponíveis como FireFox, Opera e etc e até mesmo a o Google Chrome, somente com o binário da versão 2.41 foi obtido êxito ao usar o recurso. 