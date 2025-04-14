---
title: "Singleton Python para compartilhamento de instância do Web Driver Selenium"
description: "Como implementar o padrão Singleton em Python para compartilhar uma única instância do Selenium WebDriver"
date: 2021-02-22
categories: ["Desenvolvimento", "Python", "Design Patterns"]
tags: ["Python", "Selenium", "Design Patterns", "Singleton", "WebDriver"]
---

Utilizando Selenium em alguns casos você precisa de uma única instância desse web driver em várias partes da sua aplicação, como exemplo uma aplicação para WhatsApp Web. Guardar a sessão do web driver e carregá-la em uma nova instância ao necessitar em mais de um serviço, pode acabar tendo perda de performance e flexibilidade da aplicação, então usar uma padrão de projeto como Singleton acaba sendo uma boa saída.

O Singleton é um padrão de projeto criacional que permite a você garantir que uma classe tenha apenas uma instância, enquanto provê um ponto de acesso global para essa instância. Utilizar o padrão Singleton quando uma classe em seu programa deve ter apenas uma instância disponível para todos seus clientes; por exemplo, um objeto de base de dados único compartilhado por diferentes partes do programa.

## Exemplo

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

class WebDriver:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            chrome_options = Options()
            chrome_options.add_argument("--headless")
            chrome_options.add_argument("--no-sandbox")
            chrome_options.add_argument("--disable-dev-shm-usage")
            
            cls._instance = super().__new__(cls)
            cls._instance.driver = webdriver.Chrome(
                options=chrome_options,
                executable_path='./chromedriver'
            )
        return cls._instance
    
    def get_driver(self):
        return self.driver

# Exemplo de uso
driver1 = WebDriver().get_driver()
driver2 = WebDriver().get_driver()

print(driver1 == driver2)  # True - Mesma instância
```

Agora podemos garantir que a classe do web driver tenha apenas uma única instância, e podemos utilizá-la em toda aplicação.

## Referência

- [Refactoring Guru - Singleton](https://refactoring.guru/pt-br)

Tags: Python, Selenium, Singleton, Design Patterns 