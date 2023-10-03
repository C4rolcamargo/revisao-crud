# revisao-crud
const mysql = require('mysql');

// Configuração de conexão com o banco de dados
const connection = mysql.createConnection({
  host: 'local',
  user: 'aluno',
  password: '12345',
  database: 'database',
});

function inserirRegistros() {
  connection.connect((err) => {
    if (err) {
      console.error('Erro ao conectar ao banco de dados:', err);
      return;
    }

  
    const registros = [];
    for (let i = 1; i <= 20; i++) {
      registros.push({ name: `Cliente ${i}`, address: `Endereço ${i}` });
    }

  
    connection.query('INSERT INTO customers (name, address) VALUES ?', [registros.map((registro) => [registro.name, registro.address])], (error, results) => {
      if (error) {
        console.error('Erro ao inserir registros:', error);
      } else {
        console.log('Registros inseridos com sucesso!');
      }

    
      connection.end();
    });
  });
}

inserirRegistros();

