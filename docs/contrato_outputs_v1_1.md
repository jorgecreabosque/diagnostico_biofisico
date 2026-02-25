## diagnostico_biofisico

Motor automatizado de diagnostico biofisico basado en integracion de datos espaciales, climaticos y edaficos.

El sistema genera insumos cartograficos y metricos estandarizados para soporte tecnico y toma de decisiones.

---

## Objetivo del sistema

Automatizar la generacion de:

- Capas base: DEM, pendiente, indices espectrales y cobertura
- Contexto territorial: AOI, buffer y red hidrica oficial
- Suelos: variables minimas desde SoilGrids
- Clima: climatologia anual y series mensuales
- Diagnostico espacial integrado
- Outputs estandarizados reproducibles

---

## Arquitectura general

```mermaid
flowchart TB

  A[Configuracion del proyecto] --> B[SP1 Inputs]
  B --> C[SP2 Capas biofisicas]
  C --> D[SP3 Diagnostico espacial]
  D --> E[Outputs estandarizados]

  %% SP1 (compacto)
  subgraph SP1_Detalle[SP1 Detalle]
    direction TB
    Bx[Inputs validados]
    Bx --> B1[AOI]
    Bx --> B2[Infraestructura]
    Bx --> B3[Buffer extrapredial]
  end
  B --> Bx

  %% SP2 (compacto en dos columnas)
  subgraph SP2_Detalle[SP2 Detalle]
    direction TB
    Cx[Capas biofisicas]
    Cx --> Ctop[Topografia]
    Cx --> Cespec[Indices espectrales]
    Cx --> Club[Cobertura suelo]
    Cx --> Csoil[Suelos]
    Cx --> Cclim[Clima]
    Cx --> Chyd[Red hidrica]

    %% forzar columnas internas
    Ctop --> Ctop2[DEM y pendiente]
    Cespec --> Cespec2[NDVI NDWI NBR]
    Club --> Club2[LULC]
    Csoil --> Csoil2[SoilGrids]
    Cclim --> Cclim2[CHIRPS y temperatura]
    Chyd --> Chyd2[Red oficial Chile]
  end
  C --> Cx

  %% SP3 (compacto)
  subgraph SP3_Detalle[SP3 Detalle]
    direction TB
    Dx[Diagnostico]
    Dx --> D1[Grilla analisis]
    Dx --> D2[Cruces]
    Dx --> D3[Proximidades]
    Dx --> D4[Score o clasificacion]
  end
  D --> Dx

  %% Outputs (compacto)
  subgraph OUT_Detalle[Outputs Detalle]
    direction TB
    Ex[Entregables]
    Ex --> E1[Rasters]
    Ex --> E2[Vectores]
    Ex --> E3[Tablas]
    Ex --> E4[Graficos]
    Ex --> E5[Logs]
  end
  E --> Ex
```
