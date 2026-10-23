# Catálogo de Datos — Rumbo a Casa

**Rumbo a Casa** es una propuesta desarrollada para el **MAD Open Data Challenge 2026**, organizado por la Universidad Carlos III de Madrid en colaboración con la Comunidad de Madrid. Aprovechando los portales de datos abiertos tanto de la Comunidad como del Ayuntamiento de Madrid, hemos diseñado una aplicación de rutas peatonales inteligentes y más seguras, priorizando calles principales bien iluminadas y la cercanía a puntos de refugio y asistencia abiertos (como farmacias de guardia, comisarías u hospitales con urgencias).

La iniciativa busca que cualquier persona que camine sola de noche lo haga con mayor tranquilidad y respaldo, sabiendo con certeza qué equipamientos están operativos a su alrededor ante cualquier eventualidad. Si bien la herramienta no sustituye a los servicios de emergencias (112), proporciona una capa preventiva crucial: aporta visibilidad del entorno, permite compartir la ubicación en tiempo real con contactos de confianza y emite avisos automáticos si no se llega a casa en el tiempo estimado.

En este directorio se documentan y ponen a disposición los conjuntos de datos empleados en el proyecto, sirviendo como catálogo de referencia central para el equipo, la comunidad investigadora y colaboradores interesados en reproducir o ampliar los análisis.

---

## 1. Datasets Procesados y Exportados (`data/exports/`)

Los ficheros en `data/exports/` son conjuntos de datos consolidados, limpios y georreferenciados, listos para ser consumidos en Sistemas de Información Geográfica (**QGIS**, ArcGIS), pipelines de análisis de datos (**Python / Pandas / GeoPandas**) o aplicaciones web.


### Sistemas de Coordenadas de Referencia (CRS)
- **EPSG:4326 (WGS 84)**: Coordenadas geográficas estándar (`lon`, `lat`), empleadas en los ficheros `.geojson` y coordenadas web.
- **EPSG:25830 (ETRS89 / UTM zone 30N)**: Sistema métrico proyectado oficial en España y Madrid (`x_25830`, `y_25830`), utilizado para cálculos euclídeos precisos de distancias e iluminación.

---

### 1.1. `pois` (Puntos de Interés / Refugios de Seguridad)
- **Ficheros**:
  - `data/exports/pois.csv` 
- **Descripción**: Red unificada de puntos de apoyo y refugio ciudadano: farmacias (guardia y ordinarias), comisarías de policía, parques de bomberos y hospitales con urgencias médicas continuadas.


---

### 1.2. `lighting_points` (Puntos de Alumbrado Urbano / Farolas)
- **Ficheros**:
  - `data/exports/lighting_points.csv` 
- **Descripción**: Censo georreferenciado punto por punto de unidades luminosas en vía pública y parques urbanos de Madrid (Almendra Central y distritos extendidos).

---

### 1.3. `segments` (Tramos de la Red Peatonal)
- **Ficheros**:
  - `data/exports/segments.csv` 
- **Descripción**: Topología de red caminable construida a partir de OpenStreetMap, limpiada, dirigida y enriquecida con atributos de seguridad e infraestructura vial.

---

## 2. Datos Originales Crudos con Carpeta (`data/raw/`)

En `data/raw/` se preservan los ficheros originales descargados de los portales institucionales de datos abiertos para garantizar trazabilidad y reproducibilidad.

A continuación se detallan las carpetas estructuradas:

### 2.1. `data/raw/Farmacias/`
- **Archivos**:
  - `214440-3-farmacias-guardia-csv.csv`: Catálogo municipal de farmacias de guardia de Madrid.
  - `oficinas_farmacia_comunidad.csv`: Registro oficial completo de todas las oficinas de farmacia autorizadas de la Comunidad de Madrid.
  - `farmacias_chamberi_corregidas.csv`: Fichero de auditoría con validación manual de coordenadas y horarios para el distrito piloto de Chamberí.
  - `LEEME.MD`: Ficha técnica de descarga.
- **Fuente**: [Portal de Datos Abiertos del Ayuntamiento de Madrid — Farmacias de Guardia](https://datos.madrid.es/dataset/214440-0-farmacias-guardia) / Colegio Oficial de Farmacéuticos de Madrid (COFM).
- **Licencia**: Creative Commons Attribution 4.0 International (CC BY 4.0).
- **Propósito**: Base para alimentar la red de farmacias nocturnas y de guardia como puntos de refugio prioritarios.

---

### 2.2. `data/raw/alumbrado_calles/`
- **Archivos**:
  - `300573-0-unidades-luminosas-farolas.csv.csv`: Censo municipal exhaustivo de unidades luminosas en vía pública de Madrid (~23.7 MB).
  - `LEEME.MD`: Ficha técnica y definiciones del área de alumbrado del Ayuntamiento de Madrid.
- **Fuente**: [Portal de Datos Abiertos — Unidades Luminosas (Farolas)](https://datos.madrid.es/dataset/300573-0-unidades-luminosas-farolas).
- **Licencia**: CC BY 4.0.
- **Detalle Conceptual**:
  - **Unidad Luminosa**: Soporte físico que proporciona luz con independencia del número de luminarias (p. ej., un báculo con sodio a calzada y globo LED para acera es 1 unidad).
  - **Tipología (`tipol`)**: `LED` (todas las luminarias son LED), `DESCARGA` (sodio/vapor de mercurio/halogenuros antiguos) o `LED-DESCARGA` (mixta).
  - Georreferenciadas con el callejero municipal en coordenadas UTM ETRS89 huso 30N.

---

### 2.3. `data/raw/alumbrado_parques/`
- **Archivos**:
  - `300582-0-unidades-luminosas-farolas--csv.csv`
  - `300582-2-unidades-luminosas-farolas--csv.csv`
  - `300582-6-unidades-luminosas-farolas--csv.csv`
  - `LEEME.MD`: Ficha técnica.
- **Fuente**: [Portal de Datos Abiertos — Farolas en Parques Singulares](https://datos.madrid.es/dataset/300582-0-unidades-luminosas-farolas-).
- **Licencia**: CC BY 4.0.
- **Propósito**: Complementar el censo de alumbrado de viales con las farolas instaladas en el interior de parques públicos históricos y zonas verdes protegidas.

---

### 2.4. `data/raw/bomberos/`
- **Archivos**:
  - `211642-3-bomberos-parques-csv.csv`: Relación de los parques del Cuerpo de Bomberos del Ayuntamiento de Madrid.
  - `LEEME.MD`: Ficha técnica.
- **Fuente**: [Portal de Datos Abiertos — Parques de Bomberos](https://datos.madrid.es/dataset/211642-0-bomberos-parques).
- **Licencia**: CC BY 4.0.
- **Propósito**: Representar instalaciones públicas de emergencia con presencia permanente 24h/365d como puntos seguros de resguardo.

---

### 2.5. `data/raw/callejero/`
- **Archivos**:
  - `200075-1-callejero-csv.csv`: Censo municipal oficial de viales y numeraciones postales de Madrid (~96 MB).
  - `LEEME.MD`: Ficha técnica.
- **Fuente**: [Portal de Datos Abiertos — Callejero Vigente](https://datos.madrid.es/dataset/200075-0-callejero).
- **Licencia**: CC BY 4.0.
- **Contenido**: Más de 10.000 viales y 200.000 portales con coordenadas métricas oficiales, cruces de viales y códigos postales. Sirve de geocodificador maestro y validación de nombres de vía.

---

### 2.6. `data/raw/comisarías/`
- **Archivos**:
  - `300600-2-comisaria-csv.csv`: Directorio municipal georreferenciado de comisarías de policía.
  - `LEEME.MD`: Ficha técnica.
- **Fuente**: [Portal de Datos Abiertos — Comisarías](https://datos.madrid.es/dataset/300600-0-comisaria).
- **Licencia**: CC BY 4.0.
- **Contenido**: Comisarías de Policía Nacional (atención 24h), Unidades Integrales de Distrito de Policía Municipal y Oficinas de Atención al Ciudadano (OAC).

---

### 2.7. `data/raw/hospitales/`
- **Archivos**:
  - `LEEME.MD`: Documentación detallada del criterio de integración y catálogo de hospitales en Chamberí.
  *(Nota: El archivo de datos base municipal se encuentra en la raíz de `raw/`: `212769-0-atencion-medica-csv.csv`)*.
- **Fuente**: [Portal de Datos Abiertos — Atención Médica](https://datos.madrid.es/dataset/212769-0-atencion-medica).
- **Licencia**: CC BY 4.0.
- **Centros Integrados con Urgencias Médicas Continuadas (24h)**:
  1. *Hospital Universitario HM Madrid* (Plaza del Conde del Valle de Súchil, 16)
  2. *Hospital Universitario La Luz* (Calle del Maestro Ángel Llorca, 8)
  3. *Hospital Universitario Vithas Madrid La Milagrosa* (Calle de Modesto Lafuente, 14)
  4. *Hospital Viamed Santa Elena* (Calle de la Granja, 8)
  5. *Hospital Virgen de La Paloma* (Calle de la Loma, 1)
- **Política de Rigor de Datos**: Al no figurar horario ambulatorio en el catálogo municipal, no se infieren citas médicas previas; se integran exclusivamente como puntos de urgencias sanitarias 24h (`abierta_24h = True`, `horario_estado = 'sin_datos'`).

---


## 3. Principios y Políticas de Datos

1. **Tolerancia Cero a la Invención de Datos**:
   Si un campo de horario o teléfono no figura en la fuente oficial o no está verificado en terreno, se almacena como `null` o `sin_datos`. Jamás se simulan horarios o ubicaciones en una herramienta orientada a la seguridad personal.
2. **Atribución y Licencias**:
   - Datos del Ayuntamiento de Madrid bajo licencia **CC BY 4.0**.
   - Datos viales de la red caminable basados en **OpenStreetMap** (© Colaboradores de OpenStreetMap), bajo licencia **ODbL**.
   - Los datos unificados exportados en `data/exports/` se distribuyen para uso analítico y colaborativo del proyecto Rumbo a Casa manteniendo el respeto a dichas atribuciones.
