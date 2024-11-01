💥 Explicação do Back-End 💥
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
➡ Bibliotecas Utilizadas:

Express: Framework web para facilitar a criação de aplicações em Node.js.
SQLite3: Biblioteca para manipulação de bancos de dados SQLite.
Bcrypt: Usada para criptografar senhas, garantindo segurança no armazenamento.
JSON Web Token (JWT): Permite a autenticação e autorização segura de usuários.
CORS: Middleware que habilita o compartilhamento de recursos entre diferentes origens.
Socket.IO: Facilita a comunicação em tempo real entre o servidor e os clientes.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

➡ Configuração do Servidor:


    const server = http.createServer(app);
    const io = new Server(server, {
        cors: {
            origin: '*', // Habilita CORS para qualquer origem
            methods: ['GET', 'POST'],
        }
    });

Este trecho configura o servidor HTTP e o Socket.IO, permitindo comunicação em tempo real com CORS habilitado.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



➡ Banco de Dados e Criação de Tabelas:


    const db = new sqlite3.Database('banco-de-dados.db');
    db.serialize(() => {
        db.run(`CREATE TABLE IF NOT EXISTS usuarios (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            username TEXT UNIQUE,
            password TEXT
        )`);
        db.run(`CREATE TABLE IF NOT EXISTS dados_sensores (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            sensor_id INTEGER,
            temperatura REAL,
            umidade REAL,
            timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
        )`);
    });

Este bloco inicializa um banco de dados SQLite e cria as tabelas usuarios e dados_sensores caso não existam.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



➡ Rotas:

Rota para Cadastrar um Novo Usuário:

    app.post('/register', async (req, res) => {
        // Código para registro de usuário
    });

Permite o registro de novos usuários, com validação para evitar duplicações e criptografia de senhas.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



Rota para Login:

    app.post('/login', (req, res) => {
        // Código para autenticar usuários
    });

Autentica usuários e gera um token JWT que pode ser usado para acessar rotas protegidas.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Rota para Buscar Dados dos Sensores (Protegida por JWT):

    app.get('/dados-sensores', authenticateJWT, (req, res) => {
        // Código para buscar dados
    });
    
Retorna todos os dados dos sensores, acessível apenas para usuários autenticados.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Rota para Inserir Dados dos Sensores:

    app.post('/dados-sensores', async (req, res) => {
        // Código para inserir dados
    });
Permite a inserção de dados dos sensores e emite um evento via Socket.IO para atualização em tempo real.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Rota para Limpar Todos os Dados da Tabela (Protegida por JWT):

    app.delete('/limpar-dados', authenticateJWT, (req, res) => {
        // Código para limpar dados
    });
Remove todos os dados da tabela de sensores, acessível somente a usuários autenticados.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
➡ Função para Inserir Dados e Disparar Eventos:


    async function addSensorData(newData) {
        // Insere dados no banco e emite evento
    }
Essa função insere dados recebidos dos sensores e emite um evento para todos os clientes conectados.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

💥 Rodando a Aplicação 💥

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

➡ Para executar a aplicação, faça o fork do repositório, baixe-o e abra no Visual Studio Code. Utilize o terminal com "Ctrl + J" e execute:

bash
Copiar código
npm install
npm start
➡ Certifique-se de que o front-end esteja configurado para se conectar ao servidor.
