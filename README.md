# Sistema-banc-rio-POST-gree-SQL-
-- Criar tabela de clientes
CREATE TABLE clientes (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(255) NOT NULL,
  cpf VARCHAR(11) UNIQUE NOT NULL,
  endereco VARCHAR(255) NOT NULL,
  telefone VARCHAR(20) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL
);

-- Criar tabela de contas
CREATE TABLE contas (
  id SERIAL PRIMARY KEY,
  cliente_id INTEGER NOT NULL REFERENCES clientes(id),
  tipo_conta VARCHAR(10) NOT NULL CHECK(tipo_conta IN ('corrente', 'poupanca')),
  saldo DECIMAL(10, 2) NOT NULL DEFAULT 0.00,
  data_abertura DATE NOT NULL DEFAULT CURRENT_DATE
);

-- Criar tabela de transações
CREATE TABLE transacoes (
  id SERIAL PRIMARY KEY,
  conta_id INTEGER NOT NULL REFERENCES contas(id),
  tipo_transacao VARCHAR(10) NOT NULL CHECK(tipo_transacao IN ('deposito', 'saque', 'transferencia')),
  valor DECIMAL(10, 2) NOT NULL,
  data_transacao TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);

-- Criar tabela de transferências
CREATE TABLE transferencias (
  id SERIAL PRIMARY KEY,
  conta_origem_id INTEGER NOT NULL REFERENCES contas(id),
  conta_destino_id INTEGER NOT NULL REFERENCES contas(id),
  valor DECIMAL(10, 2) NOT NULL,
  data_transferencia TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
);
