# Installación y librerias

        $ npm install @ngrx/store @ngrx/effects @ngrx/router-store @ngrx/entity @ngrx/store-devtools @ngrx/schematics


- store : libreria principal , almacena la informacion
- effects : manejo de eventos para la comunicacion con el back-end
- router-store : para conectar the angular router a ngrx store
- entity : para el manejo de colecciones de objetos
- devtools : permite hacer debug del store 
- schematics : libreria de scaffolding que provee un CLI para generar archivos



# Inicialización del store

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

import { StoreModule } from "@ngrx/store";

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    StoreModule.forRoot({}) // Recibe por parametro el reducer , si no lo tiene recibe un objeto vacio.
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

