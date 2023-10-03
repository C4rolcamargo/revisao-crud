# revisao-crud

###Maquina1

const mysql = require('mysql');

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

###Maquina2

const mysql = require('mysql');

const connection = mysql.createConnection({
  host: 'seu-host',
  user: 'seu-usuario',
  password: 'sua-senha',
  database: 'seu-banco-de-dados',
});

function lerRegistros() {
  connection.connect((err) => {
    if (err) {
      console.error('Erro ao conectar ao banco de dados:', err);
      return;
    }

    connection.query('SELECT * FROM customers LIMIT 10', (error, results) => {
      if (error) {
        console.error('Erro ao ler registros:', error);
      } else {
        console.log('Registros lidos:');
        results.forEach((registro) => {
          console.log(`Nome: ${registro.name}, Endereço: ${registro.address}`);
        });
      }

      connection.end();
    });
  });
}

lerRegistros();

