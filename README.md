# React and Vue cheat sheet

## Vue

- Vue apps consist of a template, possible components, data, methods, computed and watchers.
- Vue uses a virtual DOM and a Model-ViewModel-Model architecture.
  - `data()` returns an instance of the Model
  - ViewModel is the mounted `App` that includes `data()`, `template`, `methods` among others.
  - View is the root element where the rendered DOM elements are injected to.

### Directives
- `v-text` or `{{ var }}` - insert text to textContent
- `v-bind` or `:attribute` - bind a variable to a reactive attribute
- `v-on` or `@event` - add a callback to an event, e.g. click
- `v-model` - two way binding of an input to a variable
- `v-if` - for conditional rendering of elements
- `v-for` - for rendering elements in a data structure

### Event modifiers
- Can be in conjunction with `v-on` or `@event="someFunction"`
  - .stop - the propagation of the click event will stop
  - .prevent - prevents default on `@submit.prevent="func"`
  - .self - only trigger handler if event.target is the element itself
  - .once - trigger the event only once

### Lifecycle hooks
- created - after the instance has finished processing all state-related options
- beforeMount - before initial render and component mounting
- mounted - when element is mounted after initial render
- beforeUpdate - before the component is about to update its DOM tree due to a reactive state change
- updated - after the component has updated its DOM tree due to a reactive state change

### Some snippets
```js
<script>
    const App = {
        data() {
            return {
                fullName: "John Doe",
            };
        },
    };
</script>
```

```js
<script>
    const App = {
        data() {
            return {
                counter: 0,
            };
        },
        methods:{
            increase(value){
                this.counter += value;
            },
            decrease(){
                this.counter--;
            }
        }
    };
</script>
```

```js
<div id="vue-app">
    <div>{{num}}<sup>2</sup> + {{num}}<sup>2</sup> = {{ result }}</div>
    <input type="number" v-model="num" />
</div>
<script>
    const App = {
    data() {
        return {
            num: 0,
        };
    },
    computed: {
        result: function () {
            return Math.pow(this.num, 2) * 2;
        },
    },
};
</script>
```

```js
const App = {
  data() {
    return {
      name: "John Doe",
    };
  },
  watch: {
    name(val, oldValue) {
      alert(`Name will be changed from ${oldValue} to ${val}?`)
    },
  },
  methods: {
    changeName() {
      this.name = this.$refs.input.value;
    },
  },
};
```
  
```js
methods: {
    async get() {
      this.answer = 'Loading...'
      try {
        const res = await fetch('https://example.com/api')
        this.answer = (await res.json()).answer
      } catch (error) {
        this.answer = 'Error! Could not reach the API. ' + error
      }
    }
}
```
