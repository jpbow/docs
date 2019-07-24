---
id: vue-tutorial
title: Vue Tutorial
sidebar_label: Vue
---
## Overview
Bit enables you to easily share and sync code components between different projects in different repositories.

In this tutorial we will share (and sync) a single Vue component between two projects. 

### Prior Knowledge
This tutorial assumes that you are familiar with: 

- Terminal and command line 
- Using node and npm
- Vue development and the Vue CLI
- Git

### What will you need?
In order to run this tutorial you need two projects to share the component between. The first project is a Vue shop (see below) and the other one will be a newly created Vue project.

To run the tutorial, clone and setup the vue shop project: 
https://github.com/teambit/bit-vue-tutorial
```bash
git clone https://github.com/teambit/bit-vue-tutorial
cd bit-vue-tutorial
npm install
```
![](https://i.imgur.com/xvhXRv6.png)

### What will you learn?  

In this tutorial you will learn how to:
- Setup Bit
- Share a Vue component from an existing project
- Preview the exported component on Bit.dev
- Install the component in another project
- Modify the Vue component on the new project
- Update the changed component in the original project

## Setup Bit  

First things first, we need to setup Bit.

### Create a Bit Cloud account 
Head over to [Bit.dev](https://bit.dev/) and create your account. Enter a username and password or use your GitHub credentials. 
**Welcome to Bit!**
Please remember your username, you will need it later in this tutorial. 

### Create a Bit Collection
Now that you're logged in, the 'Create a Collection' option is available to you. A collection is a group of related components that can be shared with others. Components in public collections are visible to everyone, while components in private collection are only available to invitees.

Click on the **Collections** icon on the left pane and create a new collection from the top right **New** button. Name the new collection `Tutorial`, and make it private for now. 
You can create a public collection that will be visible for everyone, or a private one, visible to you and your invitees.

### Install Bit Cli

Install Bit cli on your computer using npm:
```bash
npm install bit-bin -g
```  
(If you prefer a different package manager, please visit: [Install Bit](/docs/installing-bit.html)).
If you have already installed Bit, please verify the installation by running the following command:
```bash
$ bit --version
```

### Login into your Bit Account
Log into your bit account from your command line
```bash
bit login
```
This will open your browser and will login into your account. You are now ready to start using Bit.
As part of the login process, Bit will setup your local configuration. You can see your configuration by typing:
```bash
bit config
```
In addition, Bit will add the npm registry used by Bit to your npmrc configuration (by default located in `~/.npmrc`).


### Initialize Bit Workspace

Run the Bit initialization command inside your cloned project's root directory:
```bash
bit init
```
You should recieve a message stating:
```
successfully initialized a bit workspace.
```
Two other changes will happen:   
- A new file will be created named `.bitmap` in your root directory. This file is tracking bit components and it will only include a comment and a line with your bit version.
- A new section `bit` will be added to your `package.json` file setting the following defaults for your project:
```json
"bit": {
	"env": {},
	"componentsDefaultDirectory": "components/{name}",
	"packageManager": "npm"
}
```

> These changes should be commited into your version control tool.

## Share a Vue Component 

### Track a New Component
We will track the ProductList component in the Vue project.

You need to tell Bit about the component's entry point and the files that are related to it (if there are any).

Here is the full command:

```bash
bit add src/components/ProductList.vue
```
(In this case, there's no need to explicitly mention the entry point since there's only a single file.)

You should expect to see the following message from Bit: 
```bash
tracking component product-list:
added src/components/ProductList.vue
```
When creating new components, we need to make sure that we have properly added all the files that are required for it. Bit can analyze the component for you and verify that all files are included. You can do that by checking the status of all tracked components: 
```bash
bit status
```
Our component is using the `src/assets/products.js` - Bit will identify it and alert us: 

```bash
> product-list ...  issues found       
       untracked file dependencies (use "bit add <file>" to track untracked files as components): 
          src/components/ProductList.vue -> src/assets/products.js
```
You will need to add the missing file to the component:

```bash
bit add src/assets/products.js --id product-list
```


In this case, this file is used only by the product-list component so you can add it as a dependency. In other cases, however, if this file is used by multiple components, you may want to consider creatin a `products.vue` file as a separate component that will then become a dependancy of others. 

You can run the status command again. Bit shows you that all the tracked files are properly tracked: 

```bash
> product-list ... ok
```
### Install a Vue Compiler
Capsuling components together with their compilers gives us the freedom to use, build and test them anywhere. This includes being able to run the code in any other future-project, as well as running it in the cloud, to enable features such as the live component playground. 

Bit stores the source code of the component, but the code should still remain in your version control system (VCS) such as your Git repository. 

Bit has a large collection of compilers that are open sourced and are maintained by Bit team. In addition, the community has also contributed many compilers that you can find by searching through Bit's collections.

To build the vue component, you will need the [Vue compiler](https://bit.dev/bit/envs/bundlers/vue).

To install the compiler run this command inside the angular repository: 
```bash
bit import bit.envs/bundlers/vue --compiler
```
An affirmative message will display that the compiler is installed: 
```bash
the following component environments were installed
- bit.envs/bundlers/vue@2.5.0  
```
The Vue compiler is now set as the default compiler for the Bit workspace inside this repository. You can check the package.json and verify that the compiler is installed by locating the following entry in the Bit section: 
```json
  "bit": {
    "env": {
      "compiler": "bit.envs/bundlers/vue@2.5.0"
    },
```
### Build the Vue Component
Now that the compiler is installed we can build the component. 

To build the component, run this command inside your Vue project: 
```bash
$ bit build product-list
```
You should recieve the following message: 
```bash
.../bit-vue-tutorial/dist/ProductList.js
.../bit-vue-tutorial/dist/products.js
```
Your component was built. 

### Export Component
With the component properly built, it is now time to share it with the world.  
Components are versioned according to semantic versioning guidelines. To tag your component run the following command: 
```bash
$ bit tag product-list 1.0.0

1 component(s) tagged
(use "bit export [collection]" to push these components to a remote")
(use "bit untag" to unstage versions)

new components
(first version for components)
     > product-list@1.0.0
```
You can also check the status of the component (`bit status`) and find the following:

```bash
staged components
> product-list. versions: 0.0.1... ok
```
The important thing to notice here is that the component is considered `staged`. That means that it is now ready to be exported.

You will export the component into your collection using the `export` command. The collection name is built as follow: `<username>.<collection_name`;

```bash
$ bit export <username>.vue-demo
```
On successful execution the following message will be displayed: 

```bash
exported 1 components to scope tuko.vue-demo
```

The component is now visible on your collection on the Bit.dev. 

Checking the status of the tracked components, will no longer display the component, as it is now hosted on the remote collection: 

```bash
nothing to tag or export
```

The code however, is still available locally. Also, the component is now available for other projects. 
 

## Preview the Vue Component 

You can now go to `https://bit.dev` and log into your account (if you are not logged in yet). 
Select the collections navigator on the left panel and select **Collections**. 
Click on your collection and you will see your compoent 'product-list'. 
You can now click on the product-list and see the component playground. 


## Install  Component in Another Project

### Create a New Vue Application

We will now create another Vue application where we will use the product-list component. The fastest way to do that is to use the Vue CLI to generate a new Application. 

If you already have the Vue-cli installed globally you can simply run:
```bash
vue create vue-inventory
```

In your terminal, switch to the `vue-inventory` directory. 

### Install the Component in the New Project  

Now you can use your favorite package installer (npm or yarn) to install the component. 
The component is stored in the Bit registry, so the full path to the component will be: `@bit/<username>.<collection name>.<component name>`
Run the install command using npm:

```bash
$ npm install npm i @bit/<username>.vue-demo.product-list
```
The component is now added to your `package.json`: 
```
"dependencies": {
    "@bit/<username>.vue-demo.product-list": "^1.0.0",
```

### Use In your Application

You can now use the component in your code as an import. 
Add it as a component to the top level app component.

Your app.vue file should look like so:
```vue
<template>
  <div id="app">
    <ProductList />
  </div>
</template>

<script>
import ProductList from '@bit/<username>.bit-vue-tutorial.product-list';

export default {
  name: 'app',
  components: {
    ProductList
  }
}
</script>
```

Last, but not least, run your application:
```bash
npm run serve
```

Voila! you can now see the components list inside the newly created application. 

## Modify Component
Next, we look at the component (in your new project) and decide to make changes.

### Initialize Bit Workspace
First, you need to initialize a new Bit workspace (in your new project's root directory). This is similar to what you did in the demo project. 

```
$ bit init
```

### Import Component
In the previous step, you installed the component into Bit, but you did not import its code into your project. Now, you are going to **import** your 'product-list' component from your collection.

```
$ bit import <username>.tutorial/product-list
```

Once this is completed, the following message should appear:

```
successfully imported one component
- added <username>.tutorial/product-list new versions: 1.0.0, currently used version 1.0.0 
```

Your imported component is now located under a newly created 'components' library (located in your root folder -  not your 'src' folder).

```
├───components
│   ├───product-list
        ├───components
            ├───ProductList.vue
```

### Modify Component's Source code

Open the 'product-list' component in your editor and make add a "View" button next to share "Share" button: 


```vue
<button @click="view">
   View
</button>
```

And the corresponding method to handle the view: 
```vue
view(){
   alert('View!')
}
```

Your component's code after modification will look like this:

```vue
<template>
    <div>
        <h2>Products</h2>
        <template v-for="(product, index ) of products">
            <div v-bind:key={index}> 
                <h3>
                    <a>
                        {{ product.name }}
                    </a>
                </h3>
                <p v-if="product.description">
                    Description: {{ product.description }}
                </p>
                <button @click="share">
                    Share
                </button>
                <button @click="view">
                    View
                </button>
            </div>
        </template>
    </div>
</template>

<script>

import products from '../assets/products';

export default {
  name: 'ProductList',
  data() {
    return {products};
  },
  methods: {
      share(){
          alert('The product has been shared!')
      },
      view(){
          alert('View!')
      }
  }
}
</script>

<style scope>
    button + button {
        margin-left: 10px;
    }
</style>

```
You can run the application to see the change: 
![](https://i.imgur.com/IkmuS9H.png)


### Export the Modified  Component

Now, we are going to export the modified component back to your collection, as a new version, so it will be available for others to use. 
You can do that as you have write permissions to the collection. If this is done by another user that do not have those permissions, they might need to export the component to their own collection. 

As this component was imported by Bit, it is already tracked and handled by Bit. This is why you do not need to `add` the component, also the compiler is already known. 

Tag the modified component as a new version:

```bash
$ bit tag --all
```
You should expect to see:

```bash
1 component(s) tagged
(use "bit export [collection]" to push these components to a remote")
(use "bit untag" to unstage versions)

changed components
(components that got a version bump)
     > eden.bit-vue-tutorial/product-list@1.0.1

```

Export the component to your collection

```bash
$ bit export <username>.<collection>
```

You should recieve the following message:

```
exported 1 components to scope <username>.<collection>
```

## Update the Component in the Original Project
Now that a new version of the component exists, you can import the changes back to the original project. 

### Import Changed Component

Open your original project and run bit import to see if any components were changed (this is similar to doing `git pull` to see if the git repository has any changes).

```basg=h
bit import
```

You will see that the 'product-list' component was changed and a new version exsits: 

```bash
successfully imported one component
- updated eden.bit-vue-tutorial/product-list new versions: 1.0.1 
```

### Checkout
Merge the changes of the component to your project.

```bash
bit checkout latest <username>.<collection>/product-list 
```

Bit will perform a git merge, so the code from the updated component will now be merged into your code. 

You should expect to see:

```bash
successfully switched <username>.<collection>/product-list to version 1.0.1
 
updated src/assets/products.js 
updated src/components/ProductList.vue 

```
Run the application again to see the changes in our component. 

**That's it! You now have the changes in the component.**