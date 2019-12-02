# Actions

los actions son todos las posibles acciones que se pueden ejecutar 

ej :
    - Cargar data
    - Agregar 
    - Editar
    - Borrar
    - etc....

# Creacion de actions

 - dentro de la aplicacion de ejemplo en la el archivo customers/state/customer.actions.ts
```js
import { Action } from '@ngrx/store'
import { Customer } from '../customer.model'

// Enumerable con las posibles acciones , de esta forma da un manejo fuertemente tipado
export enum CustomerActionTypes{
    LOAD_CUSTOMERS = "[Customer] Load Customers",
    LOAD_CUSTOMERS_SUCCESS = "[Customer] Load Customers Success",
    LOAD_CUSTOMERS_FAIL = "[Customer] Load Customers Fail"
}

/*
* lo siguiente son cada una de las clases con las posibles propiedades que manejara cada accion
*/

export class LoadCustomers implements Action{
    readonly type = CustomerActionTypes.LOAD_CUSTOMERS
}

export class LoadCustomersSuccess implements Action{
    readonly type = CustomerActionTypes.LOAD_CUSTOMERS_SUCCESS

    constructor(public payload: Customer[]){}
}

export class LoadCustomersFail implements Action{
    readonly type = CustomerActionTypes.LOAD_CUSTOMERS_FAIL

    constructor(public payload: string){}
}


/*
* Se exportan todas las posibles acciones a ejecutar en un solo tipo Action
*/
export type Action = LoadCustomers
                | LoadCustomersSuccess
                | LoadCustomersFail;
```


- Ahora dentro se creara la interface con el estado de nuestra aplicacion 

app/state/app-state.ts

```js
export interface AppState{}

```


# Crear Reducer 

- Lo primero sera crear una interface con las propiedades del Customer State
y luego la interface del state del customer

- customers/state/customer.reduce.ts
```js
import * as customerActions from './customer.actions';
import { Customer } from "../customer.model";
import * as fromRoot from "../../state/app-state";


export interface CustomerState{
    customers: Customer[],
    loading: boolean,
    loaded: boolean,
    error: string
}

export interface AppState extends fromRoot.AppState{
    customers : CustomerState
}
```

- El siguiente paso sera crear la funcion reducer que se encargara de recibir el estado  del objeto 
y la action que debe ejecutar

```js

// Estado inicial
export const initialState: CustomerState = {
    customers: [],
    loading: false,
    loaded: false,
    error: ""
}

export function customerReducer(state = initialState, action: customerActions.Action): CustomerState{

    // Segun el tipo de accion retorna el stado
    switch (action.type) {
        case customerActions.CustomerActionTypes.LOAD_CUSTOMERS:{
            /**
             * El siguiente codigo es igual a 
             *  
             *      state.loading = true;
             *      return state:
             */
            return {
            ...state,
            loading: true
            } 
        }

        case customerActions.CustomerActionTypes.LOAD_CUSTOMERS_SUCCESS:{
            return{
                ...state,
                loading: false,
                loaded: true,
                customers: action.payload
            }
        }

        case customerActions.CustomerActionTypes.LOAD_CUSTOMERS_FAIL:{
            return{
                ...state,
                customers: [],
                loading: false,
                loaded: false,
                error: action.payload
            }
        }
    
        default:{
            return state;
        }
    }
}

```