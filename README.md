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

7-Video (Episode 6: Bring it All Together)

import Assignments from "./Assignments.js";
import AssignmentList from "./AssignmentList.js";
export default {
    components are declared in two types.
    components: {
        //one way
        'assignments': Assignments,
        //second way. you cam use it like <assignments></assignments> or <Assignments></Assignments> both will work
        Assignments,
        AssignmentList
    },

    //we can also use component like this which is called simple file component
    template: `
        <assignments />

        //both will work
        //it will also work like this.
        <assignment-list :assignments="filters.inProgress" title="In Progress"></assignment-list>
        //if you use this the name are similer it will work
        <AssignmentList :assignments="filters.inProgress" title="In Progress"></AssignmentList>
    `,
};

// only make components of those which is used again and again you dont have need to make component of every things.

we can also make a very beautiful and easy filters like this just like we create inProgress and completed
filters() {
        return {
            inProgress: this.assignments.filter(assignment => ! assignment.complete),
            completed: this.assignments.filter(assignment => assignment.complete)
        };
    }

8-Video (Handle a Form Submission)

// i have assign borders but it just shown all over the parent <ul> but not on li rows so we add devide-y it will add border to li itself.
<ul class="border border-gray-600 divide-y divide-gray-600">

// when you click on submit button @submit will just listen your event and directly call to your add function.
<form @submit="add">
<button type="submit" class="bg-white p-2 border-l">Add</button>

// when there is no e.preventDefault() then when you submit the form then it refresh it after submit. else it will submit.
 add(e) {
    e.preventDefault();

    alert('hello');
}

// you can also added @submit.prevent. It work the same.
<form @submit.prevent="add">
<button type="submit" class="bg-white p-2 border-l">Add</button>

add() {
    alert('hello');
}

// so we add/push new array to assignments
methods: {
        add() {
            this.assignments.push({
                name: name,
                completed: false,
                id: this.assignments.length + 1
            });
        }
    }

 9-Video (Parent-Child State Communication)  

 // if there is parent and child components so we can passed data to child component by the props but when you want to pass data from child to parent then you will create an event by this.$emit('name', value) and give it name and pass data in second arguments and the you can listen it by @name(functionName) and then call function functionName(acceptArguments) and you can do your job.

// when this function called then it will create event by emit with name add and the seocnd argument us the value
 methods: {
        add() {
            this.$emit('add', this.newAssignment);

            this.newAssignment = '';
        }
    }

// it will direct listen the add cusotm event in parent file and will call the funciton which is passed to it.
<assignment-create @add="add"></assignment-create>

// so in this mehtod it will recieve that data in name which is passed to the event and then add to the assigments array.
methods: {
        add(name) {
            this.assignments.push({
                name: name,
                completed: false,
                id: this.assignments.length + 1
            });
        }
    }

// we can also do it by this way
// just passed the assigments array to the child component and add new assignment to it there it will work but it is wierd it will passed all the assignments array and add the new array to it
props: {
        assignments: Object
    }

10-Video(It's All So Easy)

// in this video main focus is computed properties.
// how to filter assignments by tags.
// array maping.
// set array by unique.
// and make an array of set and add other elements to the array.
// active tags.
// filter tag by click on button tags

// we are taking tags from computed property
<div class="flex gap-2">
    <button
        v-for="tag in tags" 
        class="border rounded px-1 py-px text-xs"
    >{{ tag }}</button> 
</div>

computed: {
    // when you want an object to map so that you take only one element from it so like we take only tag from it here.
    tags() {
        return this.assignments.map(a => a.tag);
    }

    // when we want to make it this array unique it will only take unique tags.
    tags() {
        return new Set(this.assignments.map(a => a.tag));
    }

    // here we make an array and add all to the array of first index. then set of tags in second index. but it will not give the second index value. it will gie it format so add ...to the second index like in the below
    tags() {
        return ['all', new Set(this.assignments.map(a => a.tag))];
    }

    // it will give correct data
    tags() {
            return ['all', ...new Set(this.assignments.map(a => a.tag))];
        }
}

// tag button code and assigments table
<div class="flex gap-2">
    // when click on tag will pas tag into current tag.
    // apply dynamic classes it will apply classes to that tag whcih active when tag is equal to current tag it will apply the classes
    <button
        @click="currentTag = tag"
        v-for="tag in tags" 
        class="border rounded px-1 py-px text-xs"
        :class="{
            'border-blue-500 text-blue-500': tag === currentTag 
        }"
    >{{ tag }}</button> 
</div>
// apply computed property to filter assignments.
<ul class="border border-gray-600 divide-y divide-gray-600 mt-6">
    <assignment 
        v-for="assignment in filteredAssignments"
        :key="assignment.id" 
        :assignment="assignment"
    ></assignment>
</ul>

// by defualt the current tag will be all.
data() {
    return {
        currentTag: 'all'
    };
},

// when current tag is all then it will return all the data.
// when some other tag is active it will filter tha data by that tag
computed: {
    filteredAssignments() {
        if (this.currentTag === 'all') {
            return this.assignments;
        }

        return this.assignments.filter(a => a.tag === this.currentTag);
    },
}

11-Video (Component Responsibility)

// we passed props as a name initial-tags(kebab case) but recive as a initialTag(camelcase).
//In Vue.js, it's a common convention to use camelCase for prop names in the JavaScript/TypeScript code and kebab-case in the actual template. This is because HTML attributes are case-insensitive and are expected to be in kebab-case.

In your case, you are following this convention. Your prop names in the JavaScript part (initialTags and currentTag) are in camelCase, while in the template, they are used in kebab-case (:initial-tags and :current-tag).

This is the standard naming convention in Vue.js and helps maintain consistency throughout your application.
<assignment-tags
    :initial-tags="assignments.map(a => a.tag)" 
    :current-tag="currentTag"
    @change="currentTag = $event"
></assignment-tags>

props: {
    initialTags: Array,
    currentTag: String
},


// here we make an event and listen it in parent
<button
    @click="$emit('change', tag)"
    v-for="tag in tags" 
    class="border rounded px-1 py-px text-xs"
    :class="{
        'border-blue-500 text-blue-500': tag === currentTag 
    }"
>{{ tag }}</button> 
</div>  

// here in parent we listen to the event of @change and assign $event (which is called magic event it have the calue which is passed in this ievent). and assign it to currentTag which is in data.

<assignment-tags
    :initial-tags="assignments.map(a => a.tag)" 
    :current-tag="currentTag"
    @change="currentTag = $event"
></assignment-tags>

data() {
    return {
        currentTag: 'all'
    };
},

12-Video (A Deeper Look at V-Model)

// In this video we just lern about the backend of v-model.
// and also update data of parent component in child component with help of v-model.

// it will work reactive both accepting and recieving (mean binding and listen to it when changed)
<input type="checkbox" v-model="name" class="ml-3">

// but it will not as reactive if you change from data it will change but when you change in input it will not change in data.
<input type="checkbox" :value="name" class="ml-3">

// it will work reactively. bascially it is the long term of v-model are it is the backend of v-model.
<input type="checkbox" :value="name" @input="name = $event.target.value">

data() {
    return {
        name: ''
    }
},

// old code
// here we pass current tag data in props and then we change and create an event and then listen it in parent and teh change value of current tag in data.

// parent code
<assignment-tags
    :initial-tags="assignments.map(a => a.tag)" 
    :current-tag="currentTag"
    @change="currentTag = $event"
></assignment-tags>

data() {
    return {
        currentTag: 'all'
    };
},

// child code
<button
    @click="$emit('change', tag)"
    v-for="tag in tags" 
    class="border rounded px-1 py-px text-xs"
    :class="{
        'border-blue-500 text-blue-500': tag === currentTag 
    }"
>{{ tag }}</button> 
</div>  

props: {
    initialTags: Array,
    currentTag: String
},

<!-- end old code -->

<!-- start new code -->

// new code with defualt v-model name modelValue
// we did'nt pass any value just pass current tag in v-model and then we can recieve it in props by name 'modelValue' (which is by default name)
// we can also update that model value in child component like we did it here 
// @click="$emit('update:modelValue', tag)"
// when the button is click it will update model value.
// so we update data of parent component in child component with the help of v-model

// parent code
<assignment-tags
    v-mogdel="currentTag"
    :initial-tags="assignments.map(a => a.tag)" 
></assignment-tags>

data() {
    return {
        currentTag: 'all'
    };
},

// child code
<button
    @click="$emit('update:modelValue', tag)"
    v-for="tag in tags" 
    class="border rounded px-1 py-px text-xs"
    :class="{
        'border-blue-500 text-blue-500': tag === modelValue 
    }"
>{{ tag }}</button> 

props: {
        initialTags: Array,
        modelValue: String
    },

// new code with custom v-model name current tag.
// here we assign name to v-model 'currentTag' like this v-mogdel:currentTag="currentTag"
// we will use this name in child component.
// in recieving in props.
// in updateing we will use the name instead of @click="$emit('update:currentTag', tag)"
// we did'nt pass any value just pass current tag in  

// parent code
<assignment-tags
    v-mogdel:currentTag="currentTag"
    :initial-tags="assignments.map(a => a.tag)" 
></assignment-tags>

data() {
    return {
        currentTag: 'all'
    };
},

// child code
<button
    @click="$emit('update:currentTag', tag)"
    v-for="tag in tags" 
    class="border rounded px-1 py-px text-xs"
    :class="{
        'border-blue-500 text-blue-500': tag === currentTag 
    }"
>{{ tag }}</button> 

props: {
        initialTags: Array,
        currentTag: String
    },

13-Video (Lifecycle Hooks, Fake APIs, and AJAX)

1.we will make fake api with a tool called json server.
2.lifecycle hooks.
3.Ajax

// install json-server by this command.
npm install json-server --save-dev

// make a file with name db.json and paste the data
{
    "assignments": [
      {
        "name": "Finish project",
        "complete": false,
        "id": 1,
        "tag": "math"
      },
  
      {
        "name": "Read chapter 4",
        "complete": false,
        "id": 1,
        "tag": "science"
      },
  
      {
        "name": "Turn in homework",
        "complete": false,
        "id": 1,
        "tag": "math"
      },
  
      {
        "name": "Finish Laracasts video",
        "complete": true,
        "id": 1,
        "tag": "programming"
      }
    ]
  }

// run this command and it will run the server which will show you the fake api. then you can fetch data from it.
npx json-server db.json

// you can change the server port like this.
npx json-server db.json -p 3001

// life cycle hooks.
// when vue project is rendered then hook will be called by this priority. and these hook have the same name of functions. so we will called its function.
1.beforeCreate()
2.create()
3.beforeMount()
4.mounted()
5.beforeUnmount
6.unmount

// so if we called some data from api or database we will call it in created method.
// we are feching data from api by fetch() method.
// fetch work on promiss.
// promiss mean it will say if i get these data i will give it.
// we will pass a request then call .then it mean when fetch have data then give me that response.json() in response.
// and when we have it then give me this data in assigmnets and we will pass it to assigmnets in data and the we are good to go.
// we can also use axios.

created() {
    fetch('http://localhost:3001/assignments')
        .then(response => response.json())
        .then(assignments => {
            this.assignments = assignments;
        });
},

14-Video (More Flexible Components With Slots and Flags)

// we can serve vue project through this command.
npx serve

// we cun run our database by this command
npx json-server db.json -p 3001

but we can also added these commands to sctipt then we can just run by one command
{
  "scripts": {
    // if there is only one & then it means that run these sommands simultaneously.
    "start": "npx serve & npx json-server db.json -p 3001"
    // if there is two ends then it means that when one command is completed then run the other
    "start": "npx serve && npx json-server db.json -p 3001"
  },
  "devDependencies": {
    "json-server": "^0.17.4"
  }
}

// child component
<section v-show="assignments.length" class="w-60">
    <slot></slot>
</section> 

// parent component
whatever we past in between these component it will go to the slot
<assignment-list :assignments="filters.inProgress" title="In Progress">
    <assignment-create @add="add"></assignment-create> 
</assignment-list>



