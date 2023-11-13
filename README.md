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

3-Video (Lists, Conditionals, and Computed Properties)

<!doctype html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <title>Episode 3: Lists and Computed Properties</title>
    <script src="https://unpkg.com/vue@3"></script>
    // you can add tailwind cdn like this.
    <script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="h-full grid place-items-center">
    <div id="app">
        // Differenve between v-if and v-show is that v-show jsut toggle the visiblilty it onlay change display to hidden and not hidden other wise we can apply logic/condition through v-if
        <section v-show="inProgressAssignments.length">
            <h2 class="font-bold mb-2">In Progress</h2>
            <ul>
                // we can use v-for loop like this
                // also assign key to loop because it assign it to every item in the loop so it make it unique and we can do our operation easily on every unqiue item. if we can assign key then it will give us errors.
                <li
                    v-for="assignment in inProgressAssignments"
                    :key="assignment.id"
                >
                    <label>
                        {{ assignment.name }}
                        <input type="checkbox" v-model="assignment.complete">
                    </label>
                </li>
            </ul>
        </section>

        <section v-show="completedAssignments.length" class="mt-8">
            <h2 class="font-bold mb-2">Completed</h2>

            <ul>
                <li
                    v-for="assignment in completedAssignments"
                    :key="assignment.id"
                >

                <label>
                        {{ assignment.name }}

                        <input type="checkbox" v-model="assignment.complete">
                    </label>
                </li>
            </ul>
        </section>
        
        // Pre tags is used to display you data in json strigfy format.
        <pre>
            {{ assignments }}
        </pre>
    </div>

    <script>
        let app = {
            data() {
                return {
                    assignments: [
                        { name: 'Finish project', complete: false, id: 1 },
                        { name: 'Read Chapter 4', complete: false, id: 2 },
                        { name: 'Turn in Homework', complete: false, id: 3 },
                    ]
                }
            },

            // If you want some method to be cached.
            // if we have a repeated code then we can used this.
            // if we have some leangthy logics and reapeated againa and again and we want to cached it then we can use it
            // just define computed: {}.
            // then right computed property name like a fucntion and paste your logic and then just used its name like a data variable and it will work
            computed: {
                inProgressAssignments() {
                    // we are taking filter on assignments it will take it on each one the assignment which is completed or else
                    return this.assignments.filter(assignment => ! assignment.complete);
                },

                completedAssignments() {
                    // we can fiter the assignment and the just loop each one and passed our logic on it
                    return this.assignments.filter(assignment => assignment.complete);
                }
            }
        };

        Vue.createApp(app).mount('#app');
    </script>
</body>
</html>