# Angular routing

[source](https://angular.io/tutorial/toh-pt5)

- [add to existing app](#addtoexisting)

# <a name="addtoexisting"></a> Set up in an existing App
To add routing to an angular app use:
```
ng generate module app-routing --flat --module=app

(--flat puts the file in src/app instead of its own folder.)
(--module=app tells the CLI to register it in the imports array of the AppModule.)
```

A file "src/app/app-routing.module.ts" should have been created:

```ts
//generated file: "src/app/app-routing.module.ts"

import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

@NgModule({
  imports: [
    CommonModule
  ],
  declarations: []
})
export class AppRoutingModule { }
```

# Add a costum route to app
To show the component "HeroesComponent" on [...url...]/heroes add the following lines

```ts
const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];
```
which then results in (pay attention to the changes in @NgModules aswell!):

```ts
//updated file: "src/app/app-routing.module.ts"

import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HeroesComponent } from './heroes/heroes.component';

const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

# Display router outlet at a specific location in the app
Add the "\<router-outlet\>\<\/router-outlet\>" tag to an html component
```html
<!--src/app/app.component.html-->
<h1>{{title}}</h1>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

# Links
To add a link which navigates to a certain path add the following:
```html
<!--src/app/app.component.html-->
<h1>{{title}}</h1>
<nav>
  <a routerLink="/heroes">Heroes</a>
</nav>
<router-outlet></router-outlet>
<app-messages></app-messages>
```

#Default route
Set up a default path in the routing module

```ts
//updated file: "src/app/app-routing.module.ts"

... imports

const routes: Routes = [
  { ... other routes },
  { path: '', redirectTo: '/heroes', pathMatch: 'full' },
];

@NgModule({
  ...
})
export class AppRoutingModule { }
```

# Add Link and route with parameters
## Setup a route with a parameter
```ts
//updated file: "src/app/app-routing.module.ts"
...
const routes: Routes = [
  { ... other routes },
  { path: 'detail/:id', component: HeroDetailComponent },
];
...
```
## Add a link with parameter
```html
<a *ngFor="let hero of heroes"
  routerLink="/detail/{{hero.id}}">
  {{hero.name}}
</a>
```

## read out id from url
```ts
//class body...
constructor(
  private route: ActivatedRoute,
  private heroService: HeroService,
  private location: Location
) {}

//updated file: "src/app/hero-detail/hero-detail.component.ts"
ngOnInit(): void {
  this.getHero();
}

getHero(): void {
  const id = Number(this.route.snapshot.paramMap.get('id'));
  this.heroService.getHero(id)  //not described here!
    .subscribe(hero => this.hero = hero);
}
// /class-body
```
