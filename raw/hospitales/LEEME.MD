## DOCUMENTO QUE DEFINE EL CONJUNTO DE DATOS DE ATENCIÓN MÉDICA Y HOSPITALES

# 212769-0-atencion-medica-csv.csv

- **Fuente**: Datos Abiertos del Ayuntamiento de Madrid
- **URL**: https://datos.madrid.es/dataset/212769-0-atencion-medica
- **Fecha de descarga**: 18/10/2026
- **Fecha de actualización del dataset original**: 16 de octubre de 2026
- **Licencia**: Creative Commons Attribution 4.0 International (CC BY 4.0)
- **Formato**: CSV (codificación Latin-1 / ISO-8859-1, delimitador `;`)

### Descripción
Directorio municipal georreferenciado de centros de atención médica de la Ciudad de Madrid. Contiene centros de salud, especialidades, centros de salud mental y hospitales/clínicas/sanatorios.

### Criterio de filtrado e integración en Rumbo a Casa
- **Distrito**: Chamberí (`DISTRITO == 'CHAMBERI'`).
- **Tipo de instalación**: Hospitales, clínicas y sanatorios (`TIPO == '/contenido/entidadesYorganismos/CentrosAtencionMedica/HospitalesClinicasSanatorios'`).
- **Urgencias y disponibilidad**: Integrados como centros de urgencias médicas continuadas (24h) dentro del factor `puntos_ayuda`.
- **Tratamiento de horarios**: El campo `HORARIO` en el archivo origen se encuentra vacío para estos centros; conforme a los principios de rigor de Rumbo a Casa, no se inventan horarios específicos de consulta (`opening_hours: null`, `horario_estado: 'sin_datos'`), manteniéndose abiertos como puntos de refugio y atención sanitaria de urgencia (`abierta_24h: true`).

### Entidades integradas en Chamberí (5 hospitales)
1. **Hospital Universitario HM Madrid** (PK 9136): Plaza del Conde del Valle de Súchil, 16.
2. **Hospital Universitario La Luz** (PK 9155): Calle del Maestro Ángel Llorca, 8.
3. **Hospital Universitario Vithas Madrid La Milagrosa** (PK 9142): Calle de Modesto Lafuente, 14.
4. **Hospital Viamed Santa Elena** (PK 9152): Calle de la Granja, 8.
5. **Hospital Virgen de La Paloma** (PK 9141): Calle de la Loma, 1.
