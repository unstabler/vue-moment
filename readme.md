# vue-moment-v3

- forked from brockpetrie/vue-moment
- added vue v3 support

# CHANGES
1. migrate filters to `App.config.globalProperties.$filters`
2. provide moment, moment-filters via `Vue.provide<T>`
3. babelrc: add 'transform-object-rest-spread' plugin'


# SYNOPSIS
- the way to write plugin has changed: https://v3.vuejs.org/guide/plugins.html#writing-a-plugin
- filters are removed in v3: https://v3.vuejs.org/guide/migration/filters.html#overview
  - so you can use global object like this:
```vue
<template>
    <div class="user" v-for="user in users" :key="user.id">
        <h3>{{ user.name }}</h3>
        <h5>last access: {{ $filters.moment(user.lastAccess, "YYYY-MM-DD") || "unknown" }}</h5>
    </div>
</template>
<script lang="ts">
import { defineComponent, watch, inject } from 'vue';
// ...

export default defineComponent({
  // ...
});

</script>
```
- or you can use provide / inject pattern https://v3.vuejs.org/guide/component-provide-inject.html#working-with-reactivity
  - like this

```vue
<template>
    <div class="user" v-for="user in users" :key="user.id">
        <h3>{{ user.name }}</h3>
        <h5>last access: {{ momentFilter.moment(user.lastAccess, "YYYY-MM-DD") || "unknown" }}</h5>
    </div>
</template>
<script lang="ts">
import { defineComponent, watch, inject } from 'vue';
// ...

export default defineComponent({
  setup() {
    const momentFilters = inject('moment-filters');
    // ...
    return {
      momentFilters,
      users
    };
  }
});

</script>
```

4. sorry for my bad english 
