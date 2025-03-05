```
from flask import Flask, jsonify, request

app = Flask(__name__)

# Simulamos una base de datos con una lista de tareas
tasks = [
    {"id": 1, "title": "Comprar leche", "done": False},
    {"id": 2, "title": "Aprender REST", "done": False}
]

# Función auxiliar para encontrar una tarea por ID
def find_task(task_id):
    return next((task for task in tasks if task['id'] == task_id), None)

# Ruta para obtener todas las tareas
@app.route('/tasks', methods=['GET'])
def get_tasks():
    return jsonify({"tasks": tasks})

# Ruta para obtener una tarea específica
@app.route('/tasks/<int:task_id>', methods=['GET'])
def get_task(task_id):
    task = find_task(task_id)
    if task is None:
        return jsonify({"error": "Tarea no encontrada"}), 404
    return jsonify({"task": task})

# Ruta para crear una nueva tarea
@app.route('/tasks', methods=['POST'])
def create_task():
    if not request.json or 'title' not in request.json:
        return jsonify({"error": "El título es requerido"}), 400
    task = {
        'id': tasks[-1]['id'] + 1,
        'title': request.json['title'],
        'done': False
    }
    tasks.append(task)
    return jsonify({"task": task}), 201

# Ruta para actualizar una tarea
@app.route('/tasks/<int:task_id>', methods=['PUT'])
def update_task(task_id):
    task = find_task(task_id)
    if task is None:
        return jsonify({"error": "Tarea no encontrada"}), 404
    task['title'] = request.json.get('title', task['title'])
    task['done'] = request.json.get('done', task['done'])
    return jsonify({"task": task})

# Ruta para eliminar una tarea
@app.route('/tasks/<int:task_id>', methods=['DELETE'])
def delete_task(task_id):
    task = find_task(task_id)
    if task is None:
        return jsonify({"error": "Tarea no encontrada"}), 404
    tasks.remove(task)
    return jsonify({"result": True})

if __name__ == '__main__':
    app.run(debug=True)
```
