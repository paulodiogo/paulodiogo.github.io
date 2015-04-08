---
layout: post
title: "O ataque do Deus ASP MVC: componentizando entranhas e espólio"
date: 2015-04-07 22:55:17 -0300
comments: true
categories: 
---

O ASP MVC é realmente um Deus hoje em dia. É venerado por todos os desenvolvedores .NET e muitos de outros mundos.
Sem muitas delongas, qual o objetivo, componentizar com ASP MVC. Para muitos deve ser trivial, mas nunca tinha feito isso. Já havia feito sistemas em ASP MVC, mas não um componente. Com dezenas de possíveis clientes.
Aí está uma coisa que a Microsoft faz bem (#FanBoyDetected), componentizar e deixar a nossa vida mais tranquila, não mais fácil.

É muito fácil reusar em ASP MVC. No meu caso, criei uma ‘class library’ e adicionei as referências que eu iria usar (via nuget).

No caso de páginas, scripts, css etc, segue o rito de sempre, criar o que se quer e marcar ele como 'Embedded Resources'.

Quando for criar as 'Views', pode ser criado no mesmo esquema das aplicações padrão:

$(Project)/Views/Controller/Pagina.wtv

Inclusive pode ser criado um arquivo Web.config na pasta 'Views' para configurações.

Quanto aos outros tipos de recursos:

Eu estou usando o 'EmbeddedResourceVirtualPathProvider' feito pelo @mcintyre321. Ele carrega os arquivos que estiverem em 'Embedded Resources'.

Install-Package EmbeddedResourceVirtualPathProvider

Vai ser adicionado um arquivo 'App_Start\RegisterVirtualPathProvider.cs', que deve ser executado no start da aplicação, no  'Global.asax'.

Enfim, era isso aí.

PS. Post em construção, vou fazer um projeto de teste.