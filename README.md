# trace
TypeScript decorator to trace method calls using https://github.com/visionmedia/debug

## Usage
The `Trace` decorator can be used for a class as well as for a method.

### Decorating a class:
```ts
import { Trace } from "@aiteq/trace";

@Trace()
class User {
  constructor(public name: string) { }
  
  public getName(): string {
    return this.name;
  }
  
  public toString(): string {
    return this.getName();
  }
}

console.log(new User("Honza").toString());
```
The output would look like this:
```
> DEBUG=* node ./dist/trace-test.js

  TRACE => User.toString() +0ms
  TRACE => User.getName() +5ms
  TRACE <= User.getName: Honza +6ms
  TRACE <= User.toString: Honza +7ms
Honza
```

### Decorating a method:
```ts
import { Trace } from "@aiteq/trace";

class User {
  constructor(public name: string) { }
  
  @Trace()
  public getName(): string {
    return this.name;
  }
  
  public toString(): string {
    return this.getName();
  }
}

console.log(new User("Honza").toString());
```
The output would look like this:
```
> DEBUG=* node ./dist/trace-test.js

  TRACE => User.getName() +0ms
  TRACE <= User.getName: Honza +5ms
Honza
```

### Notes
The ouput will be colorized by `debug`.

Tracing doesn't work for constructor.
