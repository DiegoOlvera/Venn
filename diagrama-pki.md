```mermaid
graph TD
    %% FASE 1: Emisión del Certificado
    A[Inicio: Solicitud de Certificado Digital] --> B[Validación de Identidad por la RA]
    B --> C[Emisión del Certificado X.509 por la AC / CA]
    C --> D[Asociación del Certificado al Usuario en IntegraRH Cloud]

    %% FASE 2: Firma del Documento
    D --> E[Elaboración de Contrato / Expediente Laboral]
    E --> F[Generación del Hash SHA-256 del Documento]
    F --> G[Firma Digital: Cifrado del Hash con Clave Privada]
    G --> H[Empaquetado PAdES con Sello de Tiempo TSA]
    H --> I[Almacenamiento en Repositorio Inmutable]

    %% FASE 3: Validación y Verificación
    I --> J[Solicitud de Verificación de Autenticidad]
    J --> K[Recálculo del Hash del Documento en Repositorio]
    K --> L{¿Coincide el Hash Actual con el Original?}

    %% Escenario de Rechazo 1: Alteración del documento
    L -- No --> M[RECHAZO 1: Documento Modificado / Integridad Rota]

    L -- Sí --> N[Consulta del Estado del Certificado: OCSP / CRL]
    N --> O{¿El Certificado está Vigente y No Revocado?}

    %% Escenario de Rechazo 2: Certificado vencido o revocado
    O -- No --> P[RECHAZO 2: Certificado Expirado, Suspendido o Revocado]

    O -- Sí --> Q[Descifrado de la Firma con la Clave Pública]
    Q --> R{¿La Firma Corresponde al Titular?}

    %% Escenario de Rechazo 3: Firma no válida
    R -- No --> S[RECHAZO 3: Firma Inválida / Autenticidad No Comprobada]

    R -- Sí --> T[ÉXITO: Documento Válido, Íntegro y con Plena Validez Legal]
