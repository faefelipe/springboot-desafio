# Desafio Backend Itaú - API de Transações e Estatísticas

Implementação do desafio técnico de backend do Itaú utilizando **Java 21** e **Spring Boot**. A API é responsável por receber transações financeiras e calcular estatísticas em tempo real (dos últimos 60 segundos) com operações em memória, garantindo alta performance, validação estrita de dados e tratamento adequado de códigos HTTP.

---

## 🚀 Tecnologias Utilizadas

* **Linguagem:** Java 21
* **Framework:** Spring Boot 3+ (Spring Web, Spring Validation)
* **Gerenciador de Dependências:** Apache Maven
* **Estatísticas:** `DoubleSummaryStatistics` (Streams API do Java)
* **Controle de Versão:** Git (seguindo o padrão *Conventional Commits*)

---

## 📌 Requisitos e Regras de Negócio

1. **Armazenamento em Memória:** As transações são mantidas em memória para garantir baixa latência.
2. **Validação Temporal:** Transações com datas futuras não são aceitas.
3. **Validação de Valor:** Valores negativos não são aceitos.
4. **Cálculo de Estatísticas:** Apenas as transações ocorridas nos **últimos 60 segundos** são computadas para as métricas de `count`, `sum`, `avg`, `min` e `max`.

---

## 📡 Endpoints da API

### 1. Criar Transação
Recebe uma nova transação financeira e armazena em memória.

* **Método:** `POST`
* **Rota:** `/transacao`
* **Body:**
```json
{
  "valor": 120.50,
  "dataHora": "2026-08-24T20:30:00.000Z"
}

Respostas:

201 Created: Transação aceita e gravada com sucesso.

422 Unprocessable Entity: Transação no futuro ou valor menor que 0.

400 Bad Request: JSON malformatado ou campos nulos/inválidos.

2. Deletar Transações
Limpa todos os registros de transações em memória.

Método: DELETE

Rota: /transacao

Respostas:

200 OK: Todas as transações foram apagadas com sucesso.

3. Obter Estatísticas
Calcula e retorna as métricas das transações registradas nos últimos 60 segundos.

Método: GET

Rota: /estatistica

Resposta (200 OK):

JSON
{
  "count": 10,
  "sum": 1234.56,
  "avg": 123.456,
  "min": 10.0,
  "max": 500.0
}
(Caso não existam transações nos últimos 60 segundos, todos os campos numéricos retornam 0 ou 0.0).

⚙️ Como Executar o Projeto
Pré-requisitos
JDK 21 instalado

Git instalado

Passo a Passo
Clone o repositório:

Bash
git clone [https://github.com/faefelipe/springboot-desafio.git](https://github.com/faefelipe/springboot-desafio.git)
cd springboot-desafio
Compile e execute a aplicação:

Bash
./mvnw clean spring-boot:run
(No Windows, utilize mvnw.cmd clean spring-boot:run).

A aplicação estará disponível em: http://localhost:8080

🧪 Exemplos de Teste via cURL
Cadastrar Transação:

Bash
curl -X POST http://localhost:8080/transacao \
  -H "Content-Type: application/json" \
  -d '{
    "valor": 100.00,
    "dataHora": "'$(date -u +"%Y-%m-%dT%H:%M:%S.000Z")'"
  }'
Consultar Estatísticas:

Bash
curl -X GET http://localhost:8080/estatistica
Limpar Transações:

Bash
curl -X DELETE http://localhost:8080/transacao
👨‍💻 Autor
Desenvolvido por Felipe Almeida.

GitHub: @faefelipe
