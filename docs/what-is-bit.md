---
id: what-is-bit
title: Introduction
---

Teams which scale code-sharing and code reuse between projects and developers enjoy faster development cycles and simpler maintenance for their codebase.

Bit is [open source tool](https://github.com/teambit/bit) that helps you easily publish and manage reusable components. It help teams scale shared components to hundreds and even thousands of components, while eliminating the overhead around this process.

On top of this, Bit provides enhanced discoverability for shared components so every developer can easily find and choose the code they need. It also increases the adoption of shared components by removing the concerns around their consumption and usage.

Bit can be used to share code between apps and teams, as a power tool for publishing and managing multiple components in a single repository, and for organizing a reusable component collection for your team and community.

**Common use cases**:

* **[Bit for teams](/whybit/for-teams.html)**
* **[Bit for libraries](/whybit/for-libs.html)**

## Advantages of using Bit

**Easily managing and publishing hundreds of components** from multiple libraries and apps with 0 overhead and no refactoring. [Learn more](/whybit/for-teams.html#publishing-and-managing-components-at-any-scale-without-overhead)

**Gaining discoverability for shared components** so that every developer can easily find and choose the components they need. [Learn more](/whybit/for-teams.html#increasing-discoverability-of-shared-components)

**Increasing the adoption of shared components** by removing the main barriers and encouraging collaboration. [Learn more](/whybit/for-teams.html#increasing-adoption-and-usage-for-shared-components)

​## Get started
​
The best way to get started with Bit is to jump in, [sign-up to bit.dev](https://bit.dev/signup), and create your first collection. Then, [follow this tutorial](/docs/quick-start.html) to share your components. Within a short time you will create a collection of reusable components exported from your project (no refactoring needed), which can now be shared and reused.
​
For any questions, don’t hesitate to [reach out to the team](https://bit.dev/support) or chat with us [on Gitter](https://gitter.im/bit-src/Bit). You can also check out [Bit on GitHub](https://github.com/teambit/bit).

**Examples**

**[React components](https://bit.dev/components?labels=react)**
**[React Buttons](https://bit.dev/components?labels=button)**
**[Animations](https://bit.dev/components?labels=animation)**
**[Javascript utils](https://bit.dev/components?labels=utils)**

## Philosophy

Composing components with well-defined responsibilities is a long-lived principle for writing better, more scalable and simpler to maintain software.

Today, the technologies we build with enable better composition than ever before. [Encapsulated and reusable components]((https://addyosmani.com/first/)) with focused APIs are the building blocks of the software we build. From [Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) and UI components ([React](https://reactjs.com), [Vue](https://vuejs.org/), [Angular](https://angular.io) etc) to reusable [Node.js modules](https://nodejs.org/api/modules.html), utility functions, GraphQL APIs and even serverless functions, these components are our building blocks.

Bit is designed to help teams scale the sharing and management of components to hundreds and even thousands of components.

It provides powerful yet simple isolation, discoverability and reuse for these components. It takes care of the components’ entire lifecycle from development to deployment so that your team can share and manage any number of components at any scale.
​
## What is a Bit component?
​
A Bit component is an encapsulated piece of code (set of files) which should handle a single responsibility, representing a well-defined functionality and composable with other components to build larger things.

Technically, a Bit component is a set of files tracked in a project. For each component Bit calculates a dependency graph and creates an isolated component environment that wraps the component, making it isolated and reusable. Bit tracks the component across the different projects it’s used in so that it can help update and sync changes to components.
