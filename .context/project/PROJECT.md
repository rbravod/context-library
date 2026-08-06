# Context Library

## Objetivo

Context Library (CL) es una biblioteca reutilizable de contexto para proyectos asistidos por inteligencia artificial.

Su objetivo es proporcionar una estructura sencilla, portable y auditable que permita incorporar a cualquier proyecto el conocimiento necesario para que personas y herramientas de IA puedan trabajar de forma consistente.

CL debe ser independiente de la herramienta utilizada y compatible tanto con entornos conversacionales, como ChatGPT Projects, como con entornos agénticos capaces de trabajar directamente sobre un repositorio, como Codex, ChatGPT Work u otras herramientas presentes o futuras.

La fuente canónica del contexto es siempre el conjunto de **ficheros de contexto** versionados mediante Git, expresados en Markdown y, cuando corresponda, sus metadatos asociados.

Las configuraciones, memorias o instrucciones particulares de una herramienta de IA son consumidores o adaptaciones de ese contexto, nunca su fuente de verdad.

---

# Naturaleza del proyecto

Context Library cumple simultáneamente dos funciones:

1. Es el repositorio maestro donde evolucionan `core/` y `playbooks/`.
2. Es una plantilla mínima a partir de la cual pueden iniciarse nuevos proyectos.

Los proyectos copian los elementos de CL que necesitan. Una vez incorporados a un proyecto, estos pasan a formar parte de él y pueden evolucionar independientemente.

CL no pretende convertirse en un framework, una plataforma de gestión de conocimiento ni un sistema de sincronización entre proyectos.

La simplicidad operativa es un requisito fundamental.

---

# Estructura de contexto

La estructura base es:

```text
.context/
├── core/
├── playbooks/
├── project/
└── user/
```

Cada ámbito tiene una responsabilidad diferente.

## core

Contiene las reglas y principios universales de funcionamiento y gobierno del contexto.

Responde a la pregunta:

> ¿Cómo trabajamos?

Todo el contenido de `core/` es de obligado cumplimiento y debe cargarse siempre.

Los documentos se leen en el orden establecido por sus nombres de fichero. El orden de lectura no establece diferencias de autoridad entre ellos.

Inicialmente contiene:

- `01_governance.md`: gobierno y jerarquía de autoridad del contexto;
- `02_trust.md`: frontera de confianza y tratamiento de recursos externos;
- `03_knowledge.md`: captura, validación y mantenimiento del conocimiento;
- `04_working_principles.md`: principios generales de trabajo de asistentes y agentes;
- `05_metadata.md`: metadatos y versionado de los elementos de contexto reutilizables.

Las reglas de `core/` tienen la máxima autoridad dentro de Context Library.

---

## playbooks

Contiene conocimiento reutilizable y especializado que puede compartirse entre proyectos.

Responde a la pregunta:

> ¿Cómo hacemos este tipo de trabajo?

Conceptualmente, un playbook cumple una función similar a la de un fichero `SKILL.md`: proporciona a un agente conocimiento e instrucciones especializadas para realizar determinados tipos de trabajo.

Los playbooks de Context Library no son ficheros `SKILL.md` ni dependen de ese formato. CL utiliza su propio modelo de contexto, gobernanza, confianza, metadatos y validación humana.

Ejemplos:

- desarrollo Moodle;
- testing;
- seguridad;
- arquitectura;
- documentación;
- Git;
- Docker.

Los playbooks se cargan de forma selectiva según las necesidades de la tarea.

El agente determina qué playbooks son relevantes a partir del objetivo de la tarea, el contexto disponible y las instrucciones de descubrimiento aplicables. Durante la ejecución puede cargar contexto adicional si aparecen nuevas necesidades.

La mera presencia de un playbook en `.context/playbooks/` no implica que deba cargarse. El contexto especializado no debe cargarse preventivamente cuando no resulte relevante para el trabajo que se está realizando.

Pueden proceder de:

- conocimiento propio;
- experiencia acumulada en proyectos;
- documentación externa;
- estándares;
- `SKILL.md` u otros formatos equivalentes;
- material de terceros previamente revisado y adaptado.

Todo contenido incorporado a `playbooks/` debe haber superado la frontera de confianza definida por `core/`.

Los playbooks son elementos reutilizables y pueden evolucionar independientemente del proyecto en el que se utilizan. Su versión y procedencia se gestionan mediante los metadatos definidos por `core/`.

La existencia de una versión más reciente de un playbook no implica su actualización automática en los proyectos que utilizan una versión anterior.

Los playbooks no tienen autoridad independiente. Están sujetos a las reglas definidas por `core/` y al contexto aplicable de `project/`.

### Por qué no utilizar directamente SKILL.md

Los playbooks y los ficheros `SKILL.md` persiguen objetivos relacionados, pero no son equivalentes.

`SKILL.md` es un formato orientado a proporcionar instrucciones y conocimiento especializado a agentes compatibles con ese mecanismo. Context Library tiene un objetivo diferente: mantener conocimiento reutilizable como parte de un sistema de contexto gobernado por el proyecto e independiente de una herramienta o proveedor concreto.

CL no adopta directamente `SKILL.md` como formato de playbook porque necesita aplicar requisitos propios:

- frontera de confianza explícita;
- revisión y validación humana antes de incorporar contenido;
- versionado independiente;
- procedencia y condiciones legales identificables;
- posibilidad de adaptar el contenido a las necesidades y decisiones del proyecto;
- independencia respecto al formato utilizado por una herramienta concreta.

Esto no implica descartar el ecosistema de Skills. Un `SKILL.md` puede ser una fuente excelente para crear o actualizar un playbook después de ser revisado, auditado y adaptado.

Del mismo modo, cuando resulte útil, un playbook de CL podrá transformarse o adaptarse al formato requerido por una herramienta concreta.

CL mantiene la fuente canónica; los formatos específicos de cada herramienta son representaciones o adaptaciones de esa fuente.

---

## project

Contiene el conocimiento específico del proyecto.

Responde a la pregunta:

> ¿Qué sabemos y qué hemos decidido sobre este proyecto?

Puede incluir:

- objetivos;
- arquitectura;
- decisiones;
- ADR;
- casos de uso;
- historias de usuario;
- requisitos;
- restricciones;
- integraciones;
- deuda técnica;
- roadmap;
- contexto funcional;
- contexto de dominio;
- documentación de componentes.

`.context/project/` no es necesariamente un resumen del proyecto. Puede contener conocimiento suficientemente detallado como para permitir reconstruir o comprender partes relevantes del sistema.

El contexto de `project/` se carga de forma selectiva según las necesidades de la tarea. El agente determina qué información resulta relevante a partir del objetivo de la tarea, el contexto disponible y las instrucciones de descubrimiento aplicables.

La mera presencia de información en `project/` no implica que deba cargarse para todas las tareas.

El contenido de `project/` constituye la fuente canónica del contexto específico del proyecto.

Cuando un proyecto está compuesto por varios componentes o repositorios, cada componente puede disponer de su propio contexto específico. Ese contexto especializa el del proyecto que lo contiene sin contradecir contexto de mayor autoridad.

El nivel de detalle y la organización interna de `project/` dependen de las necesidades reales del proyecto. Context Library no impone una estructura documental interna universal.

---

## user

Contiene contexto particular de la persona que trabaja con el agente cuando ese contexto puede afectar de forma útil a la colaboración.

Responde a la pregunta:

> ¿Qué necesita saber el agente sobre esta persona para trabajar mejor con ella en este proyecto?

Puede incluir:

- preferencias de comunicación;
- preferencias de escritura;
- forma de trabajo;
- criterios habituales de decisión;
- convenciones personales;
- experiencia o conocimientos relevantes;
- restricciones;
- información personal cuando tenga una consecuencia operativa clara.

`user/` no es un perfil general de la persona ni un repositorio de información personal. Sólo debe contener información cuya presencia pueda modificar de forma útil cómo el agente colabora, propone, explica, prioriza o ejecuta el trabajo.

El contexto de `user/` se carga de forma selectiva según las necesidades de la tarea. Su mera presencia no implica que deba cargarse siempre.

Por ejemplo, `user/` puede indicar:

- el nivel de detalle técnico adecuado para una persona y qué conocimientos pueden darse por asumidos;
- cómo prefiere recibir propuestas, explicaciones o alternativas antes de tomar una decisión;
- convenciones de escritura que deben respetarse al redactar en su nombre;
- formas de trabajo que ayudan a mantener el foco o evitar trabajo innecesario;
- restricciones de disponibilidad, herramientas o entorno que condicionan determinadas tareas;
- criterios personales recurrentes que resultan relevantes al evaluar distintas opciones.

Este contexto sólo debe cargarse cuando pueda afectar al trabajo que se está realizando. Una preferencia de escritura puede ser relevante al redactar documentación o un artículo, pero no al analizar código; una preferencia sobre cómo presentar alternativas puede ser relevante al tomar una decisión de arquitectura, pero no al ejecutar una modificación ya decidida.

La inclusión de información personal debe ser deliberada. Cuando un dato sea sensible, debe existir una razón clara para conservarlo y para incorporarlo al contexto de un proyecto concreto.

Context Library no contempla por defecto múltiples perfiles de usuario dentro de un mismo proyecto. Cada proyecto incorpora únicamente el contexto `user/` que resulte necesario.

Si una regla deja de ser específica de una persona y pasa a ser una decisión del proyecto, debe promoverse a `project/`.

Si deja de ser específica del proyecto y se convierte en una regla universal de trabajo, debe promoverse a `core/`.

`user/` nunca puede contradecir reglas de mayor autoridad definidas por `project/` o `core/`.

---

## Composición del contexto

La estructura `.context/` representa una organización lógica del contexto y no obliga a que todos sus ámbitos estén presentes en cada repositorio.

Un proyecto puede estar formado por múltiples repositorios o componentes. En estos casos, el contexto puede distribuirse entre distintos niveles evitando duplicar información compartida.

Por ejemplo:

```text
project-context/
└── .context/
    ├── core/
    ├── playbooks/
    ├── project/
    └── user/

component-a/
└── .context/
    └── project/

component-b/
└── .context/
    └── project/
```

El contexto global contiene las reglas, conocimiento y decisiones compartidas por el proyecto.

Cada componente mantiene únicamente el contexto que le es específico.

No es necesario crear ámbitos vacíos de `core/`, `playbooks/` o `user/` para reproducir formalmente la estructura completa.

Cuando se trabaja sobre un componente como parte del proyecto, su contexto efectivo se construye mediante la composición del contexto global y su contexto específico.

Esta composición no implica cargar íntegramente todo el contexto disponible. Se mantienen las reglas de carga definidas por CL: `core/` es obligatorio y el contexto restante se carga progresivamente según las necesidades de la tarea.

El contexto específico de un componente puede especializar el contexto del proyecto que lo contiene, pero no contradecir contexto de mayor autoridad.

Un componente que deba poder utilizarse como proyecto autónomo puede incorporar su propio `core/`, `playbooks/` y demás contexto necesario.

---

# Contexto y artefactos

`.context/` contiene el contexto interno necesario para comprender, decidir y trabajar correctamente en el proyecto.

No es el contenedor de los artefactos que el proyecto produce.

El código fuente y los demás resultados producidos por el proyecto, como artículos, publicaciones, entregables o documentación destinada a terceros, viven fuera de `.context/`.

La documentación no es necesariamente un artefacto. Cuando un documento contiene conocimiento que forma parte de la fuente de verdad necesaria para comprender, desarrollar, mantener o evolucionar el proyecto, puede formar parte de `.context/project/`, independientemente de su extensión o nivel de detalle. Por ejemplo:

- arquitectura;
- Domain-Driven Design;
- ADR;
- casos de uso;
- historias de usuario;
- conocimiento funcional;
- análisis de sistemas existentes;
- restricciones;
- decisiones;
- planificación.

La distinción entre contexto y artefacto no depende de su formato, extensión o nivel de detalle, sino de la función que cumple dentro del proyecto.

Un caso de uso utilizado como fuente de verdad para construir y validar una funcionalidad es contexto del proyecto. Un documento preparado para comunicar o entregar ese conocimiento a un cliente es un artefacto.

Los artefactos pueden generarse o seleccionarse a partir del contexto cuando resulte conveniente.

Por ejemplo, la documentación destinada a terceros puede producirse a partir del conocimiento mantenido en `.context/project/` sin convertir por ello el artefacto generado en contexto canónico.

Cuando exista una necesidad real, este proceso puede automatizarse mediante scripts, integración continua o entrega continua.

Context Library no gestiona la visibilidad pública o privada de los artefactos.

El contenido de `.context/` se considera contexto interno salvo decisión explícita del proyecto de distribuirlo.

---

# Ubicación y alcance del contexto

La estructura `.context/` define una organización lógica del contexto, no una obligación sobre su ubicación física.

En un proyecto sencillo, `.context/` puede residir en el mismo repositorio que el código o los demás artefactos del proyecto.

En proyectos más complejos, el contexto puede mantenerse total o parcialmente en repositorios separados cuando existan razones de:

- visibilidad;
- propiedad;
- seguridad;
- confidencialidad;
- organización;
- ciclo de vida independiente.

La ubicación física del contexto no modifica su autoridad ni su función.

Un repositorio de código puede, por ejemplo, contener únicamente el contexto específico de un componente mientras recibe el contexto compartido del proyecto desde otro repositorio.

Del mismo modo, determinados ámbitos pueden mantenerse separados cuando no deban distribuirse junto con el resto del proyecto. Este es especialmente el caso de `user/`, que puede contener contexto personal o específico de colaboración.

La composición del contexto aplicable a una tarea debe estar definida de forma que el agente pueda descubrir qué fuentes de contexto corresponden al ámbito sobre el que está trabajando.

Separar físicamente el contexto no debe provocar duplicación innecesaria ni crear fuentes de verdad alternativas.

---
# Descubrimiento mediante AGENTS.md

`AGENTS.md` actúa como punto de entrada para que asistentes y agentes descubran el contexto aplicable al ámbito en el que están trabajando.

Su función principal es indicar dónde se encuentra el contexto y cómo debe cargarse. No debe convertirse en un contenedor alternativo de conocimiento, reglas o documentación que pertenezcan a `.context/`.

Todo proyecto que utilice Context Library debe disponer de un `AGENTS.md` raíz que permita al agente localizar el contexto inicial.

El `AGENTS.md` raíz debe indicar, como mínimo:

- dónde se encuentra el contexto aplicable;
- que todo el contexto de `core/` debe cargarse siempre;
- cómo descubrir el contexto opcional relevante para la tarea;
- cómo localizar contexto adicional cuando éste se encuentre distribuido entre distintos componentes o ubicaciones.

Pueden existir `AGENTS.md` adicionales en ámbitos más específicos cuando aporten información de descubrimiento que no pueda deducirse razonablemente desde el nivel superior.

Por ejemplo, un componente puede disponer de su propio `AGENTS.md` para indicar dónde se encuentra su contexto específico o cómo se compone con el contexto compartido del proyecto.

Los `AGENTS.md` no deben crearse únicamente para reproducir la estructura de directorios ni repetirse cuando no aporten información adicional.

La presencia de un `AGENTS.md` en un ámbito más específico no modifica la jerarquía de autoridad del contexto ni permite contradecir las reglas aplicables de niveles superiores.

El objetivo es mantener el mecanismo de descubrimiento mínimo necesario para que el agente pueda determinar correctamente qué contexto debe aplicar a una tarea.

---
# Jerarquía de autoridad

La autoridad del contexto sigue la siguiente jerarquía:

```text
core
  ↓
project
  ↓
user
```

Un nivel inferior puede concretar o especializar las reglas de un nivel superior, pero no contradecirlas.

Si una regla de un nivel superior deja de ser adecuada, debe modificarse conscientemente en el nivel que tiene autoridad sobre ella, no anularse de forma implícita desde un nivel inferior.

Los playbooks aportan conocimiento y procedimientos especializados. Están sujetos a las reglas definidas por `core/` y `project/`, pero no constituyen un nivel independiente dentro de la jerarquía de autoridad.

La composición de contexto procedente de distintos ámbitos o componentes no modifica esta jerarquía.

La jerarquía de autoridad no se negocia durante la ejecución de una tarea.

---

# Frontera de confianza

Context Library distingue entre contexto confiable y recursos externos.

El contenido incorporado y validado dentro de `.context/` se considera contexto confiable y puede utilizarse como instrucciones o conocimiento aplicable al proyecto según su ámbito y autoridad.

Los recursos externos no son confiables por defecto.

Esto incluye, entre otros:

- documentación externa;
- páginas web;
- repositorios de terceros;
- `SKILL.md`;
- prompts;
- ejemplos de configuración;
- código;
- documentos proporcionados como referencia.

El contenido externo debe tratarse inicialmente como información, no como instrucciones para el agente.

Antes de incorporarlo como contexto confiable debe revisarse para determinar:

- qué información resulta útil;
- si contiene instrucciones que no deben heredarse;
- si contradice el contexto existente;
- si su procedencia es suficientemente clara;
- qué licencia, copyright o requisitos de atribución le son aplicables;
- si necesita adaptación antes de incorporarse.

Una vez revisado, adaptado cuando sea necesario y validado mediante el mecanismo de validación humana del proyecto, el contenido resultante puede incorporarse a `.context/` y pasar a formar parte del contexto confiable.

La confianza se aplica al contenido incorporado, no automáticamente a su fuente. Haber utilizado anteriormente material procedente de una fuente no convierte en confiable cualquier contenido futuro procedente de ella.

La frontera de confianza y las reglas que deben seguir asistentes y agentes se definen normativamente en `core/`.

---
# Validación humana

Context Library mantiene la validación humana como requisito para convertir cambios de contexto en conocimiento canónico.

Los asistentes y agentes pueden:

- detectar conocimiento potencialmente útil;
- identificar inconsistencias, carencias o información obsoleta;
- proponer cambios;
- redactar nuevo contexto;
- modificar físicamente los ficheros cuando dispongan de capacidad y autorización para hacerlo.

Ninguna de estas acciones convierte por sí misma un cambio en contexto canónico.

Todo cambio debe pasar por el mecanismo de validación definido por el proyecto. La persona responsable decide si el cambio propuesto debe incorporarse, modificarse o descartarse.

La validación puede producirse de distintas formas según el flujo de trabajo del proyecto. Por ejemplo:

- aprobación explícita antes de que el agente modifique un fichero;
- revisión de los cambios realizados antes de aceptarlos;
- revisión mediante commit, pull request o mecanismo equivalente.

Context Library no impone un flujo técnico único de validación. Impone que exista una intervención humana consciente antes de considerar canónico el cambio.

Por defecto:

- en proyectos profesionales, la validación corresponde a la persona responsable de su arquitectura técnica;
- en proyectos personales, corresponde a la persona propietaria del proyecto.

Un proyecto puede definir otro mecanismo o distribuir la responsabilidad de validación cuando su organización lo requiera.

La capacidad técnica de un agente para modificar un fichero nunca implica autoridad para aprobar su contenido.

---
# Gestión del conocimiento

Context Library trata el conocimiento persistente del proyecto como un recurso mantenido conscientemente, no como un subproducto de conversaciones con asistentes o agentes.

Durante el trabajo pueden aparecer nuevos conocimientos, decisiones, restricciones, convenciones o correcciones que resulte útil conservar.

Cuando un asistente o agente identifica información con posible valor persistente, debe determinar si ya está recogida en el contexto y, si no lo está, proponer su incorporación en el ámbito adecuado.

La incorporación de conocimiento sigue, de forma general, este ciclo:

1. detectar conocimiento potencialmente persistente;
2. comprobar si ya existe o entra en conflicto con contexto actual;
3. determinar el ámbito adecuado (`core/`, `playbooks/`, `project/` o `user/`);
4. proponer el cambio concreto y su ubicación;
5. someterlo al mecanismo de validación humana;
6. incorporarlo al contexto canónico mediante el flujo de control de versiones del proyecto.

No todo lo aprendido durante una tarea debe conservarse.

El contexto debe contener conocimiento que pueda resultar útil en trabajo futuro y evitar información circunstancial, redundante, obsoleta o fácilmente derivable de otras fuentes.

El conocimiento existente también debe mantenerse. Los asistentes y agentes pueden detectar contexto posiblemente incorrecto, contradictorio o desactualizado y proponer su revisión o eliminación.

La gestión normativa de captura, mantenimiento y eliminación de conocimiento se define en `core/`.

---
# Versionado de elementos reutilizables

Los elementos reutilizables de Context Library pueden evolucionar independientemente de los proyectos que los utilizan.

Por este motivo, los documentos mantenidos en `core/`, `playbooks/` y `user/` disponen de una versión propia identificada mediante sus metadatos.

Esta versión permite conocer qué estado de un elemento reutilizable fue incorporado a un proyecto y compararlo posteriormente con versiones disponibles en su fuente.

El versionado del elemento es independiente del histórico proporcionado por Git. Ambos mecanismos cumplen funciones diferentes:

- Git registra la evolución del fichero dentro de un repositorio;
- la versión identifica la evolución de una pieza de contexto reutilizable entre distintos repositorios o proyectos.

Cuando un proyecto copia un elemento reutilizable, esa copia pasa a formar parte de su contexto y puede evolucionar independientemente.

La existencia de una versión más reciente en Context Library o en otra fuente no implica que la copia deba actualizarse automáticamente.

Una actualización debe considerar:

- las diferencias entre ambas versiones;
- las modificaciones realizadas localmente;
- la relevancia de los cambios para el proyecto;
- posibles conflictos con el contexto existente.

La incorporación de una nueva versión está sujeta al mecanismo normal de validación humana del proyecto.

Los documentos de `project/` no requieren versión propia por defecto, ya que pertenecen específicamente al proyecto y su evolución queda registrada mediante su sistema de control de versiones.

El esquema de metadatos utilizado para identificar versiones, procedencia y condiciones legales se define en `core/`.

---

# Procedencia

Context Library debe permitir conocer la procedencia del contenido reutilizable cuando éste se haya obtenido o elaborado a partir de material externo.

Conservar la procedencia permite:

- localizar y revisar la fuente original;
- comprender de dónde procede determinado conocimiento;
- volver a evaluar el contenido cuando la fuente evoluciona;
- comprobar las condiciones de licencia, copyright y atribución aplicables;
- mantener una trazabilidad razonable sobre el conocimiento incorporado.

La procedencia se refiere al origen externo del contenido, no al repositorio en el que actualmente se mantiene.

El contenido original creado directamente como parte de Context Library no necesita declarar una fuente. Su repositorio y su histórico de control de versiones proporcionan la trazabilidad necesaria.

Cuando un elemento reutilizable procede de material externo o se basa en él, su metadato `source` debe permitir identificar y localizar la fuente original.

La existencia de una fuente no convierte su contenido en confiable. Todo material externo debe atravesar la frontera de confianza antes de incorporarse al contexto canónico.

Conservar la procedencia tampoco implica mantener una relación de sincronización con la fuente. Una vez incorporado y validado, el contenido pasa a evolucionar según las reglas de Context Library y del proyecto que lo utiliza.

Las reglas normativas sobre procedencia y sus metadatos se definen en `core/`.

---

# Licencias de contenido externo

La incorporación de contenido externo a Context Library debe respetar las condiciones bajo las que dicho contenido puede utilizarse, modificarse y redistribuirse.

Antes de incorporar material externo debe comprobarse, cuando resulte aplicable:

- su licencia;
- los requisitos de atribución;
- las condiciones para realizar modificaciones o trabajos derivados;
- las obligaciones de redistribución;
- los avisos de copyright que deban conservarse;
- cualquier otra restricción relevante para su incorporación al proyecto.

La disponibilidad pública de un recurso no implica que pueda copiarse, modificarse o redistribuirse libremente.

Cuando el contenido externo se incorpore a un elemento reutilizable, sus metadatos deben reflejar la licencia y el copyright aplicables al contenido resultante, además de conservar su procedencia mediante `source`.

Si las condiciones aplicables no permiten determinar con suficiente claridad que el contenido puede incorporarse y utilizarse de la forma prevista, no debe integrarse como contexto canónico hasta resolver esa incertidumbre.

Cuando resulte necesario conservar textos de licencia, avisos de atribución u otra información legal adicional, éstos deben mantenerse junto al contenido de la forma requerida por sus condiciones originales.

La incorporación de material externo no modifica por sí misma la licencia del contenido original ni permite atribuir a Context Library derechos que no posee.

Las reglas de confianza, procedencia y metadatos aplicables al contenido externo se definen en `core/`.

---

# Licencia de Context Library

Context Library es un proyecto libre y su contenido original se publica bajo la licencia Creative Commons Attribution-ShareAlike 4.0 International (`CC-BY-SA-4.0`).

Esta licencia permite utilizar, copiar, adaptar y redistribuir el contenido, incluso con fines comerciales, siempre que se cumplan sus condiciones de atribución y se mantenga la misma licencia en los trabajos derivados cuando resulte aplicable.

La elección de `CC-BY-SA-4.0` pretende favorecer que el conocimiento desarrollado en Context Library pueda reutilizarse y adaptarse en otros proyectos sin perder su carácter abierto ni la atribución de su procedencia.

Los elementos reutilizables originales de Context Library identifican esta licencia mediante sus metadatos:

`license: CC-BY-SA-4.0`

La licencia de Context Library se aplica únicamente al contenido sobre el que el proyecto dispone de los derechos necesarios para ofrecerlo bajo estas condiciones.

El contenido procedente de terceros conserva las condiciones legales que le sean aplicables. Su incorporación a Context Library no modifica automáticamente su licencia ni permite relicenciarlo bajo `CC-BY-SA-4.0`.

Cuando un elemento combine contenido original de Context Library con material externo, deberá utilizar una licencia compatible con todos los contenidos incorporados y conservar los avisos, atribuciones y condiciones que correspondan.

El repositorio debe incluir el texto de la licencia aplicable al contenido original de Context Library.

---

# Repositorios

Context Library se mantiene en un repositorio Git propio que actúa como fuente maestra de `core/` y `playbooks/`.

Los proyectos que utilizan CL incorporan los elementos reutilizables que necesitan. Estas copias pasan a formar parte del contexto del proyecto y pueden evolucionar independientemente de su fuente.

No existe una relación de sincronización obligatoria entre Context Library y los proyectos que utilizan sus elementos.

El contexto específico de `user/` puede mantenerse en un repositorio privado independiente cuando deba reutilizarse entre proyectos sin formar parte de repositorios compartidos o públicos.

Cada proyecto decide cómo distribuir físicamente su contexto entre repositorios según sus necesidades de organización, propiedad, visibilidad y seguridad.

En proyectos sencillos, código, artefactos y `.context/` pueden convivir en un mismo repositorio.

En proyectos más complejos, pueden existir repositorios independientes para:

- contexto compartido del proyecto;
- componentes o módulos;
- contexto privado;
- código o infraestructura;
- otros elementos con ciclos de vida o requisitos de acceso diferentes.

Context Library no prescribe una estrategia concreta de composición Git, como submodules, subtrees o repositorios monolíticos.

La estructura de repositorios debe favorecer una fuente de verdad clara, evitar duplicaciones innecesarias y permitir que agentes y personas puedan descubrir el contexto aplicable al trabajo que realizan.

---

# Creación de proyectos

Context Library puede utilizarse como plantilla para iniciar el contexto de un nuevo proyecto.

La creación de un proyecto no consiste necesariamente en copiar toda la estructura y contenido disponible en CL. Deben incorporarse únicamente los elementos que resulten aplicables al proyecto.

Como punto de partida, un proyecto puede:

1. incorporar el `core/` vigente de Context Library;
2. seleccionar los playbooks que resulten inicialmente necesarios;
3. crear su contexto específico en `project/`;
4. incorporar contexto de `user/` cuando resulte útil y apropiado;
5. crear los mecanismos de descubrimiento necesarios mediante `AGENTS.md`.

No es necesario crear directorios o documentos vacíos únicamente para reproducir la estructura completa de Context Library.

Una vez incorporados, los elementos reutilizables pasan a formar parte del contexto del nuevo proyecto. El proyecto conserva la versión incorporada y puede modificarla o evolucionarla independientemente.

Context Library no mantiene una relación de dependencia o sincronización automática con los proyectos creados a partir de ella.

Las versiones posteriores de `core/`, `playbooks/` o `user/` pueden revisarse e incorporarse cuando aporten valor al proyecto, siempre mediante su mecanismo normal de validación humana.

El contexto inicial debe ser suficiente para trabajar correctamente, pero no intentar anticipar todas las necesidades futuras.

El contexto adicional se incorpora cuando aparece una necesidad real.

---

# Reutilización

Context Library está diseñada para que el conocimiento útil pueda reutilizarse entre proyectos sin crear dependencias innecesarias entre ellos.

La reutilización se basa en copiar los elementos de contexto que resulten aplicables e incorporarlos al proyecto que los necesita.

Una vez incorporado, un elemento reutilizable:

- pasa a formar parte del contexto del proyecto;
- conserva sus metadatos de versión, licencia, copyright y procedencia cuando corresponda;
- puede adaptarse a las necesidades del proyecto;
- puede evolucionar independientemente de su fuente;
- no mantiene una relación de sincronización automática con ella.

La reutilización no implica que todos los proyectos deban utilizar las mismas versiones ni conservar indefinidamente el contenido original sin modificaciones.

Cuando una evolución realizada dentro de un proyecto tenga valor generalizable, puede proponerse su incorporación a Context Library como nueva versión del elemento reutilizable correspondiente.

Del mismo modo, cuando Context Library publique una versión posterior de un elemento, los proyectos que utilicen versiones anteriores pueden evaluar sus cambios e incorporar aquellos que les resulten útiles.

En ambos sentidos, la reutilización requiere una decisión consciente y está sujeta al mecanismo normal de validación humana.

Context Library favorece así el intercambio de conocimiento entre proyectos sin convertirlos en consumidores dependientes de una fuente central.

---
# Compatibilidad con herramientas de IA

Context Library está diseñada para ser independiente de un proveedor, modelo o herramienta de inteligencia artificial concreta.

El contexto canónico se mantiene en Markdown y utiliza convenciones simples y portables. No depende de memorias propietarias, formatos internos de una plataforma ni funcionalidades exclusivas de un agente determinado.

Esto permite utilizar el mismo conocimiento con distintas herramientas, siempre que éstas puedan acceder al contexto y recibir las instrucciones necesarias para descubrirlo e interpretarlo.

La compatibilidad no implica que todas las herramientas utilicen Context Library de la misma forma ni que dispongan de las mismas capacidades.

Una herramienta puede, por ejemplo:

- descubrir y cargar contexto directamente desde el sistema de ficheros;
- trabajar sobre un repositorio completo de forma agéntica;
- recibir una selección de documentos como contexto;
- requerir que determinadas instrucciones se adapten a un formato específico;
- disponer de mecanismos propios de memoria, proyectos, skills o configuración.

Cuando una herramienta requiera un formato específico, éste debe considerarse una adaptación o representación del contexto canónico, no una fuente de verdad alternativa.

Las capacidades propias de cada herramienta pueden aprovecharse cuando aporten valor, pero no deben introducir dependencias innecesarias en la estructura canónica de Context Library.

Context Library no pretende ofrecer una abstracción que elimine las diferencias entre herramientas. Su objetivo es mantener el conocimiento y las reglas de trabajo en una forma suficientemente portable para que puedan reutilizarse y adaptarse entre ellas.

La incorporación de soporte específico para una herramienta debe responder a una necesidad real y no formar parte del núcleo de CL salvo que resulte generalmente aplicable.

---

# Trabajo conversacional y agéntico

Context Library está diseñada para utilizarse tanto en flujos conversacionales como en flujos agénticos.

En un flujo conversacional, la persona mantiene el control directo de la interacción. Puede proporcionar al asistente el contexto relevante, revisar sus propuestas y realizar o aprobar los cambios derivados del trabajo.

En un flujo agéntico, el agente puede disponer de acceso directo al proyecto y utilizar sus mecanismos de descubrimiento para localizar, cargar y aplicar el contexto necesario durante la ejecución de una tarea.

Ambos modos utilizan el mismo contexto canónico y están sujetos a las mismas reglas de autoridad, confianza y validación humana.

La diferencia reside en las capacidades disponibles y en cómo se desarrolla la interacción, no en la naturaleza o autoridad del contexto.

El trabajo puede combinar ambos modos.

Por ejemplo, una decisión puede explorarse inicialmente mediante conversación, incorporarse después al contexto canónico mediante validación humana y utilizarse posteriormente por un agente durante la ejecución autónoma de una tarea.

Del mismo modo, un agente puede detectar durante su trabajo una decisión pendiente, una inconsistencia o nuevo conocimiento que requiera intervención humana y devolver esa cuestión al flujo conversacional antes de continuar.

Context Library no presupone que el agente pueda modificar ficheros, ejecutar herramientas o acceder directamente al repositorio. Estas capacidades dependen de la herramienta y del entorno utilizados.

El modelo debe seguir siendo útil cuando la colaboración se limite a proporcionar contexto y recibir respuestas, y aprovechar capacidades agénticas adicionales cuando estén disponibles.

---

# Idioma

Context Library no impone un idioma de trabajo.

Los documentos de `core/` y los ficheros `AGENTS.md` se mantendrán en inglés.

`core/` contiene reglas reutilizables destinadas a aplicarse entre distintos proyectos, herramientas y proveedores. Los ficheros `AGENTS.md` actúan como mecanismos de descubrimiento dirigidos principalmente a herramientas y agentes de IA.

En ambos casos, el uso del inglés favorece su portabilidad y reutilización independientemente del idioma de trabajo de cada proyecto.

Cada proyecto utilizará el idioma que resulte más adecuado para las personas que participan en él y para su destino previsto.

Los proyectos destinados previsiblemente a una comunidad internacional pueden adoptar inglés desde su inicio.

La optimización del consumo de tokens no debe realizarse a costa de dificultar el uso humano del contexto.

La traducción puede realizarse posteriormente cuando exista una necesidad real.

---
# Secretos

Los valores de secretos no forman parte del contexto.

No deben almacenarse en la documentación de contexto ni incorporarse a sistemas de control de versiones.

El conocimiento necesario para utilizar un secreto sí puede formar parte del contexto.

Los documentos pueden indicar:

- qué secreto es necesario;
- para qué se utiliza;
- dónde o cómo debe obtenerse;
- cómo debe ser referenciado por herramientas o aplicaciones.

Nunca deben contener su valor.

Esta separación permite documentar completamente una integración o configuración sin convertir Context Library en un mecanismo de almacenamiento de secretos.

---

# Obsolescencia

El contexto canónico debe representar el conocimiento vigente del proyecto.

A medida que un proyecto evoluciona, parte de su contexto puede quedar desactualizado, ser sustituido por nuevas decisiones o dejar de resultar aplicable.

Mantener contexto obsoleto como si siguiera vigente puede ser más perjudicial que no disponer de ese contexto, ya que asistentes, agentes y personas pueden utilizarlo como fuente de verdad.

Por este motivo, el mantenimiento del contexto incluye su revisión, actualización y eliminación.

Cuando se detecta información posiblemente obsoleta, debe determinarse si corresponde:

- actualizarla;
- sustituirla;
- eliminarla;
- conservarla explícitamente como obsoleta o histórica cuando siga teniendo relevancia para el trabajo actual o futuro.

Por ejemplo, el uso de una API obsoleta puede seguir formando parte del contexto cuando existe código legacy que depende de ella. En ese caso, el conocimiento relevante no es que la API siga siendo válida, sino que existe esa dependencia, dónde se encuentra y cómo debe tratarse.

El conocimiento histórico no debe confundirse con el contexto vigente.

Context Library no pretende conservar dentro del contexto canónico un registro completo de todos los estados anteriores del conocimiento. El sistema de control de versiones proporciona el histórico de los documentos cuando sea necesario consultarlo.

La detección de obsolescencia puede realizarla una persona o un agente, pero cualquier modificación del contexto canónico sigue sujeta al mecanismo normal de validación humana.

Las reglas normativas para el mantenimiento del conocimiento obsoleto se definen en `core/`.

---
# Observación del sistema

El contexto mantenido no es la única fuente de conocimiento disponible durante el trabajo.

Asistentes y agentes pueden descubrir información relevante observando el propio sistema: su código, configuración, comportamiento, infraestructura, pruebas, errores, documentación o artefactos existentes.

Esta capacidad permite detectar conocimiento que todavía no ha sido documentado, así como diferencias entre el contexto mantenido y el estado real del sistema.

Sin embargo, observar algo no lo convierte automáticamente en contexto canónico.

Debe distinguirse entre:

- hechos directamente observados;
- interpretaciones o inferencias derivadas de esos hechos;
- decisiones que puedan tomarse a partir de ellos.

Cuando una observación revele conocimiento con posible valor persistente, puede proponerse su incorporación al contexto mediante el proceso normal de gestión del conocimiento y validación humana.

Cuando la observación contradiga el contexto existente, la contradicción debe hacerse explícita y resolverse antes de modificar la fuente de verdad.

La incertidumbre también forma parte de la información disponible. Cuando la evidencia no permita establecer una conclusión suficientemente fiable, ésta no debe convertirse artificialmente en una afirmación canónica.

La observación del sistema permite que Context Library evolucione a partir del trabajo real sin convertir automáticamente cada descubrimiento de un agente en conocimiento persistente.

---
# Evolución y obsolescencia de Context Library

Context Library se desarrolla en un ecosistema experimental y rápidamente cambiante.

Su arquitectura, estructura y mecanismos actuales no se consideran un objetivo permanente.

Si aparecen estándares ampliamente adoptados que resuelven mejor alguno de los problemas abordados por CL, el proyecto debe poder adoptarlos, integrarse con ellos o sustituir sus mecanismos propios.

Del mismo modo, las convenciones específicas creadas por Context Library deben abandonarse cuando dejen de aportar valor frente a alternativas más simples, interoperables o ampliamente adoptadas.

No debe mantenerse una solución únicamente porque haya sido diseñada dentro del proyecto.

Context Library debe evitar que sus propias decisiones de implementación se conviertan en dependencias innecesarias para el conocimiento que mantiene.

El activo que debe preservarse es el conocimiento, junto con la información necesaria para comprender su autoridad, procedencia y condiciones de uso.

La estructura, los formatos y los mecanismos utilizados para organizar, descubrir o proporcionar ese conocimiento a las herramientas pueden cambiar.

---

# Principios de diseño

- Independencia de proveedor.
- Git y Markdown como fuente canónica.
- Contexto controlado por las personas.
- Validación humana antes de convertir un cambio en contexto canónico.
- Descubrimiento progresivo del contexto.
- Mínima carga de contexto necesaria.
- Frontera explícita entre contenido confiable y externo.
- Copiar antes que sincronizar.
- Procedencia y licencias verificables.
- Máxima simplicidad operativa.
- Automatizar únicamente cuando exista una necesidad real.
- El contexto debe ser autosuficiente para la unidad de trabajo para la que haya sido diseñado.
- El contexto debe poder componerse y especializarse sin duplicar innecesariamente conocimiento compartido.
- Distinguir observación, inferencia y conocimiento canónico.
- La evolución debe responder a necesidades reales, no a complejidad anticipada.
- Adoptar estándares externos cuando resulten mejores que soluciones propias.
- Preservar el conocimiento por encima de la estructura que lo contiene.

---

# Fuera del MVP

No forman parte inicialmente de Context Library:

- CLI propia;
- `cl init` u otros mecanismos de inicialización automática de proyectos;
- sincronización automática entre proyectos;
- submodules como mecanismo prescrito de distribución;
- gestores de dependencias;
- sistemas RAG propios;
- bases de datos;
- clasificación de documentos públicos o privados;
- scheduler propio;
- múltiples perfiles dentro de `user/`;
- carga automática de Skills externos;
- esquemas complejos de metadatos;
- adaptadores específicos de proveedor sin un caso de uso demostrado;
- automatización de mecanismos que todavía no hayan sido validados mediante uso real.

Estas capacidades sólo se incorporarán si la experiencia real demuestra su necesidad.