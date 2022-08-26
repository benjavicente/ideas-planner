<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/water.css@2/out/water.css">

# Ideas planner

## Extructura de datos

### Opción / Ramo

Cada opción tiene requerimientos relacionados a otra opción / ramos.

### Grupo

Por ejemplo, el grupo de ramos de dinamica que se pueden hacer. Un major, titulo, minor y track son un grupo, pero son elegidos por una elección. **Un grupo puede pertenecer a una categoría en un grupo padre**. Por ejemplo, un major puede ser disciplinario o interdisciplinario, un minor de especialidad o amplitud, un título civil o industrial.

Los grupos son la principal estructura de datos y debiese comportarse como nodos de una red que termina en ramos.

### Elección

Elecciones de la planificación. Major, minor, track opcional, titulo

### Carrera

Base de la planificación. No necesariamente una carrera con el mismo nombre es la misma (una carrera puede tener diferentes planificaciones en distintos tiempos).

### Periodos

Los semestres. Deben ser ordenados. Probablemente, se pueden definir como una lista ordenada, donde cada valor especifica propiedades de cada periodo (como créditos máximos).

## Reglas

El sistema debe tener un sistema de reglas que permita asociar elecciones, ramos, grupos, semestres, etc. Además, un máximo de créditos en cada parte. Globalmente, se podría definir si cursos que son válidos en múltiples grupos añaden créditos máximos distintos.

### Requisitos

Una opción / ramo podría tener una lista de requisitos, en un formato con and y or.

### Relaciones entre grupos y selecciones

Por ejemplo, un grupo que representa un minor de especialidad debera permitirse solo si `selected.major == especialidad_minor`


## Interfaz

El interfaz podría tener las siguientes características:

- Debe permitir su uso con solo mouse y con solo teclado.
- No debería esperar al servidor a que responda para poder continuar a hacer una acción. Una consulta no debería frenar el uso de la plataforma, a menos que la acción que se realice necesita aprobación del servidor (modificar el semestre de un curso no debiese esperar a una consulta, pero si guardar la planificación en el servidor).
- Solo debe haber una fila para cada columna de semestres. Esto permitirá añadir más columnas fácilmente y hará que el interfaz sea más familiar. El contenedor de estas columnas deberá permitir scroll sin perder el contenido del resto de la página. Inicialmente, se podría mostrar la planificación desde el semestre actual, para no mostrar inicialmente lo que ya no se puede cambiar en la planificación.
- Cada columna del semestre podría tener un enlace a busca-cursos para cargar ese horario (es super fácil, está en UCalendar).


Deberían existir cerca de 5 páginas:

- Listado de mayas del usuario (estudiante)
- Planificación de maya (estudiante)
- Panel de entrada de administración (administrador)
- Panel de creación de mayas (administrador)
- Panel de estadísticas (administrador)


## Ejemplos

### de Elección de Major y Minor

<label for="major">Elige un Major:</label>
<select id="major">
	<optgroup label="Disciplinarios">
		<option>Ingeniería y Ciencias Ambientales</option>
		<option>Computación y Sistemas de Información</option>
		<option>Ingeniería de Construcción</option>
		<option>Ingeniería Eléctrica</option>
		<option>Ingeniería Estructural</option>
		<option>Ingeniería Geotécnica</option>
		<option>Ingeniería Hidráulica</option>
		<option>Ingeniería Mecánica</option>
		<option>Ingeniería Minera</option>
		<option>Ingeniería Química</option>
		<option>Ingeniería en Investigación Operativa</option>
		<option>Ingeniería de Sistemas de Transportes</option>
		<option>Ingeniería de Software</option>
	</optgroup>
	<optgroup label="Interdisciplinarios">
		<option>Geociencias</option>
		<option>Ingeniería Biológica</option>
		<option>Ingeniería Biomédica</option>
		<option>Ingeniería Matemática</option>
		<option>Ingeniería y Arquitectura</option>
		<option>Ingeniería, Diseño e Innovación</option>
		<option>Ingeniería Robótica</option>
		<option>Ingeniería Física</option>
		<option>Ingeniería Civil</option>
	</optgroup>
</select>

<label for="minor">Elige un Minor:</label>
<select id="minor">
	<optgroup label="Amplitud">
		<option data-rule="selected.major != 'Ingeniería de Sistemas de Transportes'">Externalidades de Transporte</option>
		<option data-rule="selected.major != 'Ingeniería Biológica'">Fundamentos de Ingeniería Biológica</option>
		<option data-rule="selected.major != 'Geociencias'">Geociencias</option>
		<option data-rule="selected.major != '...'">Ingeniería de Construcción</option>
		<option data-rule="selected.major != '...'">Ingeniería Eléctrica</option>
		<option data-rule="selected.major != '...'">Ingeniería Estructural</option>
		<option data-rule="selected.major != '...'">Ingeniería Geotécnica</option>
		<option data-rule="selected.major != '...'">Ingeniería Hidráulica y Ambiental</option>
		<option data-rule="selected.major != '...'">Ingeniería Industrial</option>
		<option data-rule="selected.major != '...'">Ingeniería Minera</option>
		<option data-rule="selected.major != '...'">Ingeniería Matemática</option>
		<option data-rule="selected.major != '...'">Ingeniería Mecánica</option>
		<option data-rule="selected.major != '...'">Ingeniería Química</option>
		<option data-rule="selected.major != '...'">Innovación Tecnológica</option>
		<option data-rule="selected.major != '...'">Logística y Transporte de carga</option>
		<option data-rule="selected.major != '...'">Matemáticas Aplicadas</option>
		<option data-rule="selected.major != '...'">Programación</option>
		<option data-rule="selected.major != '...'">Sistemas de Transporte</option>
		<option data-rule="selected.major != '...'">Tecnologías de la Información</option>
	</optgroup>
	<optgroup label="Profundidad">
		<option data-rule="selected.major == '...'">Articulación con Ingeniería Civil</option>
		<option data-rule="selected.major == '...'">Articulación con Ingeniería de Transporte</option>
		<option data-rule="selected.major == 'Ingeniería y Arquitectura'">Articulación en Arquitectura</option>
		<option data-rule="selected.major == '...'">Articulación en Ingeniería de Construcción</option>
		<option data-rule="selected.major == '...'">Articulación en Premedicina</option>
		<option data-rule="selected.major == '...'">Articulación en Proyectos de Diseño</option>
		<option data-rule="selected.major == '...'">Articulación Ingeniería Civil (Major Ingeniería y Arquitectura)</option>
		<option data-rule="selected.major == '...'">Bioingeniería</option>
		<option data-rule="selected.major == 'Ingeniería de Software'">Data Science y Analytics</option>
		<option data-rule="selected.major == '...'">Fundamentos Científicos y Tecnológicos de la Computación</option>
		<option data-rule="selected.major == '...'">Gestión y Operaciones Mineras</option>
		<option data-rule="selected.major == '...'">Geología Ingenieril</option>
		<option data-rule="selected.major == '...'">Ingeniería Biomédica</option>
		<option data-rule="selected.major == '...'">Ingeniería de Alimentos</option>
		<option data-rule="selected.major == '...'">Ingeniería de Procesos</option>
		<option data-rule="selected.major == '...'">Ingeniería Eléctrica</option>
		<option data-rule="selected.major == '...'">Logística Minera (para Transporte)</option>
		<option data-rule="selected.major == '...'">Mecatrónica</option>
		<option data-rule="selected.major == '...'">Robótica</option>
		<option data-rule="selected.major == '...'">Teoría y Aplicación de Ingeniería Matemática</option>
	</optgroup>
</select>

<script>
	document.addEventListener("DOMContentLoaded", () => {
		const major = document.getElementById("major");
		const minor = document.getElementById("minor");
		const options = minor.querySelectorAll("option");

		major.addEventListener("change", () => {
			const selectedMajor = major.value;
			options.forEach(option => {
				// Esto debería estar mucho mejor implementado obviamente
				const isEq = option.dataset.rule.includes("==");
				if (isEq == option.dataset.rule.includes(selectedMajor)) {
					option.hidden = false;
				} else {
					option.hidden = true;
				}
			})
		})
	})
</script>
