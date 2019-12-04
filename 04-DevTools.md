# DevTools 

- Para hacer debug de nuestra aplicacion cuando se utiliza redux , podemos instalar en nuestro navegador
la extension de Redux DevTools

- Adicionalmente tambien se debe configurar en la aplicacion de la siguiente manera 

    1. Instalar paquete

            $ npm i @ngrx/store-devtools

    2. Añadir a los imports del app-module
        ```js
            import { StoreDevtoolsModule } from "@ngrx/store-devtools";

        @NgModule({
        declarations: [
            ...
        ],
        imports: [
            BrowserModule,
            AppRoutingModule,
            HttpClientModule,
            StoreModule.forRoot({}),
            EffectsModule.forRoot([]),
            // despues de las configuraciones del store
            StoreDevtoolsModule.instrument(),
            ...
        ],
        ```
