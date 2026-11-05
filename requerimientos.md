# Gestión de Socios de Negocio (Business Partners) - SAP Business One
---
# Diagrama de Flujo de Requerimientos Funcionales

Estructura y el flujo de los requerimientos funcionales en diagrama:

```mermaid
graph LR
    classDef startNode fill:#2E7D32,stroke:#fff,stroke-width:2px,color:#fff;
    classDef processNode fill:#E65100,stroke:#fff,stroke-width:2px,color:#fff;
    classDef decisionNode fill:#0277BD,stroke:#fff,stroke-width:2px,color:#fff;
    classDef endNode fill:#4A148C,stroke:#fff,stroke-width:2px,color:#fff;

    Start([Inicio: Gestión BP]) --> Tipos[Definir Tipo: Cliente, Proveedor o Lead]:::startNode
    Tipos --> General[Registrar Datos Maestros e Identificación Fiscal]:::processNode
    General --> Direcciones[Configurar Múltiples Direcciones y Contactos]:::processNode
    Direcciones --> Finanzas[Asignar Condiciones de Pago y Listas de Precios]:::processNode
    Finanzas --> Decision{¿Es Lead?}:::decisionNode
    
    Decision -->|Sí| Conversion[Convertir Lead a Cliente manteniendo historial]:::processNode
    Decision -->|No| Validacion[Validar Moneda, Cuentas Asociadas e Impuestos]:::processNode
    
    Conversion --> FinProcess([Socio Operativo en SAP B1]):::endNode
    Validacion --> FinProcess
