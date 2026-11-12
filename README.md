# Auto Evaluación de Peligros y Riesgos por puesto de trabajo

Aplicación web de una sola página para que los trabajadores de la **Biblioteca Departamental Jorge Garcés Borrero** identifiquen y califiquen los peligros y riesgos de su propio puesto de trabajo.

Se enmarca en la participación de los trabajadores del **Decreto 1072 de 2015 (art. 2.2.4.6.15)** y usa la metodología **GTC 45** para valorar el riesgo. Es un insumo para la matriz de peligros y valoración de riesgos, que debe ser revisada y validada por el responsable del SG-SST con el COPASST.

## Uso

La aplicación es HTML, CSS y JavaScript puro, sin compilación. Puede abrirse directamente o servirse por HTTP:

```powershell
cd peligros_riesgos_biblioteca
python -m http.server 8080
```

Luego abra `http://localhost:8080`.

## Flujo de trabajo

1. **Datos del trabajador**: nombre, cédula, tipo de vinculación (planta o contratista), área, cargo y descripción del puesto.
2. **Peligros del puesto**: catálogo de peligros biológicos, físicos, químicos, psicosociales, biomecánicos, de seguridad y fenómenos naturales. La app sugiere peligros según el área, el cargo y la descripción, y permite agregar peligros propios.
3. **Calificación GTC 45** de cada peligro marcado:
   - **Deficiencia (ND)**: 2, 6 o 10 según los controles existentes.
   - **Exposición (NE)**: 1 a 4 según la frecuencia.
   - **Consecuencia (NC)**: 10, 25, 60 o 100 según la gravedad.
4. **Resultado automático**:
   - Probabilidad **NP = ND × NE** → Bajo, Medio, Alto o Muy alto.
   - Nivel de riesgo **NR = NP × NC**:
     | NR | Nivel | Aceptabilidad |
     | --- | --- | --- |
     | ≥ 600 | I | No aceptable |
     | 150 – 599 | II | No aceptable o aceptable con control específico |
     | 40 – 149 | III | Mejorable |
     | < 40 | IV | Aceptable |
5. **Autorización** de tratamiento de datos personales (Ley 1581 de 2012) y **guardado** de la autoevaluación.

## Indicadores

- Participación total, de personal de planta y de contratistas (meta: 58 + 80 = 138 personas).
- Peligros identificados y riesgos no aceptables (niveles I y II).
- Peligro más reportado, clasificación predominante y área con más riesgos no aceptables.
- Distribución por nivel de riesgo y por clasificación.
- Interpretación automática de cada indicador.

## Exportaciones

- **Excel (.xlsx)**: hojas *Evaluaciones*, *Trabajadores* e *Indicadores*, con SheetJS.
- **CSV**: detalle de evaluaciones con separador `;` y BOM UTF-8.

## Privacidad y almacenamiento

- Los registros se guardan **solo en el navegador del usuario** (`localStorage`, clave `peligros_reg`).
- No hay servidor ni base de datos central: la información no se envía a ninguna parte.
- Para consolidar los datos de varias personas hay que descargar el Excel o el CSV y unificarlos.
- No se debe usar en equipos compartidos sin borrar los registros al terminar.

## Estructura

```
peligros_riesgos_biblioteca/
├── index.html   # aplicación completa (HTML + CSS + JS)
└── README.md
```

## Enlace publicado

https://o-10.github.io/peligros-riesgos-biblioteca-departamental/
