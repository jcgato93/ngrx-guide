# Entity

Adaptador de estado de entidad para gestionar colecciones de registros.

Entity proporciona una API para manipular y consultar colecciones de entidades.

1. Reduce las repeticiones para crear reductores que gestionan una colección de modelos.

2. Proporciona operaciones CRUD eficaces para gestionar colecciones de entidades.

3. Adaptadores extensibles de tipo seguro para seleccionar información de entidad.


# Implementación

- En customers/state/customer.reducer.ts

```js
import { EntityState, EntityAdapter, createEntityAdapter } from "@ngrx/entity";

// Reemplazar del ejemplo anterior
export interface CustomerState extends EntityState<Customer>{
    selectedCustomerId: number | null,
    loading: boolean,
    loaded: boolean,
    error: string
}


export interface AppState extends fromRoot.AppState{
    customers : CustomerState
}

export const customerAdapter:EntityAdapter<Customer> = createEntityAdapter<Customer>();

export const defaultCustomer: CustomerState = {
    ids: [],
    entities: {},
    selectedCustomerId: null,
    loading: false,
    loaded: false,
    error: ""
}

export const initialState = customerAdapter.getInitialState(defaultCustomer);


//....
// Reemplazar
 case customerActions.CustomerActionTypes.LOAD_CUSTOMERS_SUCCESS:{
            return customerAdapter.addAll(action.payload, {
                ...state,
                loading: false,
                loaded: true
            })
        }

//....
// Reemplazar
case customerActions.CustomerActionTypes.LOAD_CUSTOMERS_FAIL:{
            return{
                ...state,
                entities: {},
                loading: false,
                loaded: false,
                error: action.payload
            }
        }        


// dentro del mismo archivo se cambia por lo siguiente uno de los selectors

// Selectors de propiedades especificas que se necesitan
export const getCustomers = createSelector(
    // feature
    getCustomerFeatureState ,

    //propiedad especifica que queremos obtener
    customerAdapter.getSelectors().selectAll
)
```