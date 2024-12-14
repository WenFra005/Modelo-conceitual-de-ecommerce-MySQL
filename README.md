# Modelo Conceitual e Relacional de Banco de Dados - E-commerce
## Objetivo do Projeto
O objetivo deste projeto é criar um banco de dados eficiente para um sistema de e-commerce que permite a venda de produtos através de uma plataforma, respeitando os princípios de normalização (3FN) e garantindo a integridade dos dados.

## Descrição Geral do Sistema
O sistema permite o cadastro e a gestão de:

* Contas de usuários (Pessoa Física ou Jurídica).
* Pedidos compostos por um ou mais produtos.
* Produtos vendidos na plataforma, com fornecedores associados.
* Vendedores terceiros que disponibilizam produtos.
* Endereços para contas, fornecedores e pedidos.
* Formas de pagamento associadas às contas.
## Estrutura do Banco de Dados
### Entidades Principais
1. **Conta**
* Contém os dados principais da conta do cliente.
* A conta pode ser associada a uma Pessoa Física ou Pessoa Jurídica (Generalização/Especialização).
* Uma conta pode ter múltiplas formas de pagamento cadastradas.
  
2. **Pedido**
* Representa a compra realizada por uma conta.
* Contém informações como status, endereço de entrega e código de rastreamento.
* Um pedido pode conter um ou mais produtos.

3. **Produto**
* Produtos disponíveis na plataforma.
* Associados a uma categoria e a fornecedores.
* Vendidos por vendedores terceiros.

4. **Fornecedor**
* Cada fornecedor possui um endereço e fornece um ou mais produtos.

5. **Vendedor**
* Representa vendedores terceiros que disponibilizam produtos na plataforma.
* Cada vendedor possui um endereço associado.

6. **Forma de Pagamento**
* Diferentes formas de pagamento cadastradas para uma conta.

7. **Endereço**
* Entidade genérica para armazenar os endereços associados a contas, pedidos, fornecedores e vendedores.

## Relacionamentos
### Conta e Pessoa_Física/Pessoa_Jurídica
* Relacionamento **1:1**.
* **Generalização/Especialização**: Uma conta é exclusiva para uma pessoa física ou jurídica.

### Conta e Forma_Pagamento
* Relacionamento **1:N**: Uma conta pode ter várias formas de pagamento.

### Conta e Pedido
Relacionamento **1:N**: Uma conta pode realizar vários pedidos.

### Pedido e Item_Pedido
* Relacionamento **1:N**: Cada pedido pode conter um ou mais produtos.

### Produto e Categoria
Relacionamento **N:1**: Um produto pertence a uma única categoria.
**ON DELETE SET NULL**: Produtos não são excluídos quando uma categoria é removida.
**ON UPDATE CASCADE**: Atualizações no ID da categoria refletem nos produtos.

### Fornecedor e Produto (Fornecimento_de_produtos)
Relacionamento **N:M** (Tabela intermediária: ``Fornecimento_de_produtos``).
**ON DELETE CASCADE**: Exclusão de um fornecedor ou produto remove os registros associados.
**ON UPDATE CASCADE**: Atualizações são propagadas automaticamente.

### Vendedor e Produto (Venda_de_Vendedor)
Relacionamento **N:M** (Tabela intermediária: ``Venda_de_Vendedor``).


### Fornecedor e Endereco
Relacionamento **1:1**: Cada fornecedor possui um endereço.
**ON DELETE RESTRICT**: Não é permitido excluir um endereço associado a um fornecedor.
**ON UPDATE CASCADE**: Atualizações no endereço são refletidas.

### Vendedor e Endereco
Relacionamento **1:1**: Cada vendedor possui um endereço.

### Pedido e Endereco
Relacionamento **1:1**: Cada pedido possui um endereço de entrega.

## Diagrama do Banco de Dados
O diagrama abaixo apresenta o modelo atualizado, com as entidades, relacionamentos e suas chaves primárias/estrangeiras:
<div align = "center">
  <img src = "https://github.com/WenFra005/Modelo-conceitual-de-ecommerce-MySQL/blob/main/modelo-conceitual/Modelo%20Conceitual.png" alt = "modelo conceitual" width = "700"/>
</div>

(Substitua pelo caminho correto da imagem no repositório)

