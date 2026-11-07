# Diagramas de Flujo – Listas de Precios Personalizadas

Complemento del Documento de Alcance Funcional (sección 2.4, RN-010 a RN-015). Los diagramas están en Mermaid.

## 1. Diagrama de estatus

Muestra todos los estatus de una lista, las transiciones permitidas y quién las ejecuta.

```mermaid
stateDiagram-v2
    state "Capturada" as CAP
    state "Pendiente Aprobar Dirección" as PAD
    state "Aprobada Dirección" as AD
    state "Pendiente Aprobar Cliente" as PAC
    state "Aprobada Cliente" as AC
    state "Autorizada" as AUT
    state "Cancelada" as CAN
    state "No Autorizada" as NA

    [*] --> CAP : Gestor crea la lista
    CAP --> PAD : Gestor envía a Dirección
    PAD --> AD : Autorizador registra aprobación
    AD --> PAC : Gestor envía al Cliente
    PAC --> AC : Autorizador registra aprobación
    AC --> AUT : Permiso especial autoriza
    AUT --> [*]

    PAD --> CAP : Autorizador registra aprobación con cambios
    PAC --> CAP : Autorizador registra aprobación con cambios

    PAD --> NA : Autorizador
    PAC --> NA : Autorizador
    AC --> NA : Permiso especial

    CAP --> CAN : Gestor
    PAD --> CAN : Gestor
    AD --> CAN : Gestor
    PAC --> CAN : Gestor
    AC --> CAN : Gestor

    CAN --> CAP : Gestor reactiva
    NA --> CAP : Gestor reactiva
```

Notas:

* *Autorizada* es el único estatus final. Para cambiar una lista autorizada se crea una nueva versión.
* La lista solo puede modificarse en *Capturada*. Al regresar a *Capturada*, las aprobaciones anteriores dejan de ser válidas y el proceso reinicia desde Dirección.
* Cada cambio de estatus se registra en la bitácora: fecha, usuario, estatus anterior, estatus nuevo y comentario opcional.

## 2. Diagrama de proceso por roles

Muestra quién hace cada paso. Dirección y el Cliente responden por correo, fuera del sistema; los Autorizadores registran su respuesta.

```mermaid
flowchart TD
    subgraph GES["Gestor de Listas"]
        G1["Crea o corrige la lista<br/>(Capturada)"]
        G2["Cambia a Pendiente Aprobar Dirección<br/>y envía la lista por correo a Dirección"]
        G3["Cambia a Pendiente Aprobar Cliente<br/>y envía la lista por correo al Cliente"]
        G4{"¿Reactivar la lista?"}
    end

    subgraph DIR["Dirección (fuera del sistema)"]
        D1{"Respuesta de Dirección"}
    end

    subgraph CLI["Cliente (fuera del sistema)"]
        C1{"Respuesta del Cliente"}
    end

    subgraph AUTZ["Autorizadores"]
        A1["Registra Aprobada Dirección"]
        A2["Registra Aprobada Cliente"]
        A3["Registra aprobación con cambios<br/>(regresa a Capturada)"]
        NA["No Autorizada"]
    end

    subgraph PERM["Usuario con permiso de Autorización Final"]
        P1{"Revisión final"}
        P2(["Autorizada<br/>Fin del ciclo"])
    end

    G1 --> G2 --> D1
    D1 -- "Aprueba" --> A1 --> G3 --> C1
    D1 -- "Aprueba con cambios" --> A3
    D1 -- "No autoriza" --> NA

    C1 -- "Aprueba" --> A2 --> P1
    C1 -- "Aprueba con cambios" --> A3
    C1 -- "No autoriza" --> NA

    P1 -- "Autoriza" --> P2
    P1 -- "Rechaza" --> NA

    A3 --> G1
    NA --> G4
    G4 -- "Sí" --> G1
    G4 -- "No" --> FIN(["Permanece No Autorizada"])

    CANC["En cualquier momento antes de Autorizada,<br/>el Gestor puede cancelar la lista (Cancelada).<br/>Una lista Cancelada puede reactivarse a Capturada."]
    GES -.- CANC
```
