---
layout: post
title: "Vue masked input"
date: 2019-11-06 13:50:00 -0300
comments: true
categories:  [vue, vuejs, vuetify]
---
There are many excelent [components](https://github.com/vuejs/awesome-vue#masked-input) to get a [masked input](https://en.wikipedia.org/wiki/Input_mask) when you are using vuejs. But, I could not find one that fill all my requisites.

I have use the following aproach:

I used the [string-mask](https://github.com/the-darc/string-mask) component to format the values;
Write the `get` and `set` for the value of the input; and
Write one method to verify if the value typed is an number.


GET:

~~~javascript

    get() {
        const valuePrice = state.price;
        const formatter = new StringMask(state.maskinput, {
            reverse: true
        });
        let result = "";
        if (valuePrice !== "" && valuePrice != null) {
            result = formatter.apply(valuePrice.toString().replace(/[^0-9]/g, ""));
        }
        return result;
    }
    
~~~

SET:

~~~javascript
set(value) {
    const formatter = new StringMask(state.mascara, {
        reverse: true
    });
    
    const normalized = value.replace(/[^0-9]/g, "");
    
    let result = "";
    
    if (normalized !== "" && normalized !== null) {
        result = formatter.apply(normalized);
    }
    
    if (result === "0" || result === "0,00") {
        result = null;
    }

    state.price = result;
}
~~~

Verify if is number:

~~~javascript

methods: {
    isNumber: function (evt) {
        evt = (evt) ? evt : window.event;
        var charCode = (evt.which) ? evt.which : evt.keyCode;
        if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
            evt.preventDefault();;
        } else {
            return true;
        }
    }
},

~~~

To use:

~~~javascript

@keypress="isNumber($event)"
:value="valor" @input="value => valor = value"

~~~


We can add a default value, in my case, I cannot allow a zero value.