# 📊 Análisis E-commerce — Proyecto Final ThePower

## 📖 Descripción
Este proyecto realiza un **análisis completo de un e-commerce**, desde la limpieza y transformación de los datos con **Python (Pandas)** hasta la creación de un **dashboard analítico en Power BI**.  
El objetivo fue obtener una visión 360° del negocio en tres ejes:
- 💰 Ventas  
- 👥 Clientes  
- 🚚 Logística  

---

## 🧱 Estructura del Proyecto
```
📂 Proyecto_Final/
│
├── .git/                               # Carpeta del repositorio Git
├── Datos en bruto/                    # Datasets originales (df_Customers, df_Payments, df_Products, Ordenes)
├── datos_limpios_unificados/          # Dataset final limpio (fact_table.xlsx)
├── Informe y ReadMe/                  # Informe PDF y archivo README
├── Limpieza y presentación PowerBI/   # Archivo .pbix y visualizaciones finales
```

---

## 🧰 Tecnologías Utilizadas
- **Python (Pandas, NumPy)** – Limpieza y transformación de datos  
- **Power BI Desktop** – Modelado, medidas DAX y dashboards  
- **Excel** – Integración y revisión intermedia de datasets  
- **GitHub** – Repositorio y documentación  

---

## ⚙️ Fase 1 — Limpieza y Transformación (Python / Pandas)

### 🧩 Datasets utilizados
| Archivo | Descripción |
|----------|-------------|
| `df_Customers` | Datos de clientes (ID, ciudad, estado) |
| `df_Payments` | Detalles de pago (tipo, cuotas, importe) |
| `df_Products` | Categorías y atributos de productos |
| `Ordenes` | Información de pedidos, fechas y estado |

### 🧼 Principales transformaciones
- Eliminación de duplicados y registros vacíos.  
- Conversión de tipos (`datetime`, `float`, `string`).  
- Creación de nuevas columnas:
  - `purchase_date`, `purchase_month`, `purchase_year`  
  - `hours_to_approve`, `days_to_deliver`  
  - `line_total`, `on_time_flag`, `delivered_flag`
- Filtrado de valores atípicos (fechas inválidas, precios nulos).  

### 📦 Resultado
→ Exportación del dataset limpio **`fact_table.xlsx`**, con todas las métricas preparadas para el modelado en Power BI.

---

## 📈 Fase 2 — Modelado y Análisis (Power BI)

### 🧰 Power Query
- Promoción de encabezados y cambio de tipos de datos.  
- Eliminación de filas con `customer_id` o `product_category_name` nulos.  
- Creación de columnas derivadas (`price_amt`, `shipping_amt`, `line_total_amt`, `approve_hours`, `delivery_hours`).  
- Conversión de importes a euros (centavos → €).  

### 🧮 Medidas DAX
**Ventas:**
```DAX
Ingresos € = SUM(fact_table[line_total_amt])
Pedidos = DISTINCTCOUNT(fact_table[order_id])
Ticket Medio € = DIVIDE([Ingresos €], [Pedidos])
```

**Clientes:**
```DAX
Clientes Únicos = DISTINCTCOUNT(fact_table[customer_id])
Ingresos por Cliente € = DIVIDE([Ingresos €], [Clientes Únicos])
Clientes Acumulados = CALCULATE(DISTINCTCOUNT(fact_table[customer_id]),
FILTER(ALL(DimDate), DimDate[Date] <= MAX(DimDate[Date])))
```

**Logística:**
```DAX
% On-Time = DIVIDE([Pedidos On-Time], [Pedidos Entregados])
Horas Entrega Promedio = AVERAGE(fact_table[delivery_hours])
```

---

## 📊 Fase 3 — Dashboards

### 💚 Ventas
- **KPIs:** Ingresos €, Pedidos, Ticket Medio €, Unidades.  
- **Visuales:**  
  - Línea: Ingresos por mes  
  - Barras: Ingresos por estado  
  - Barras: Ingresos por categoría  
  - Tabla: Top 10 productos  

### 💙 Clientes
- **KPIs:** Clientes Únicos, Pedidos por Cliente, Ingresos por Cliente €.  
- **Visuales:**  
  - Línea: Clientes por mes  
  - Barras: Clientes por estado (Top 10)  
  - Donut: Clientes por método de pago  
  - Línea: Clientes acumulados  

### ❤️ Logística
- **KPIs:** % On-Time, % Entregados, Horas Promedio de Aprobación y Entrega.  
- **Visuales:**  
  - Línea: Pedidos por fecha de entrega  
  - Barras: % On-Time por estado  
  - Donut: Pedidos On-Time vs Tardíos  
  - Tabla: Promedio de retrasos  

### 🏁 Portada / Resumen Ejecutivo
Incluye las 3 métricas clave:
| Métrica | Gráfico | Insight |
|----------|----------|----------|
| Ingresos Totales (€) | Pie: por categoría | “Toys” domina las ventas |
| Clientes Únicos | Donut: por método de pago | Tarjeta de crédito +70% |
| % On-Time | Pie: entregas a tiempo | 93,6% puntualidad |

---

## 🔍 Conclusiones
- Los clientes compran **una sola vez**, sin recurrencia.  Esto se puede deber a que se genere un ID nuevo por cada cliente a pesar de que compre el mismo mas de una vez.
- **Toys** representa un *outlier positivo* (94,11% de los ingresos).  
- **93,6%** de las entregas fueron puntuales → logística eficiente.  
- **SP y RJ** concentran la mayor parte de las ventas.  
- Dominancia del método de pago **tarjeta de crédito (≈70%)**.

---

## 🧠 Insights Clave
1. Alta dependencia de una sola categoría de producto.  
2. Excelente eficiencia operativa.  
3. Oportunidad para programas de fidelización.  

---

## 🔄 Próximos pasos
- Implementar alertas automáticas en Power BI para retrasos.  
- Incluir variables de marketing y satisfacción del cliente.  
- Extender el modelo a series temporales para pronósticos.  

---

## ✒️ Autor
**Claudio Baldini**  
ThePower Business School — Octubre 2025  


