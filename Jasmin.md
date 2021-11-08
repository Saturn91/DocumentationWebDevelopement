# Unit Tests for Jasmin
This section was created with references to an angular project, but I'm sure the general part can also be used in othe rprojects

# Installation and setup
Projects which are created with angular cli do already contain tests. To run them enter 
```
ng test
```

# Create Test for a simple Math service
Seel bellow a simple function which we would like to test
```ts
//math.service.ts

export function add(a: number, b: number): number {
  return a + b;
}
```
Now for the test
```ts
//math.service.spec.ts --> spec.ts at the ned is mandatory!

import { add } from './math.service';

describe('math.service.ts', () => {
  // define inputs:
  let number1: number;
  let number2: number;

  // before each test (described in an it-function) this function gets called
  beforeEach(() => {
    // we reset the two inputs after each test so we can be sure the value does not get altered (no side effects!)
    number1 = 731;
    number2 = 577;
  });

  // define first test
   it('should add up two numbers', () => {
    expect(add(number1, number2)).toEqual(1308);
  });

  // define second test
   it('should add up numbers no mather the order', () => {
    expect(add(number2, number1)).toEqual(1308);
  });

  // you can also expect several conditions in one it function
   it('should pass random tests', () => {
    for (let i = 0; i < 10; i++) {
      const num1 = Math.random() * Number.MAX_SAFE_INTEGER;
      const num2 = Math.random() * Number.MAX_SAFE_INTEGER;
      expect(add(num1, num2)).toEqual(num1 + num2);
    }
  });
});
```
# Run the test
Enter "ng test" in your projects terminal
```
ng test
```
After all tests have run you should get a message like bellow displayed of corse the number depends on the numbers of tests you have specified. If you would only have the example above it should be 3.
```
...
TOTAL: 60 SUCCESS
```
