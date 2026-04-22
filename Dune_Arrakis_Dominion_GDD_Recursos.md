**GAME** **DESIGN** **DOCUMENT**

**Dune:** **Arrakis** **Dominion** **Distributed**

**Sistema** **de** **Recursos** **y** **Producción**

**Versión:** 0.1 **Fecha:** Abril 2026 **Motor:** Godot 4.x

**Plataforma:** PC/Web

**ÍNDICE**

> 1\. <u>Visión General</u>
>
> 2\. <u>Sistema de Recursos</u> 3. <u>Cadena de Producción</u>
>
> 4\. <u>Mecánicas de Extracción</u> 5. <u>Sistema de Rondas</u>
>
> 6\. <u>Interfaz de Usuario</u>
>
> 7\. <u>Implementación en Godot</u>

**1.** **VISIÓN** **GENERAL**

**1.1** **Premisa** **del** **Juego**

El jugador controla una **Casa** **Menor** asignada a un sector de
Arrakis. Debe gestionar la extracción de recursos, construir enclaves,
manejar criaturas y recibir visitantes mientras cumple cuotas de
producción y evita conflictos diplomáticos.

**1.2** **Objetivos** **del** **Sistema** **de** **Recursos**

> Crear un **circuito** **económico** creíble dentro del universo Dune
> Ofrecer **decisiones** **significativas** sobre asignación de recursos
> Mantener **accesibilidad** (1-2 horas por partida)
>
> Justificar narrativamente cada mecánica

**1.3** **Tipos** **de** **Recursos**

||
||
||
||
||
||
||
||

**2.** **SISTEMA** **DE** **RECURSOS**

**2.1** **Recurso** **Primario:** **Especia** **(Melange)**

**Propiedades**

> **Unidad:** Kg de Especia
>
> **Producción:** Variable según sector y condiciones
>
> **Decaimiento:** La especia cosechada pierde 5% de valor por ronda si
> no se procesa/vende
>
> **Almacenamiento:** Requiere contenedores especiales (costosos)

**Modelo** **Matemático** **de** **Producción**

> Producción_Especia =

||
||
||
||

> × Eficiencia_Enclaves

**Variables:**

> Afloramientos_Sector: 1-5 por sector (fijos al inicio) Factor_Clima:
> 0.3 - 1.5 (basado en eventos de tormenta) Factor_Gusanos: 0.5 - 2.0
> (si hay gusanos activos, mayor producción) Eficiencia_Enclaves: 0.5 -
> 2.0 (basado en nivel de instalaciones) Costo_Operacional: 10-50
> Solaris por ronda

**Justificación** **Narrativa**

> *"La* *especia* *no* *se* *'mina'.* *Se* *observa,* *se* *espera,*
> *se* *arriesga.* *El* *desierto* *decide* *cuándo* *y* *dónde."* *—*
> *Fragmento* *de* *"Manual* *del* *Operador* *de* *Casa* *Menor"*

En Dune canon, la especia:

> Se forma en las profundidades del desierto
>
> Los gusanos de arena son esenciales para su ciclo vital Las "trampas
> de arena" indican afloramientos
>
> Las tormentas pueden destruir o revelar depósitos

**2.2** **Recurso** **Secundario:** **Solaris**

**Propiedades**

> **Unidad:** Unidades de Energía (UE)
>
> **Producción:** Constante si hay paneles solares activos
> **Almacenamiento:** Baterías con capacidad limitada **Decaimiento:**
> No se deteriora

**Modelo** **de** **Producción**

> Producción_Solaris =

||
||
||
||

> = Excedente

**Justificación** **Narrativa**

Arrakis recibe el doble de radiación solar que la Tierra debido a sus
dos soles. Los Fremen desarrollaron windtraps y captadores solares. Las
tormentas de arena reducen la eficiencia.

**2.3** **Recurso** **Crítico:** **Agua**

**Propiedades**

> **Unidad:** Litros (l)
>
> **Producción:** Limitada (windtraps, reciclaje) **Consumo:** Personal,
> instalaciones, criaturas **Almacenamiento:** Tanques limitados

**Modelo** **de** **Consumo**

> Consumo_Agua =

||
||
||
||

> \+ Instalaciones × 10-100 l/ronda = Total_Consumo

**Justificación** **Narrativa**

> *"El* *agua* *es* *vida* *en* *Arrakis.* *Cada* *gota* *cuenta."* *—*
> *Proverbio* *Fremen*

En el universo Dune, el agua es el recurso más valioso en el desierto.
Los Fremen reciclan todo el líquido corporal.

**2.4** **Recurso** **de** **Construcción:** **Materiales**

**Propiedades**

> **Unidad:** Toneladas (T)
>
> **Producción:** Extracción de rocas, reciclaje de escombros **Uso:**
> Construcción y mejoras

**Modelo**

> Materiales_Nuevos = Minas_Activas × 5 T/ronda
>
> \+ Reciclaje × 0.3 × Materiales_Demolidos

**3.** **CADENA** **DE** **PRODUCCIÓN**

**3.1** **Flujo** **General**

> \[RECOURSOS BRUTOS\] → \[PROCESAMIENTO\] → \[RECURSOS PROCESADOS\] →
> \[USO\]

||
||
||
||
||
||

> Trampas de arena Talleres

**3.2** **Estaciones** **de** **Producción**

**Fase** **1:** **Extracción**

||
||
||
||
||
||
||

**Fase** **2:** **Procesamiento**

||
||
||
||
||
||

**Fase** **3:** **Almacenamiento**

> **Silo** **de** **Especia**: Capacidad 100 kg **Baterías**
> **Solares**: Capacidad 500 UE **Tanque** **de** **Agua**: Capacidad
> 1,000 l **Almacén** **de** **Materiales**: Capacidad 200 T

**3.3** **Balanceo** **del** **Sistema**

Para mantener accesibilidad, el juego tendrá:

> 1\. **Límites** **claros** de producción por instalación
>
> 2\. **Sin** **microgestión** - las instalaciones funcionan
> automáticamente 3. **Decisiones** **estratégicas** sobre qué construir
> y cuándo
>
> 4\. **Eventos** **que** **interrumpen** el flujo (tormentas,
> migraciones de gusanos)

**4.** **MECÁNICAS** **DE** **EXTRACCIÓN**

**4.1** **Exploración** **del** **Sector**

Al inicio de cada partida, el jugador recibe un **sector**
**procedural** que contiene:

> **Afloramientos** **de** **Especia** (marcados como puntos de interés)
> **Quebradas** **y** **Zonas** **Protegidas** (para windtraps)
>
> **Zonas** **de** **Alta** **Radiación** (para paneles solares)
> **Yacimientos** **de** **Rocas** (para minas)

**Mecánica** **de** **Exploración**

> Acciones_de_Exploración = 3/ronda Tiempo_de_Exploración = 1 acción = 1
> zona revelada

Revelar una zona muestra:

> Tipo de recurso Cantidad estimada Peligros asociados

**4.2** **Colocación** **de** **Instalaciones**

El jugador selecciona ubicaciones en un **mapa** **isométrico** del
sector:

> 1\. **Zonas** **abiertas**: Solo paneles solares 2. **Quebradas**:
> Windtraps, enclaves
>
> 3\. **Afloramientos**: Trampas de especia 4. **Acantilados**: Torres
> de vigilancia

**Restricciones** **de** **Ubicación**

> Cada instalación requiere **espacio** **específico** Zonas peligrosas
> requieren **personal** **de** **riesgo**
>
> Algunas zonas solo se desbloquean con **tecnología**

**4.3** **Ciclo** **de** **Producción** **Automatizado**

Una vez colocadas, las instalaciones funcionan automáticamente:

> \[Ronda N\]

||
||
||
||
||
||
||

> └─\> Resultado aplicado al inventario

**5.** **SISTEMA** **DE** **RONDAS**

**5.1** **Estructura** **de** **una** **Ronda**

> ┌─────────────────────────────────────────────────────────┐

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> └─────────────────────────────────────────────────────────┘

**5.2** **Duración** **de** **Ronda**

> **1** **Ronda** **=** **1** **ciclo** **de** **producción**
>
> **Partida** **completa** **=** **12-20** **rondas** (1-2 horas)
>
> **Condiciones** **de** **fin**: Cuota cumplida, bankruptcy, o decisión
> del jugador

**5.3** **Eventos** **Aleatorios**

||
||
||
||
||
||
||
||
||

**6.** **INTERFAZ** **DE** **USUARIO**

**6.1** **Pantalla** **Principal** **(HUD)**

> ┌──────────────────────────────────────────────────────────────────┐

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> └──────────────────────────────────────────────────────────────────┘

**6.2** **Pantalla** **de** **Construcción**

> ┌──────────────────────────────────────────────────────────────────┐

||
||
||
||
||
||
||
||
||
||

||
||
||
||
||

> └──────────────────────────────────────────────────────────────────┘

**6.3** **Flujo** **de** **Ronda** **Visual**

> ┌─────────────┐

||
||
||
||
||
||
||
||
||

> └─────────────┘

**7.** **IMPLEMENTACIÓN** **EN** **GODOT**

**7.1** **Estructura** **del** **Proyecto**

> res://

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> └── fonts/

**7.2** **Clase** **ResourceManager** **(Core)**

> class_name ResourceManager extends Node

||
||
||
||

> enum ResourceType {ESPECIA, SOLARIS, AGUA, MATERIALES, CONOCIMIENTO}

||
||
||
||
||
||
||
||

||
||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||

||
||
||
||

> func get_fill_percentage(type: ResourceType) -\> float: return
> resources\[type\] / capacities\[type\]

**7.3** **Clase** **Installation** **(Base)**

class_name Installation extends Node2D

||
||
||
||

||
||
||
||
||

||
||
||
||
||

||
||
||
||

||
||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||

||
||
||
||

> func destroy() -\> void: queue_free()

**7.4** **Sistema** **de** **Producción**

> class_name ProductionSystem extends Node

||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||
||
||

||
||
||
||
||
||
||
||

> return total_maintenance

**7.5** **EventSystem**

> class_name EventSystem extends Node
>
> signal event_triggered(event_data: Dictionary)

||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

> \]

||
||
||
||
||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||

> pass

**7.6** **RoundManager**

class_name RoundManager extends Node

||
||
||
||
||

||
||
||
||

||
||
||
||
||

var is_processing: bool = false

||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||

||
||
||
||
||
||

||
||
||
||
||
||
||
||
||
||
||
||
||

> return score

**ANEXO** **A:** **Tablas** **de** **Balanceo**

**Producción** **Base** **por** **Instalación**

||
||
||
||
||
||
||
||
||

**Costos** **de** **Construcción**

||
||
||
||
||
||
||

**Probabilidades** **de** **Eventos**

||
||
||
||
||
||
||
||

**PRÓXIMOS** **PASOS**

> 1\. **Revisar** **y** **validar** este documento de diseño
>
> 2\. **Implementar** **prototipo** en Godot 4.x con las clases básicas
> 3. **Playtesting** del loop de producción
>
> 4\. **Iterar** basado en feedback

*Documento* *generado* *para:* *Dune:* *Arrakis* *Dominion*
*Distributed* *Basado* *en* *el* *universo* *creado* *por* *Frank*
*Herbert*
