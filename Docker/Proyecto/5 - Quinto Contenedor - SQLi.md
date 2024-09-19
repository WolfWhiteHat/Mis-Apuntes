




Lo primero será crear un formulario de registro con HTML y CSS:
```html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Formulario de Registro</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #000000;
        color: #ffffff;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }
    form {
        background-color: rgba(255, 255, 255, 0.1);
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0px 0px 10px 0px rgba(255, 255, 255, 0.3);
    }
    h2 {
        text-align: center;
        color: #ffffff;
    }
    input[type="text"], input[type="password"] {
        width: 100%;
        padding: 10px;
        margin: 8px 0;
        border: 1px solid #ffffff;
        border-radius: 5px;
        box-sizing: border-box;
        background-color: rgba(255, 255, 255, 0.1);
        color: #ffffff;
    }
    input[type="submit"] {
        width: 100%;
        background-color: #4caf50;
        color: white;
        padding: 14px 20px;
        margin: 8px 0;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }
    input[type="submit"]:hover {
        background-color: #45a049;
    }
</style>
</head>
<body>
    <form action="#" method="post">
        <h2>Registro</h2>
        <label for="username">Usuario:</label>
        <input type="text" id="username" name="username" required>
        <label for="password">Contraseña:</label>
        <input type="password" id="password" name="password" required>
        <input type="submit" value="Registrarse">
    </form>
</body>
</html>
```
Y ahora en el backend vamos a crear el siguiente código hecho en Python para establecer la conexión con una base de datos MySQL.