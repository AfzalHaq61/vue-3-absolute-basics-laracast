1-video (Vue 3 Absolute Basics)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>

    // add this cdn to add vue 3
    <script src="https://unpkg.com/vue@3"></script>
</head>
<body>
    // the v-model will bind the value of input to greeting variable data and also handle listening to variable of its changes so it will be changes in here in input. if its changes dynamically or in data funciton. it is called reactivity.
    <p>
        <input type="text" v-model="greeting">
    </p>

    // The greeting is define in javascript data
    // we can also show its length of the data variable by simple add .length
    <p>
        {{ greeting }} ({{ greeting.length }})
    </p>
    
    // add this script to add vue to the project or page. so create vue app and mount it to a div by its id.
    <script>
        Vue.createApp({

            // we create data funciton which will return data to the page or project
            // for example we define greeting which we show in the page
            data() {
                return {
                    greeting: 'hello world'
                }
            },

            // mounted will call whenever the page is refreshed.
            // we use setTimeOut of javascript for 3 sec and changed the greeting value by this.greeting. this will direct get data funciton and take the variable and also the data whereever it is showing will be changed.
            mounted() {
                setTimeout(() => {
                    this.greeting = 'Changed';
                }, 3000);
            }

        }).mount('#app');
    </script>
</body>
</html>

2-video (Attribute Binding and Event Handling)

// Here is a shortcut for div with classes or id

// It will create a div with all these classes
div.flex.justify-center.p-4.m-4

// It will create a div with id of app
div#app

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="https://unpkg.com/vue@3"></script>

    <style>
        // this styling of html and body will automatically center the div vertically and horizentally
        html, body {
            height: 100%;
        }
        
        body {
            display: grid;
            place-content: center;
        }

        .text-red {
            color: red;
        }

        .text-green {
            color: green;
        }
    </style>
</head>
<body>
    <div id="app">
        // v-bind is call binding dynamic data to class or somthing
        // v-on is used for even calling or generation
        //you can use short form : for v-bind and @ for v-on 
        <button
            :class="active ? 'text-red' : 'text-green'"
            @click="toggle"
        >Click Me</button>

        //you can also use full form like v-bind and v-on
        <button
            v-bind:class="active ? 'text-red' : 'text-green'"
            v-on:click="toggle"
        >Click Me</button>
    </div>
    
    <script>
        Vue.createApp({
            data() {
                return {
                    active: false
                };
            },

            // function is made like this you have to make it in methods funciton other wise it will not work
            methods: {
                toggle() {
                    this.active = ! this.active;
                }
            }
        }).mount('#app');
    </script>
</body>
</html>