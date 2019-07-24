---
id: best-practices
title: Best Practices
---

When you introduce Bit into your team’s toolkit, knowing the basic rules makes it even more useful. We've compiled a list of best practices to help you get the most out of Bit.

## Read through the Getting Started guide

This is a general rule that relates to any new tool. Bit introduces a new type of workflow and some unique concepts that can be new for some developers. The Getting Started guide explains new ideas and concepts.

## Track Meaningful Components

Components should have a [single responsibility](https://en.wikipedia.org/wiki/Single_responsibility_principle). In other words - a component represents a functionality. When tracking files as components, include all files related to that functionality.

## Use Meaningful Namespaces

For better discoverability of components, include as many namespaces as needed. This makes the components easier to discover by other developers. It also helps mitigate component naming collisions.

## Document Components

Include documentation and examples alongside components. This will improve collaboration, and explain to others how to use your code. Use JSDocs, markdown files, and live playground examples.

## Use Component Environments

Code usually requires compilation tasks to make it into a distributable and executable. The same goes for the components in the project. When we take components out of the context of a project, Bit needs to know how to make them usable. Component Environments handle these tasks.

## Prefer Transpiling Over Bundling

Bundled code forces too many restrictions on its consumers. It forces them to include the entire bundle as a single block, dependencies included. Transpiled code gives the consumer more flexibility. It allows dependency tree management features like tree-shaking and code-splitting.

## Don’t Tag Half-Done Work

Tag a new version only when it’s completed. Understand that other developers may consume a version once it's exported. Tagging and exporting half-done work may introduce unwanted behaviors into their work.

## Test Before You Tag

Testing code you distribute is always important. With Bit, you distribute more code. Test your components and include their test files as well. Distributing component tests helps developers to know if their changes modify the component’s behavior. This makes the process of collaborating on components stabler. By the way, test cases also serve as excellent documentation.

## Use SemVer to Communicate Changes

When tagging a new version for a component, use Bit to increment the version. Proper versioning helps other developers understand and predict the side effects of a version. Bit supports this flow with the `-—patch`, `-—minor` and `-—major` flags of the `tag` command.

## Write Good Version Messages

Like a good Git commit message, begin with a summary of the change. Following by a body of the message that should provide details for the motivation of the change.

## Import Often

When working within a team, try and import remote changes for components often. Prefer integrating your work to your team's often to avoid handling larger changes. Importing remote changes often helps mitigate many integration issues.

## Share Often

When you have a small and meaningful version of a component, share it. Small, incremental changes are easier to handle and use by other developers. Sharing often means integrating small changes. This is easier to merge and reduce the chances and severity of merge conflicts.

## Prefer Using Package Managers

Unless you need to change components, prefer installing components using packages managers. This simplifies a project's structure by fetching the code's distribution. Treating components as any other external package simplifies a project's build process as well.

## Prefer Ejecting Sourced Components

Sourcing a component should be temporary. Use this feature for modification purposes. After the modification, tag a new version, share and eject it from the project. Ejecting a component removes the source code from a project, replacing it with a node module.

## Defer From Ejecting Local Components

Ejecting components from their source project is tempting. Ejecting a component from its project complicates the project's maintenance. It turns the component into dependency, and not an integral part of the project. Use `bit import` to sync these components with remote changes.

## Use SCM to Keep Local-Unshareable Modifications

You can source and modify components. Sometimes these changes are project-specific and not meant to be shared. Keep those modifications local and committed to your SCM. Bit can merge incoming changes and keep your modifications.