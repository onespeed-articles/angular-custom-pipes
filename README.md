# Custom Pipes

### Requirements
All pipes must follow this format:
```javascript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'myCustomPipe'
})
export class MyCustomPipe implements PipeTransform {
  transform(value: string) {
    return value + ' is the best!'
  }
}
```
__Remember:__ _the transform function is not optional_

### Implementation
**You'll need to add your custom pipe to your app module before trying to use it in your templates.** Pipes work inside of your component's template(html). You're even able to run pipes with in angular directives like ngFor. Below is an implementation of the pipe 'myCustomPipe':

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'my-component',
  template: `
    <div>
      <p *ngFor="let fav of favoriteFoods">
        {{ fav | myCustomPipe }}
      </p>
    </div>
  `
})
export class MyComponent {
  favoriteFoods = [
    'Pizza',
    'Ice Cream',
    'Peanutbutter'
  ];
}
```

The first argument is auto passed into your pipe's transform function. In this example, the value being passed will be a string since its the value before the ```|``` operator. Simple... right? Well, this is a very basic implementation of a custom pipe.

### Custom pipe with multiple arguments
```javascript
import { Component, Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'myCustomPipe'
})
export class MyCustomPipe implements PipeTransform {
  transform(value: string[], limit: number) {
    return value.slice(0, limit).map((fav: string) => {
      return fav + ' is the best!'
    })
  }
}

@Component({
  selector: 'my-component',
  template: `
    <div>
      <p *ngFor="let fav of favoriteFoods | myCustomPipe:limit">
        {{ fav }}
      </p>
    </div>
  `
})
export class MyComponent{
  limit = 3;
  favoriteFoods = ['Pizza', 'Ice Cream', 'Peanutbutter', 'Egg', 'Bacon', 'Waffle'];
}
```

As you see above you're able to pass multiple arguments by using the ':' character. As mentioned in the previous exampled, the first agument gets auto passed. This time, the first argument is the entire ```favoriteFoods``` array.

## Conclusion
Pipes are very versitile and can help with minor data minipulation.
