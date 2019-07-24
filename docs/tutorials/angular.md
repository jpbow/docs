---
id: angular-tutorial
title: Angular Tutorial
sidebar_label: Angular
---

# Angular Tutorial

## Overview
Bit enables you to share components and sync their source code between different projects that reside in different repositories. 
In this tutorial we will share an angular component between two projects. 

### Prior Knowledge
This tutorial assumes that you are familiar with: 

- Terminal and command line 
- Using node and npm (or yarn)
- Angular development and the Angular CLI
- Git


### What you need?

In order to run this tutorial you need two projects to share the component between. The first project is an angular store (see below) and the other one will be a newly created angular project.

To run this tutuorial, clone and setup the angular store project: https://github.com/teambit/angular-store-tutorial
```bash
git clone https://github.com/teambit/angular-store-tutorial
cd angular-store-tutorial
npm install
```

### What will you learn?  
In this tutorial you will learn how to:
- Setup Bit
- Share an angular component from an existing project
- Preview the exported component on the Bit cloud
- Install the component in another project
- Modify the Angular component on the new project
- Update the changed component in the original project

## Setup Bit  

First things first, we need to setup Bit.

### Create a Bit Cloud account 
head over to the Bit cloud(https://bit.dev/) and create your account. Enter a username and password or use your github credentials. 
**Welcome to Bit!**
Please remember your username, you will need it later in this tutorial. 

### Create a Bit Collection
When you are logged into Bit Cloud you can create a collection. The collection is a group of components that are related and can be shared with others. Components in public collections are visible to everyone, while components in private collection are only available to invitees.

Click on the collections icon on the left pane and create a new collection from the top right **New** button. Name the new collection `Tutorial`, and make it private for now. 
You can create a public collection that will be visible for everyone, or a private one, visible to you and your invitees.

### Install Bit Cli

Install Bit cli on your computer using npm:
```bash
npm install bit-bin -g
```  
(If you would like to use other installation methods, please visit: [Install Bit](/docs/installing-bit.html))
If you have already installed Bit, please verify the installation by running the following command:
```bash
$ bit --version
```

### Login into your Bit Account
Now you need to log into your bit account, from the command line run
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
Now go into the angular store project you cloned before and switch to the repository.
while you are inside the repository run the bit initialization command:
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

## Share an Angular Component 

### Track a new component
We are going to track the product-list component from the angular project.
The component will be tracked with the id `product-list`.

You need to tell Bit about the component and the files that are related to it. As all the files are located under the product-list directory, the simple way is to add all the files in the product-list directory to our component. 
There are two more things you need to tell Bit: 

 - The Id of the component that we are tracking
 - The file in the directory which is the entry point to the component. In our case, this is the `product-list.component.ts` file. Here is the full command:
```bash
bit add src/app/product-list/*.* --id product-list --main src/app/product-list/product-list.module.ts
```
You should expect to see the following message from Bit: 
```bash
tracking component product-list:
added src/app/product-list/product-list.component.css
added src/app/product-list/product-list.component.html
added src/app/product-list/product-list.component.ts
```
When creating new components, we need to make sure that we have properly added all the files that are required for the component. Bit can analyze the component for you and verify that all files are included. You can do that by checking the status of the component: 
```bash
bit status
```
Our component is using the `src/app/products.ts` file and Bit will identify the missing file: 
```bash
> product-list ... issues found
untracked file dependencies (use "bit add <file>" to track untracked files as components):
src/app/product-list/product-list.component.ts -> src/app/products.ts
```
You will need to add the missing file to the component:
```bash
bit add src/app/products.ts --id product-list
```
>  In this case, this file is used only by the product-list component so you can add it to the product-list component. In other cases, however, if this file is used by multiple components, you may want to consider creating `products.ts` file as a separate component that will become a dependancy of other components. 

Now you can run the status command again. Bit shows you that all the used files are properly tracked: 
```bash
> app/product-list ... ok
```
### Install Angular Compiler
So far, you have provided bit with the source file of the component. But in order to consume the files in other projects, the component needs to be built. In this case, it should be compiled by the Angular compiler. 
>Bit is storing the source code of the component, but the code should still remain in your version control system (VCS) such as your Git repository. 

Bit has a large collection of compilers that are open sourced and maintained By the Bit team. In addition, the community is also suggesting compilers that you can use by searching Bit collections. 
For building the angular component, you will need the [angular compiler](link //ToDo). This compiler is based on ng-packagr, which is the tool used by Angular CLI to bundle packages to npm. 
To install the compiler run this command inside the angular repository: 
```bash
bit import  --compiler //ToDo
```
An affirmative message will display that the compiler is installed: 
```bash
The following component environments were installed
ToDo
```
  The angular compiler will now be set as the default compiler for the Bit workspace inside this repository. You can check the package.json and verify that the compiler is installed by locating the following entry in the Bit section: 
```json
//Todo
```
### Build Angular Component
Now that the compiler is installed, you want to build the component. Building the component serves two purposes: 
- Making the component directly consumable by other projects
- Making sure that the component is all-inclusive and contains all the parts that are required in order to share it with others 
Right now the component lives inside your project and may consume some dependencies from your project. 
Bit build is taking place in an isolated environment (nicknamed "capsule"), so it will make sure the component build will succeed on the cloud or in any other project. 
To build the component, run this command inside your angular project: 
```bash
$ bit build product-list
```
We should recieve the following message: 
```bash
/ToDo
```
This is good. Your component was built. 

### Export Component
With the component properly built, it is now time to share it with the world.  
Components are versioned according to sematic versioning guidelines. To tag your component run the following command: 
```bash
bit tag --all 1.0.0
```
This command will tag all the components that are currently staged in Bit. In our case, it is only product-list.  //ToDo

```bash
1 components tagged | 1 added, 0 changed, 0 auto-tagged
added components: ui/button@0.0.1
```
You can also check the status of the component (`bit status`) and you will find the following: 
```bash
staged components
> product-list. versions: 0.0.1... ok
```
The important thing to notice here is that the component is considered `staged`. That means that it is now ready to be exported. 

To export the component to your collection use the export command. Specify the name of your collection in the following structure: <username>.<collection>: 
```bash
$ bit export <username>.tutorial
```
On successful execution the following message will be displayed: 
```bash
exported 1 components to scope wonderwoman.diana
```

The component is now visible on your collection on the bit.dev cloud. 

Checking the status of the component, will no longer display the component as it is now hosted on the remote collection: 

```bash
nothing to tag or export
```

The code however, is still available locally. Also, the component is now available for other projects. 
 

## Preview the Angular Component 

You can now go to `https://bit.dev` and log into your account (if you are not logged in yet). 
Select the collections navigator on the left panel and select collections. 
Click on your collection and you will see your compoent product-list. 
You can now click on the product-list and see the component playground. 


## Install Component in Another Project

### Create a New Angular Application

You are now going to create another angular application and use the product-list component. The fastest way to do that is use the Angular CLI to generate a new Application. 

If you already have the Angular-cli installed globally you can just run
```bash
ng new angular-inventory
```
If you do not have the angular-cli installed globally and you do not want to install it, you can use [`npx`](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b) to install it temporarily: 
```bash
npx --package @angular/cli ng new angular-inventory
```
In your terminal, switch to the `angular-inventory` directory. 

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
     > <tuko>.angular-vue-tutorial/product-list@1.0.1
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
- updated tuko.bit-vue-tutorial/product-list new versions: 1.0.1 
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
