# React routing

based on [source](https://reactrouter.com/docs/en/v6/examples/basic)
stackblitz [link](https://stackblitz.com/github/remix-run/react-router/tree/main/examples/basic?file=src/App.tsx)

1. create App ```create-react-app <app-name> --template typescript```
2. check if app is running as expected ```cd <app-name> && yarn start```
3. Add router dom ```yarn add react-router-dom```

The bellow code is a modification of the code sandbox and in my eyes the minimum...

I suggest to organize the project as follows:

--src
  |--main.tsx
  |--app.tsx (ass shown bellow but function Home and so one are replaced by HomeModule...
  |--app.router.tsx --> all routes
  |--modules
  |   |--HomeModule
      |    |--components
      |    |     |--EyeCatcher.component.tsx
      |    |--services
      |    |     |--services for only the home module
      |    |--HomeModule.tsx -> main layout of home
      |    |--HomeModule.routes.tsx -> subroutes of home
      |--common
           |--services 
           |    |--services which get used globaly
           |--components
           |    |--globaly used components (like header)
           |--reducers
           |    |--globaly used reducers

main.tsx
```TS
ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter> <-- add this here and import
      <App />
    </BrowserRouter> <-- add this here and import
  </React.StrictMode>,
  document.getElementById("root")
);
```

app.tsx
```TS
import * as React from "react";
import { Routes, Route, Outlet, Link } from "react-router-dom";

export default function App() {
  return (
    <div>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/dashboard">Dashboard</Link>
          </li>
          <li>
            <Link to="/nothing-here">Nothing Here</Link>
          </li>
        </ul>
      </nav>

      <Routes>
        <Route path="/">
          <Route index element={<Home />} />
          <Route path="about" element={<About />} />
          <Route path="dashboard" element={<Dashboard />} />

          <Route path="*" element={<NoMatch />} />
        </Route>
      </Routes>
    </div>
  );
}

function Home() {
  return (
    <div>
      <h2>Home</h2>
    </div>
  );
}

function About() {
  return (
    <div>
      <h2>About</h2>
    </div>
  );
}

function Dashboard() {
  return (
    <div>
      <h2>Dashboard</h2>
    </div>
  );
}

function NoMatch() {
  return (
    <div>
      <h2>Nothing to see here!</h2>
      <p>
        <Link to="/">Go to the home page</Link>
      </p>
    </div>
  );
}
```
