# trace
TypeScript decorator to trace method calls using https://github.com/visionmedia/debug

## Usage
The `Trace` decorator can be used for classes as well as for methods.

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
- While [decorators](https://www.typescriptlang.org/docs/handbook/decorators.html) are still experimental, you must set `experimentalDecorators` to `true` in your `tsconfig.json`.
- The output is controlled by the `DEBUG` environment variable. All tracing records are prefixed with the `TRACE` string. So for enabling the tracing set the DEBUG variable to e.g. `TRACE` or `*`. See `debug`'s [doc](https://github.com/visionmedia/debug) for details.
- The output will be colorized by `debug`.
- Tracing doesn't work for constructors.
