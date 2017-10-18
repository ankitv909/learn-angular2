---
layout: default
title: Outputs
edit_link: https://github.com/ionic-team/learn-angular2/edit/gh-pages/outputs/index.md
tweet: "Emit your own crazy events with Outputs in Angular 2"
---

If you want to bind to particular event, you can use the new [Event syntax](/events) in Angular 2, but what if you need your own custom event?

To create a custom event, we can use the new `@Output` decorator. Take the following component:

```javascript
{% raw %}
import { Component } from '@angular/core';

@Component({
  selector: 'user-profile',
  template: '<div>Hi, my name is {{user.name}}</div>'
})
export class UserProfile {
  constructor() {}
}
{% endraw %}
```

Let's import `Output` and `EventEmitter` and create our new event

```javascript
{% raw %}
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'user-profile',
  template: '<div>Hi, my name is {{user.name}}</div>'
})
export class UserProfile {
  @Output() userUpdated = new EventEmitter();

  constructor() {
    // Update user
    // ...
    this.userUpdated.emit(this.user);
  }
}
{% endraw %}
```

Now when we used this component in its parent component, we can bind the event that `user-profile` emits

```html
{% raw %}
  <user-profile (userUpdated)="handleUserUpdated($event)"></user-profile>
{% endraw %}
```

```javascript
{% raw %}
export class SettingsPage {
  constructor(){}

  handleUserUpdated(user) {
    // Handle the event
  }
}
{% endraw %}
```
