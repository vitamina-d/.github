# 🧬 Vitamina-D
[![Main Repo](https://img.shields.io/badge/Project-Main_Readme-green?style=for-the-badge)](https://github.com/orgs/vitamina-d/repositories)

Este documento sirve como **punto de entrada central** de los repositorios que conforman Vitamina-D, una aplicación web para el análisis de datos genómicos.

---

## 📋 Descripción

Plataforma web de bioinformática que integra herramientas especializadas para el análisis de secuencias genómicas y estructuras proteicas. Desarrollada con una arquitectura de microservicios contenedorizados, permite investigar variaciones genéticas y su relación con condiciones como el raquitismo mediante:

- 🔍 Búsqueda de homología con BLAST
- 🧬 Traducción de secuencias y análisis genómico
- 🔬 Predicción de estructuras 3D de proteínas
- 📊 Comparación estructural y alineamiento
- 📈 Visualización interactiva de datos

## 🎓 Objetivos del Proyecto Académico

1. Desarrollar una aplicación web para análisis de datos genómicos
2. Implementar un backend que integre servicios bioinformáticos
3. Analizar genes relacionados con el metabolismo de la vitamina D

## 🎯 Caso de Estudio

El proyecto surge de la necesidad de investigar el **raquitismo** históricamente prevalente en poblaciones no originarias que colonizaron la Patagonia austral (s. XIX-XX), pero ausente en poblaciones originarias. La plataforma facilita el estudio de variaciones genéticas en genes relacionados con el metabolismo de la vitamina D (VDR, CYP27B1, CYP24A1, etc.) y su impacto en la salud ósea.

## 🏗️ Arquitectura del Sistema

Arquitectura de microservicios orquestada con Docker Compose:

```
   ┌───────────────────────────────────────┐
   │           Frontend (React)            │
   │        http://localhost:5173          │
   └─────────────────┬─────────────────────┘
                     │ HTTP/REST
                     ▼
   ┌───────────────────────────────────────┐
   │      Backend API (ASP.NET Core)       │
   │        http://localhost:8081          │
   └───┬────────┬────────┬───────────┬─────┘
       │        │        │           │
       │        │        │           │
       ▼        ▼        ▼           ▼
   ┌──────┐ ┌───────┐ ┌──────┐  ┌──────────┐
   │ bioc │ │ blast │ │ bio  │  │ External │
   │ (R)  │ │  (R)  │ │python│  │   APIs   │
   │ 8000 │ │ 8001  │ │ 8002 │  └─┬────────┘
   └──────┘ └───────┘ └──────┘    └ Ensembl
                                  └ NCBI
                                  └ UniProt
                                  └ NeuroSnap
```

## 🎯 Componentes Principales

### Frontend - [bioc_front](https://github.com/vitamina-d/bioc_front)
**React + TypeScript + Vite** | Puerto: `5173`
- Interfaz web interactiva con Bootstrap
- Visualización 3D con 3Dmol.js
- Gráficos con Plotly.js
- Notificaciones y loaders

### Backend - [bioc_back](https://github.com/vitamina-d/bioc_back)
**ASP.NET Core 8.0** | Puerto: `8081`
- Orquestador central de servicios internos
- Arquitectura en capas (Clean Architecture)
- Integración con APIs externas (Ensembl, NCBI, UniProt, NeuroSnap)
- Documentación Swagger

### Bioconductor - [bioc_r](https://github.com/vitamina-d/bioc_r)
**R + Plumber** | Puertos: `8000` (API), `8787` (RStudio)
- Análisis genómico con Bioconductor
- Genoma humano hg38 (BSGenome)
- Alineamiento de secuencias
- Estadísticas nucleotídicas

### BLAST - [bioc_blast](https://github.com/vitamina-d/bioc_blast)
**R + BLAST+** | Puerto: `8001`
- BLASTx contra SwissProt
- Búsqueda de homología

### BioPython - [biopython](https://github.com/vitamina-d/biopython)
**Python + FastAPI** | Puerto: `8002`
- Traducción de secuencias
- Cálculo de reverso/complemento
- Alineamiento estructural (RMSD)

## 🚀 Inicio Rápido

### Instalación

1. **Clonar los repositorios**

```bash
mkdir vitamina-d-project
cd vitamina-d-project

git clone https://github.com/vitamina-d/bioc_back.git
git clone https://github.com/vitamina-d/bioc_front.git
git clone https://github.com/vitamina-d/bioc_r.git
git clone https://github.com/vitamina-d/bioc_blast.git
```

2. **Estructura de directorios**

```
vitamina-d/
├── bioc_back/
├── bioc_front/
├── bioc_r/
└── bioc_blast/
```

3. **Iniciar los servicios**

```bash
cd bioc_back
docker-compose up -d
```

### Acceder a los Servicios

| Servicio | URL | Descripción |
|----------|-----|-------------|
| **Frontend** | http://localhost:5173 | Interfaz web principal |
| **Backend API** | http://localhost:8081 | API REST |
| **Swagger** | http://localhost:8081/swagger | Documentación API |
| **Bioc R API** | http://localhost:8000 | Servicios Bioconductor |
| **BLAST API** | http://localhost:8001 | Servicio BLAST |
| **BioPython API** | http://localhost:8002 | Servicios Python |

## 🔧 Stack Tecnológico

**Frontend**: React 19, TypeScript, Vite, Bootstrap, Plotly.js, 3Dmol.js  
**Backend**: ASP.NET Core 8.0, C#  
**Análisis**: R 4.4, Bioconductor 3.20, Python 3.13, BioPython  
**Bases de datos**: SwissProt (BLAST), BSGenome hg38  
**APIs externas**: Ensembl, NCBI E-utilities, UniProt, RCSB PDB, NeuroSnap  
**Infraestructura**: Docker, Docker Compose

## 📚 Documentación

Cada componente tiene documentación detallada en su repositorio:
- [📖 Frontend](https://github.com/vitamina-d/bioc_front#readme) - Vistas, componentes y servicios
- [📖 Backend](https://github.com/vitamina-d/bioc_back#readme) - Arquitectura y endpoints
- [📖 Bioconductor](https://github.com/vitamina-d/bioc_r#readme) - Análisis genómico en R
- [📖 BLAST](https://github.com/vitamina-d/bioc_blast#readme) - Búsqueda de homología

---

<div align="center">

**Universidad Nacional Arturo Jauretche**  
Proyecto Integrador Profesionalizante (PIP)  
_Florencio Varela, Buenos Aires, Argentina | 2025_ 


[🏠 Repositorios](https://github.com/orgs/vitamina-d/repositories) | [📖 Documentación](https://github.com/vitamina-d/doc)

</div>
