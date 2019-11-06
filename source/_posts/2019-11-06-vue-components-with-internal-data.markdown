---
layout: post
title: "Vue components with internal data"
date: 2019-11-06 13:35:26 -0300
comments: true
categories: 
---
When you write [components](https://br.vuejs.org/v2/guide/components.html) in vue you sometimes need some internal data in each component, to handle internal behavior.

Like when I had a problem with formating numeric texts.

The component was rendered correctly, but, the first time the user entered the input the format was lost.

I realized that the [`$refs`](https://br.vuejs.org/v2/guide/components-edge-cases.html#Acessando-Instancias-de-Componentes-e-Elementos-Filhos) was undefined and the format function was called again only when the user typed a value and the event `input` was fired.

So I added a internal data that was changed when the component was [mounted](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram) and this behavior disappeared.

First add the data in the component:

~~~
data: function () {
    return { mounted: false }
},
~~~

And changed the value in `mounted` method:

~~~
mounted() {      
    this.mounted = true;
},
~~~

And changed my `computed` value to check the value of the data:

~~~
 computed: {
        awesomeValue: {
            get: function () {

                
                //HERE I CHECK THE VALUE
                if (!this.mounted) {
                    return;
                }

                //... DO THINGS TO GET VALUE

                return valor;
            },
            set: function (value) {

                //... DO THINGS TO SET VALUE

            }
        },

~~~