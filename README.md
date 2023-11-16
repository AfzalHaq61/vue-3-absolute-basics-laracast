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

4-video (Episode 4: Your First Custom Vue Component)

<!doctype html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <title>Episode 4: Your First Custom Vue Component</title>
    <script src="https://unpkg.com/vue@3"></script>
    <script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="h-full grid place-items-center">
    <div id="app">
        // we can use the component like this
        <app-button>Submit</app-button>
    </div>

    <script>
        let app = {
            // we can define components like this. in this video child component have not there own file but define in the same file.
            components: {
                // component name
                'app-button': {

                    //in template we define the file main data.
                    // we can disabled button by property attribute disabled which is dynamically defined
                    // also we can use this defined property in tailwind by class called disabled
                    // disabled:cursor-not-allowed. like this which is used in button
                    template: `
                        <button 
                            class="bg-gray-200 hover:bg-gray-400 border rounded px-5 py-2 disabled:cursor-not-allowed" 
                            :disabled="processing"
                        >
                            <slot />
                        </button>
                    `,

                    data() {
                        return {
                            processing: false
                        };
                    }
                },
            }
        };

        Vue.createApp(app).mount('#app');
    </script>
</body>
</html>

5-Video(Episode 5: Extract Components to Their Own Files)

<!doctype html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <title>Episode 5: Extract Components to Their Own Files</title>
    <script src="https://unpkg.com/vue@3"></script>
    <script src="https://cdn.tailwindcss.com"></script>
</head>

<body class="h-full grid place-items-center">
    <div id="app">
        <app-button>Submit</app-button>
    </div>
    // there is some files like we are making in simple index html files then we can add type="module"
    <script type="module">

        // import component like this
        import AppButton from "./js/components/AppButton.js";

        // then rgister like this. it is ready to use.
        let app = {
            components: {
                'app-button': AppButton
            }
        };

        Vue.createApp(app).mount('#app');
    </script>
</body>
</html>

//Script Files this is a code which we use in the main file
export default {
    template: `
        <button class="bg-gray-200 hover:bg-gray-400 border rounded px-5 py-2 disabled:cursor-not-allowed" :disabled="processing">
            <slot />
        </button>
    `,

    data() {
        return {
            processing: true
        };
    }
}

6-Video (Episode 5: Extract Components to Their Own Files )

<!doctype html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <title>Episode 5: Extract Components to Their Own Files</title>
    <script src="https://unpkg.com/vue@3"></script>
    <script src="https://cdn.tailwindcss.com"></script>

    // i added the spinner website url in the end
    <style>
        @keyframes spinner {
            to {transform: rotate(360deg);}
        }

        // the class will first change the color to transparent and then load the spinner.

        .is-loading { color: transparent; }

        .is-loading:before {
            content: '';
            box-sizing: border-box;
            position: absolute;
            top: 50%;
            left: 50%;
            width: 20px;
            height: 20px;
            margin-top: -10px;
            margin-left: -10px;
            border-radius: 50%;
            border: 2px solid #ccc;
            border-top-color: #000;
            animation: spinner .6s linear infinite;
        }
    </style>
</head>

<body class="h-full grid place-items-center">
    // processing is pass as a prop we can use its data in the app button
    <div id="app">
        <app-button :processing="true">Submit</app-button>
    </div>

    <script type="module">
        // all the components will be declared in this file.
        import App from "./js/components/App.js";

        Vue.createApp(App).mount('#app');
    </script>
</body>
</html>

// App.js file
// in this file all the components will be declared here and the then we will import this in the main file.

import AppButton from "./AppButton.js";

export default {
    components: {
        'app-button': AppButton
    }
};

// Button.js file

//you can see here dynamic classes we can bind classes like this. this method is called object method we can do this by arrays or something else. 
// if the type is primaray so that statemnet will be true else other.
//and the first one we make it true which will be for every props.
export default {
    template: `
        <button 
            :class="{
                'border rounded px-5 py-2 disabled:cursor-not-allowed': true,
                'bg-blue-600 hover:bg-blue-700': type === 'primary',
                'bg-purple-200 hover:bg-purple-400': type === 'secondary',
                'bg-gray-200 hover:bg-gray-400': type === 'muted',
                'is-loading': processing
            }" 
            :disabled="processing"
        >
            <slot />
        </button>
    `,

    //props are use like this.
    // this will be in detail we define here as an object
    // here is its type.
    // also define default for it
    props: {
        type: {
            type: String,
            default: 'primary'
        },

        processing: {
            type: Boolean,
            default: false
        }
    }

    or we can also do this like this
    props: {
        type: String,
        processing: Boolean,
    }
}

// adding spinner from this url
https://stephanwagner.me/only-css-loading-spinner

In Vue.js, there are certain attributes that are recognized by default, even without using the : binding syntax. These attributes include standard HTML attributes like class, style, and id. Therefore, when you use :class or :style, you are explicitly indicating to Vue.js that you want to bind those attributes dynamically.

On the other hand, custom attributes, like processing and type in your example, are not automatically recognized for dynamic binding. If you want to dynamically bind a custom attribute, you need to use the : binding syntax.

In your case:

html
Copy code
<app-button :processing="false" type="secondary">Submit</app-button>
:processing="false": This works because you are using the :, indicating that you want to bind the processing attribute dynamically.

type="secondary": This might not work as expected if the type attribute is a custom attribute for your app-button component. To dynamically bind it, you should use :type:

html
Copy code
<app-button :processing="false" :type="'secondary'">Submit</app-button>
By using :type="'secondary'", you are explicitly telling Vue.js to bind the type attribute dynamically, even if it's a custom attribute.