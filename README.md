<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Criar Post</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

    <h1>Criar Post</h1>

    <form id="post-form">
        <input type="text" id="titulo" placeholder="Digite o título do post" required>
        <textarea id="conteudo" placeholder="Escreva o conteúdo do post" rows="5" required></textarea>
        <button type="submit">Publicar</button>
    </form>

    <section id="post-output">
        <h2 id="renderizador-titulo"></h2>
        <p id="renderizador-conteudo"></p>
    </section>

    <script src="script.js"></script>

</body>
</html>
* {
    box-sizing: border-box;
}

body {
    font-family: system-ui, sans-serif;
    margin: 0;
    padding: 20px;
    background-color: #f4f4f9;
}

h1 {
    text-align: center;
}

form {
    max-width: 500px;
    margin: 0 auto;
    padding: 20px;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

input, textarea, button {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
}

button {
    background-color: #4CAF50;
    color: white;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}

#post-output {
    max-width: 500px;
    margin: 20px auto;
    padding: 20px;
    background-color: white;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h2 {
    margin: 0;
    font-size: 24px;
}

p {
    font-size: 16px;
    color: #333;
}
const form = document.querySelector('#post-form');
const titulo = document.querySelector('#titulo');
const conteudo = document.querySelector('#conteudo');
const renderizadorTitulo = document.querySelector('#renderizador-titulo');
const renderizadorConteudo = document.querySelector('#renderizador-conteudo');

// Função para lidar com a submissão do formulário
form.addEventListener('submit', function (e) {
    e.preventDefault(); // Previne o comportamento padrão do form

    // Criando o objeto de dados para envio
    const data = {
        title: titulo.value,
        body: conteudo.value,
        userId: 1
    };

    // Requisição POST para a API
    fetch('https://jsonplaceholder.typicode.com/posts', {
        method: 'POST',
        body: JSON.stringify(data),
        headers: {
            'Content-type': 'application/json; charset=UTF-8'
        }
    })
    .then(response => response.json())
    .then(data => {
        // Renderizando os dados retornados da API
        renderizadorTitulo.innerHTML = data.title;
        renderizadorConteudo.innerHTML = data.body;
    })
    .catch(error => console.error('Erro:', error));
});
