---
layout: post
title: "Vue slots #1"
date: 2019-11-06 13:43:55 -0300
comments: true
categories: 
---
When you want to create a component that has dynamic child, that's a case to use the [`<slot>`](https://vuejs.org/v2/guide/components-slots.html) There are many other cases, but this one is beautiful.

I needed that the title of a [card](https://getbootstrap.com/docs/4.3/components/card/#header-and-footer) had a dynamic text based on a certain condition, like: if the application has a context, show the label of the context.

~~~
Vue.component("personal-title-card", {
    template: `
	<div>
		<div class="float-left">
			<slot></slot>
		</div>                      
        <div class="float-right">
			<strong>{{contextLabel}}</strong>
		</div>
    </div>`,
    computed: {
        ...mapGetters(["contextLabel"])
    }
});
~~~

To use is as simple as that:

`<personal-title-card>Accumsan massa elementum.</personal-title-card>`

According to the [documentation](https://br.vuejs.org/v2/guide/components-slots.html):

> A `<slot>` outlet without name implicitly has the name “default”.

You can name a [`<slot>`](https://vuejs.org/v2/guide/components-slots.html#Named-Slots) like:

~~~
Vue.component("personal-title-card-2", {
    template: `
	<div>
		<div class="float-left">
			<slot name="text"></slot>
		</div>                      
        <div class="float-right">
			<strong>{{contextLabel}}</strong>
		</div>
    </div>`,
    computed: {
        ...mapGetters(["contextLabel"])
    }
});
~~~

Again, to use is as simple as that:

~~~
<personal-title-card>
  <template v-slot:text>
    Accumsan massa elementum.
  </template>
</personal-title-card>
~~~