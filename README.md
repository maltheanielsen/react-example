# react-example
Learn React 

Terminal/Powershell kommandoer:

      ls (list files and directories)
      cd (change directory)
      cd .. (gå tilbage)

      npx create-react-app hello-world (opretter et projekt med navnet hello-world)
      code . (åbner nuværende folder i VS code)
      npm start (for at starte serveren og køre React projekt)
      ctrl + c (lukke serveren ned)

React projekt - foldere I skal arbejde i:
  - public (til billeder eller andre assets)
  - src
  --- App.js (den fil I skal arbejde i)
  --- components (ny folder I skal lave til jeres komponenter)

Oprettelse af komponent i /components:
1. Opret filen (fx Nav.js)
2. Tilføj function med return og en export, så andre kan tilgå den

        function Nav(){
          return(
            <nav>
              <div>Hej fra Nav</div>
            </nav>
          )
        }

        export default Nav;

3. Brug dit komponent i App.js
    - Tilføj en import
   
          import Nav from './components/Nav.js';
          
    - Brug dit komponent sådan her:

          <Nav />
          
    - Hvis, der er flere komponenter, så skal de alle være under et element. Sådan her:
   
          function App(){
            return(
              <>
                <Nav />
                <div className="App">
                  <p>Hello, world</p>
                </div>
              </>
            )
          }
        
# Styling

Metode 1: Inline CSS

    <nav style={{padding: '150px', color: 'green'}}>
    
Metode 2: CSS objects

    const navStyle = {
      padding: '200px 0',
      backgroundColor: '#fff',
      color: '#333'
    }

    const borderStyle = {
        border: "1px solid green",
    }

    function Nav(){
        return(
            <nav style={navStyle}>
                <h1 style={borderStyle}>Hej fra navbar</h1>
            </nav>
        )
    }
        
Metode 3: Stylesheet
  1. Opret et stylesheet og kald den fx Nav.css
  2. Importere den:
  
    import styles from './Nav.css';
    
# react-router-dom

1. Installer react-router-dom:

        npm install --save react-router-dom
  
2. Importere følgende til din nav bar

        import {
          BrowserRouter as Router,
          Switch,
          Route,
          Link
        } from "react-router-dom";
  
3. Tilføj Router component med Link og Switch

        function Nav() {
          return (
            <Router>
              <Link to="/">Home</Link>
              <Link to="/about">About</Link>
              <Switch>
                <Route exact path="/">
                  <Homepage />
                </Route>
                <Route path="/about">
                  <About />
                </Route>
              </Switch>
            </Router>
          );
        }

Under Route tilføjer du den komponent du vil have vist, når man trykker på linket. Her kalder jeg Homepage-komponentet og About-komponentet.

# React class

Ligesom function(al) components har React også class components. Brug dem - medmindre, at din komponent "kun" skal præsentere noget.
En class component nedarver fra React.Component og derfor skal både React importeres og 'extends' til - og nå, den kræver også en render() metode for at returnere HTML'en:

      import React from 'react';

      class Sjov extends React.Component{
          render(){
              return(
                  <>
                      <h1>Hej fra class component</h1>
                 </>
              )
          }
      }

      export default Sjov;
  
# Props og States
      
Både props og states er objekter der gemmer på information, men alligevel er de forskellige:
- States bruges i et komponent (svarer til lokale variabler)  
- Props giver man med til sine komponenter (svarer til parameter i en funktion)

Eksempel med state, hvor vi skifter værdien:

      constructor(){
              super(); //Giver adgang til alle "parents" funktioner
              this.state = {car: 'audi'};
          }
          render(){
              return(
                  <>
                      <h1>Hej fra min {this.state.car}</h1>
                      <button onClick={() => this.setState({car: 'mercedes'})}>Klik mig</button>
                 </>
              )
          }

Eksempel med probs, hvor vi sender en værdi med når vi kalder komponentet:
Her kalder vi vores komponent:

      <Person name="Malthe"/> 
         
Sådan ser vores class component ud:

import React from 'react';

      class Person extends React.Component{
          render(){
              return(
                  <h1>Hej fra {this.props.name}</h1>
              )
          }
      }

      export default Person;
         

# Map

Vi kan bruge map() når vi vil løbe vores lister igennem.

I dette eksempel opretter jeg en liste og gør værdierne til list items

      import React from 'react';

      class Car extends React.Component{
          state = {
              cars: ["bmw", "audi", "mercedes"]
          }

          render(){
              return(
                  <>
                      <h1>Hej fra leg</h1>
                      <ul>{this.state.cars.map(car =>
                          <li>{car}</li>
                      )}</ul>
                  </>
              )
          }
      }

      export default Car;

Vi returnerer den på følgende måde

# Objekter

       state = {
            cars: [
                  {
                        name: 'audi',
                        color: 'grey',
                        engine: 'tfsi'
                  },
                  {
                        name: 'mercedes',
                        color: 'green',
                        engine: 'tdi'
                  }
            ]
       }
       
De mappes igennem på følgende måde:

      <ul>{this.state.cars.map(car => (
         <li>{car.name}, {car.color}, {car.engine}</li>
      ))}</ul>

# API (Axios)

      npm install axios

Import: 

      import axios from 'axios';

Brug Axios i componentDidMount(). Alt i den metode bliver kørt EFTER komponentet er indlæst.

      componentDidMount(){
        axios.get("https://jsonplaceholder.typicode.com/users")
        .then(result => {
            this.setState({names: result.data});
        })
      }
      
Brug map til at render det med:

      <ul>{this.state.names.map(name => (
         <li>{name.name}</li>
      ))}</ul>

# Bootstrap

Installer Bootstrap med npm:

      npm install bootstrap
      
Import det i enten app eller index

      import 'bootstrap/dist/css/bootstrap.min.css';
      
Brug følgende classes for at gøre det responsivt: container -> row -> col-xx-x (fx col-md-3). (Tip: Hver række skal give 12)

# Læg din app på en server

Byg din app:

      npm run build
      
Læg indholdet fra build-mappen på din server. Nemt!

Obs - hvis problemer skulle opstå:

Subfolder:

Tilføj følgende til package.json

  },
  "homepage": "https://web-mcdm.dk/[mappenavn]"
}

      
