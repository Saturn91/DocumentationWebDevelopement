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

# Read private variable within class
```ts
it('should private property "id" should have value "saturn91"', () => {
  expect(myClass['id'].toBe('saturn91');
});
```

# Inject Angular services and override them
As you do testing of Angular components you might have to inject services like your database service which in you app would actually call the backend. Something which should not be done during automated testing! To avoid such time consuming test behaviour and to make sure any failing test is caused by the component it is testing and not by external elements (decoupeling!) you can inject mockup classes instead of the real ones.

## Identify what services you have to inject.
Lets look at an example component of one of our current projects
```ts
@Component({
  selector: 'app-learn',
  templateUrl: './learn.component.html',
  styleUrls: ['./learn.component.scss']
})
export class LearnComponent implements OnInit {

  private id = '';
  public stack: undefined | IndexCardStack = undefined;

  constructor(
    private route: ActivatedRoute,
    private stackStorageService: StackStorageService
  ) { }

  ngOnInit(): void {
    this.id = this.route.snapshot.queryParams.id;
    this.stackStorageService.getDocument(this.id).then((stack: IndexCardStack) => {
      this.stack = stack;
    });
  }
}
```
You can see in the constructor there are to external services passed as parameters. In angular this means that the are provided in the module or in the root. If we want to decouple our test we have to mockup those two services. 

## Lets look at what we have to replace:
we find 4 relevant lines in ngInit in which methodes and properties of this provided services are used:
```ts
this.id = this.route.snapshot.queryParams.id;
this.stackStorageService.getDocument(this.id).then((stack: IndexCardStack) => {
  this.stack = stack;
});
```
So we want to controll the value and behaviour of this methodes and properties during the test. Lets do that

## create mockup classes
What we will actually do is to replace the two identified classes with so called mockup classes. This are a barebones fassade of the real classes but deliever the data and behaviour we need during the test.
The two beloow specified classes will do that during our test. Notice that they only provide the functions and properties which we actually need in this specific test. For mor sufisticated services alternativly you could extend the original class and override the needed function or implement a interface which represents the original class.
```ts
describe('LearnComponent', () => {
  let component: LearnComponent;
  let fixture: ComponentFixture<LearnComponent>;

  class MockupAuthService {
      public snapshot = {
        queryParams: {
          id: 'test'
        }
      };
    }
    class MockupStorage {
      public getDocument(id: string): Promise<IndexCardStack> {
        return new Promise((resolve) => {
          resolve(new IndexCardStack([], new IndexCardStackMetaData('', '', '', id, StackVisibility.Undef, '')));
        });
      }
    }
    
    [...]
}
```

Finally we have to tell the Angular component to actually use this Mockup classes instead of the original ones
```ts
describe('LearnComponent', () => {
  let component: LearnComponent;
  let fixture: ComponentFixture<LearnComponent>;

  class MockupAuthService {
   [...]    
  }
  class MockupStorage {
     [...]
  }
    
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ LearnComponent ],
      providers: [
        { provide: ActivatedRoute, useClass: MockupAuthService},
        { provide: StackStorageService, useClass: MockupStorage}
      ]
    })
    .compileComponents();
  });
  
  [...]
}
```
Now we can run our tests and se if it works
