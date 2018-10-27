<template>
    <div id="hello">
        <h1 v_once>{{title}}</h1>
        <input type="text" v-on:input="changeTitle">
        <p>{{sayHello()}} - <a v-bind:href ="link">Google</a></p>
        <p>{{sayTitle()}}</p>
        <hr>
        <p>{{ finishedLink }}</p>
        <p v-html="finishedLink"></p>
        <hr>
        <button v-on:click="increase(2, $event)">Click me + 2!</button>
        <button v-on:click="counter++">Click me + 1!</button>
        <p>{{ counter }}</p>
        <p>{{ counter*2 }}</p>
        <p>{{ counter*2 > 10 ? 'Greater than 10':'Smaller than 10' }}</p>
        <p v-on:mousemove="updateCoordinates">
            Coordinates: {{ x }}, {{ y }}
            - <span v-on:mousemove="dummy">DEAD SPOT</span>
            - <span v-on:mousemove.stop.prevent>DEAD SPOT</span>
        </p>
        <input type="text" v-on:keyup.enter.space="alertMe">
        <hr>
        <!--v-model listen changes and reflect the change all part were we use de variable-->
        <input type="text" v-model="name">
        <p>{{name}}</p>
        <hr>
        <button @click="counter++">Increase</button>
        <button @click="counter--">Decrease</button>
        <button @click="secondCounter++">Increase Second</button>
        <p>Counter: {{ counter }} || SecondCounter {{ secondCounter}}</p>
        <p>{{ result() }} || {{ output }}</p>
    </div>
</template>

<script>

    export default {
        name: "Hello",
        data () { //data its not reactive
            return {
                title: 'Hello World!',
                link: 'http://google.com',
                finishedLink: '<a href="http://google.com">Google</a>',
                counter: 0,
                secondCounter: 0,
                x: 0,
                y: 0,
                name: 'Max'
            }
        },
        computed: { //Excecutes only if the content inside of it changes
          output (){
              console.log('Computed')
              return this.counter > 5 ? 'Greater than 5' : 'Smaller than 5'
          }
        },
        methods: { //exceutes every time because vuejs doesn now the content of the functions
            changeTitle (event) {
                this.title = event.target.value
            },
            sayHello (){
                return "Hello!"
            },
            sayTitle (){
                return this.title
            },
            increase (step, event){
                this.counter += step
            },
            updateCoordinates (event) {
                this.x = event.clientX
                this.y = event.clientY
            },
            dummy (event) {
                event.stopPropagation()
            },
            alertMe() {
                alert('Alert!')
            },
            result(){
                console.log('Method')
                return this.counter > 5 ? 'Greater than 5' : 'Smaller than 5'
            }
        }
    }
</script>
