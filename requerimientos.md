# SistemasERP - Módulo de Socios de Negocio (Business Partners) en SAP Business One
---
# Diagrama de Flujo Integral de Requerimientos y Procesos

Estructura completa y validación de Socios de Negocio en diagrama:

```mermaid
graph TD
    classDef startNode fill:#2E7D32,stroke:#fff,stroke-width:2px,color:#fff;
    classDef processNode fill:#E65100,stroke:#fff,stroke-width:2px,color:#fff;
    classDef decisionNode fill:#0277BD,stroke:#fff,stroke-width:2px,color:#fff;
    classDef testNode fill:#6A1B9A,stroke:#fff,stroke-width:2px,color:#fff;
    classDef endNode fill:#4A148C,stroke:#fff,stroke-width:2px,color:#fff;

    Start([Inicio: Solicitud de Alta de BP]) --> Tipos[Definir Tipo: Cliente C, Proveedor V o Lead L]:::startNode
    Tipos --> General[Registrar Datos Maestros: CardCode, Nombre, RFC/ID]:::processNode
    General --> Test1{Pruebas Unitarias: ¿CardCode único y campos obligatorios?}:::testNode

    Test1 -->|No| Error1[Bloquear registro y reportar campos faltantes/duplicados]:::processNode
    Error1 --> General

    Test1 -->|Sí| Direcciones[Configurar Múltiples Direcciones y Personas de Contacto]:::processNode
    Direcciones --> Finanzas[Asignar Moneda, Listas de Precios y Cuentas de Mayor]:::processNode
    Finanzas --> DecisionLead{¿Es un Lead?}:::decisionNode

    DecisionLead -->|Sí| Conversion[Convertir Lead a Cliente conservando historial de ofertas]:::processNode
    DecisionLead -->|No| Funcionales[Evaluación Funcional: Límite de Crédito y Estado]:::processNode
    Conversion --> Funcionales

    Funcionales --> Test2{Pruebas Funcionales y Reglas de Negocio}:::testNode
    
    Test2 -->|Socio Bloqueado| Bloqueo[Restringir estrictamente transacciones comerciales]:::processNode
    Test2 -->|Crédito Excedido| Autorizacion[Activar Autorización / Advertencia de Crédito]:::processNode
    Test2 -->|Aprobado| Integridad[Validar Integridad Referencial OCRD y Plan de Cuentas]:::processNode

    Bloqueo --> Fin([Fin del Ciclo / Operación Rechazada]):::endNode
    Autorizacion --> Fin
    Integridad --> Success([Socio Operativo Registrado en OCRD]):::endNode
