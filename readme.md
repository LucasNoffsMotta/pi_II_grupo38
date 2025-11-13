##Comandos SQL Utilizados para criar as tabelas conforme o diagrama UML


CREATE TABLE Pessoa (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    endereco VARCHAR(150),
    telefone VARCHAR(20)
);

CREATE TABLE PessoaFisica (
    pessoaId INT PRIMARY KEY,
    cpf VARCHAR(11) UNIQUE NOT NULL,
    dataNascimento DATE,
    rg VARCHAR(20),
    FOREIGN KEY (pessoaId) REFERENCES Pessoa(id)
);

CREATE TABLE PessoaJuridica (
    pessoaId INT PRIMARY KEY,
    cnpj VARCHAR(14) UNIQUE NOT NULL,
    razaoSocial VARCHAR(120),
    nomeFantasia VARCHAR(120),
    FOREIGN KEY (pessoaId) REFERENCES Pessoa(id)
);

CREATE TABLE Aluno (
    pessoaId INT PRIMARY KEY,
    matricula VARCHAR(20) UNIQUE NOT NULL,
    dataIngresso DATE,
    statusAcademico VARCHAR(30),
    FOREIGN KEY (pessoaId) REFERENCES Pessoa(id)
);

CREATE TABLE Professor (
    pessoaId INT PRIMARY KEY,
    siape VARCHAR(20) UNIQUE NOT NULL,
    titulacao VARCHAR(50),
    areaAtuacao VARCHAR(100),
    departamentoId INT,
    FOREIGN KEY (pessoaId) REFERENCES Pessoa(id),
    FOREIGN KEY (departamentoId) REFERENCES Departamento(id)
);

CREATE TABLE Departamento (
    id INT PRIMARY KEY AUTO_INCREMENT,
    codigo VARCHAR(10) UNIQUE NOT NULL,
    nome VARCHAR(100),
    sigla VARCHAR(10)
);

CREATE TABLE Curso (
    id INT PRIMARY KEY AUTO_INCREMENT,
    codigo VARCHAR(10),
    nome VARCHAR(100),
    cargaHoraria INT
);

CREATE TABLE Fornecedor (
    id INT PRIMARY KEY AUTO_INCREMENT,
    codigoFornecedor VARCHAR(20),
    tipoFornecedor VARCHAR(50),
    servicosPrestados VARCHAR(200)
);


CREATE TABLE AlunoCurso (
    alunoId INT,
    cursoId INT,
    PRIMARY KEY (alunoId, cursoId),
    FOREIGN KEY (alunoId) REFERENCES Aluno(pessoaId),
    FOREIGN KEY (cursoId) REFERENCES Curso(id)
);

CREATE TABLE ProfessorCurso (
    professorId INT,
    cursoId INT,
    PRIMARY KEY (professorId, cursoId),
    FOREIGN KEY (professorId) REFERENCES Professor(pessoaId),
    FOREIGN KEY (cursoId) REFERENCES Curso(id)
);
