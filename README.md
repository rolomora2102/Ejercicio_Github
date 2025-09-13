# Ejercicio_Github

1) “Lista inteligente” que aprende hábitos

Modelo de predicción

Señales: frecuencia (cada cuánto compras), recencia (hace cuánto), estacionalidad (fines de semana, quincena, Navidad), contexto (clima, ubicación de casa vs. trabajo), co-ocurrencias (si compras pasta, sueles comprar salsa).

Algoritmo: combinación simple y explicable (puntuación = α·frecuencia + β·recencia + γ·co-ocurrencias + δ·estacionalidad). Empieza con reglas y luego puedes migrar a un modelo ligero (logística o gradient boosting).

Top-N sugerencias con confianza y motivo (“sueles comprar cada 2 semanas; última vez: hace 15 días”).

Aprendizaje continuo

Refuerza la puntuación cuando el usuario acepta una sugerencia; la reduce cuando la descarta.

Distingue marcas y presentaciones (leche deslactosada 1 L).

Cold start

Plantilla por país + categorías básicas + importación de compras previas (tickets OCR o integración supermercado).

Privacidad/controles

Botón “No sugerir más”, edición de preferencias y exclusiones permanentes.

UX

Sección “Sugeridos para hoy” + “Reponer pronto” + “En promoción”.

“Auto-agregar” opcional cuando el score supere umbral.

3) Lista compartida en tiempo real (multiusuario)

Sincronización

WebSockets/Realtime DB. CRDT o last-write-wins con operational transforms para evitar conflictos.

Operaciones atómicas: agregar/editar/cambiar cantidad/marcar comprado/asignar a persona.

Roles y control

Propietario, editores, solo lectura. Historial por ítem con undo.

Presencia y bloqueo suave

“Danii está editando ‘Arroz’…”, y locks temporales para ediciones largas.

Comentarios & tareas

Chat por artículo (“¿sirve marca X?”), @menciones, fotos.

Asignaciones

“Quién compra qué”, con estado (pendiente, en carrito, comprado).

Offline-first

Cache local, cola de operaciones, conflict resolution al reconectar.

Notificaciones

Push por cambios relevantes (nuevo ítem, agotado, lista completada).

Varios locales

Soporte de múltiples tiendas por lista (mismo ítem, distintos precios).

Integraciones

Compartir por link, importación desde WhatsApp/Notas (parseo).

5) Presupuesto y alertas de ofertas

Presupuesto

Presupuesto mensual y por compra; barra de progreso en la lista.

Estimador de ticket: precio histórico × cantidad (por tienda).

Dashboard: gasto por categoría, marca, tienda; comparativo vs meses previos.

Precios & ofertas

Fuentes: API de supermercados / scraping permitido / comunidad (sube foto del ticket).

Historial de precio por producto; etiqueta “precio bajo de los últimos 90 días”.

Alertas configurables:

Por producto (“avísame si el atún baja de ₡1 100”).

Por categoría (“leches 10% off o más”).

Por tienda y geocerca (si entras a la tienda, notifica ofertas relevantes).

Sustituciones inteligentes: si el favorito supera el presupuesto, sugiere alternativas equivalentes (misma categoría/nutrientes) con ahorro estimado.

OCR de recibos

Capturas de tickets para actualizar precios, validar gasto y mejorar predicciones.

Reglas personales

“No sugerir ofertas con azúcar añadida”, “solo marcas X/Y”.

7) Categorización y orden según ruta óptima en tienda

Modelo de tienda

Mapa por pasillo/sector (Abarrotes → A1: cereales, A2: pastas; Lácteos; Frutas/Verduras; Carnes; Limpieza…).

El usuario elige una tienda; se descarga su layout (o uno comunitario).

Enriquecimiento de productos

Cada ítem → categoría + pasillo + ubicación aprox. (shelf mapping simple).

Ordenamiento dinámico

Ordena la lista por secuencia de pasillos de la entrada a la caja.

Agrupa por pasillo con separadores y checklist rápido.

Reordenamiento en vivo si cambias de entrada o saltas un pasillo.

Algoritmo

Grafo simple de pasillos; resuelve una ruta tipo TSP heurística (Nearest Neighbor + 2-opt) con pesos bajos (porque el grafo es pequeño).

Regla práctica: “una sola pasada” minimizando retrocesos.

Modo multi-comprador

Divide por zonas: asigna pasillos a personas para comprar en paralelo; muestra progreso por zona.

Accesibilidad & preferencias

“Evitar productos fríos al inicio” (reordena Lácteos/Helados al final).

Prioriza perecederos al final; pesado (agua/arroz) al inicio si llevas carrito.

Fallback

Si no hay layout real, usa orden canónico de categorías y permite arrastrar-soltar para que el usuario lo ajuste y lo guardas como “Ruta personal”.
