---
id: 862
date: '2019-02-23T20:18:59+02:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'https://glowingsword.ru/861-revision-v1/'
permalink: '/?p=862'
---

Столкнулся сегодня с ошибкой :

You are using the runtime-only build of Vue where the template compiler is not available. Either pre-compile the templates into render functions, or use the compiler-included build

при попытке заюзать  Ant Design для Vue, при этом ошибка отлавливается только в консоли, в браузере просто отображается белая страница.

Оказалось, что в main.js вместо
<code>
new Vue({
el: "#app",
components: { App },
template: "<app></app>"
});
</code>

нужно было указать 
<code>
  new Vue(App).$mount('#app')
</code>

или

<code>
new Vue({
  render: h => h(App),
}).$mount('#app')
</code><code>

после чего проблема перестала проявляться.

Проблема проявляется в первом случае, так как он использует runtime-only версию Vue в которой отсутствует компиляция темплейтов.
Разница между этими двумя видами билдов Vue неплохо объясняется тут https://vuejs.org/v2/guide/installation.html#Runtime-Compiler-vs-Runtime-only

Странно что разработчики  Ant Design для Vue в своём руководстве https://vue.ant.design/docs/vue/use-with-vue-cli/ советуют юзать вариант, который не корректно работает в связке с vue-cli 3 и babel-plugin-import.</code>