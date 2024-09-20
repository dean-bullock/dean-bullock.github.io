---
layout: post
title:  "Signal inputs"
date:   2024-09-18 21:00:00 +0100
categories: angular patterns
---

**Exploring Angular's New Signal Inputs: A Game Changer for Component Communication**

Angular has continuously evolved to meet modern development needs, and with each new release, it introduces features that make it more robust, efficient, and developer-friendly. One of the latest exciting additions to Angular is *Signal Inputs*. This new feature simplifies component communication, making it easier to manage inputs in a reactive, declarative way. Let’s dive into what signal inputs are, why they matter, and how you can leverage them in your Angular applications.

### What Are Signal Inputs?

In Angular, inputs are the primary mechanism for passing data from a parent component to a child component. Traditionally, Angular has relied on `@Input()` decorators to manage input properties in components. While this works well, it can become cumbersome when dealing with complex data flows, especially when reactive patterns are involved.

Signal inputs are part of Angular's shift towards reactive programming by integrating the Signals API introduced in Angular v17. Signals are reactive primitives that automatically track dependencies and re-evaluate when those dependencies change. With signal inputs, Angular allows components to subscribe to reactive signals as input properties, providing a more declarative and reactive way to manage inputs.

### Why Should You Care About Signal Inputs?

Signal inputs offer several benefits:
1. **Declarative Reactivity**: With signals, Angular handles reactivity for you. You define a signal, and Angular ensures the component updates automatically when the signal changes, without manual handling.
2. **Simpler Data Flow Management**: Instead of managing complex subscriptions and change detection manually, signal inputs abstract much of that complexity, allowing you to focus on writing clean and maintainable code.
3. **Improved Performance**: Signals work in a more fine-grained manner than traditional `@Input()` properties. They reduce unnecessary change detection cycles and improve overall application performance.

### How Do Signal Inputs Work?

Let’s look at an example to understand how signal inputs fit into Angular applications.

#### Traditional `@Input()` Approach

Here’s a quick refresher on how we typically pass data from a parent to a child component using the `@Input()` decorator.

{% raw %}

```typescript
// Parent Component
@Component({
  selector: 'app-parent',
  template: `<app-child [message]="parentMessage"></app-child>`,
})
export class ParentComponent {
  parentMessage: string = 'Hello from Parent!';
}

// Child Component
@Component({
  selector: 'app-child',
  template: `<p>{{ message }}</p>`,
})
export class ChildComponent {
  @Input() message = '';
}
```

In this example, the parent passes the `parentMessage` string to the child component via an `@Input()` property.

#### Using Signal Inputs

With signal inputs, Angular replaces this `@Input()` property with a signal that reacts to changes automatically.

```typescript
import { signal, input } from '@angular/core';

// Parent Component
@Component({
  selector: 'app-parent',
  template: `<app-child [message]="parentMessageSignal()"></app-child>`,
})
export class ParentComponent {
  parentMessageSignal = signal('Hello from Parent!');
}

// Child Component
@Component({
  selector: 'app-child',
  template: `<p>{{ message() }}</p>`,
})
export class ChildComponent {
  message = input('');
}
```
{% endraw %}

In this setup, the parent component defines a signal `parentMessageSignal` using Angular's `signal()` function. The child component now receives a readonly signal `input()`, allowing it to reactively update the UI whenever the signal's value changes.

The notable differences are:
- The child component now receives a signal as its input rather than a static property.
- In the template, we call `message()` to access the current value of the signal.

This makes signal inputs more suitable for applications where data is likely to change frequently and where reactivity is a priority.

### Key Benefits of Using Signal Inputs

1. **Automatic Dependency Tracking**: Signals automatically track dependencies and trigger re-evaluation when any input changes. This reduces the manual effort of managing subscriptions or relying on `ngOnChanges` to detect changes.
2. **Cleaner Code**: By abstracting away the intricacies of reactivity, signal inputs lead to cleaner, more concise code. Developers can focus on logic and UI rather than worrying about the intricacies of change detection.
3. **Built-in Efficiency**: Angular's reactivity with signals is optimized for performance. With a more targeted reactivity model, signal inputs ensure that only the necessary components re-render, reducing the performance overhead seen with larger-scale change detection cycles.

### Wrapping Up

Angular's new signal inputs mark a significant improvement in how developers manage input properties within components. By embracing a more reactive, declarative approach, signal inputs make component communication simpler, more maintainable, and better suited for complex data flows.

As Angular continues to evolve, the introduction of signal inputs is another step toward making modern web development faster and more efficient. So, if you're already working with Angular, now is the time to experiment with signals and bring a fresh level of reactivity to your projects.

**Have you started using signal inputs in your Angular applications? If not, what feature are you most excited to explore in Angular's latest release?**