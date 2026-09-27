# Riesgo: acceso a tareas ajenas

## Qué podría ocurrir

Si la API no comprobase quién es el propietario de una tarea, un usuario podría modificar o eliminar tareas pertenecientes a otros usuarios.

## Cómo lo evita la aplicación

La API compara `task.ownerId` con `req.user.sub` antes de actualizar o eliminar una tarea.

`task.ownerId` representa el identificador del usuario propietario de la tarea, mientras que `req.user.sub` representa el identificador del usuario autenticado obtenido del token JWT.

Si ambos valores no coinciden, la aplicación devuelve un error `404` y no permite acceder ni modificar la tarea.

## Cómo lo demostramos

La prueba `aísla las tareas entre dos usuarios (previene IDOR)` utiliza dos usuarios diferentes. El segundo usuario intenta modificar una tarea del primero y debe recibir un código `404`, mientras que la tarea original permanece sin cambios.
