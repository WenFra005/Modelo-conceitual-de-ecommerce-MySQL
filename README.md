# **📊 Modelo Conceitual e Relacional de Banco de Dados - E-commerce**
Este projeto apresenta um **modelo conceitual** de banco de dados relacional para um sistema de **e-commerce**, utilizando o MySQL como sistema de gerenciamento. O modelo foi elaborado seguindo as 3 Formas Normais (3FN) para garantir a consistência, integridade e performance dos dados.
## **🚀 Objetivo do Projeto**
O objetivo deste banco de dados é organizar e armazenar as informações necessárias para o funcionamento de uma plataforma de venda de produtos online, com suporte a múltiplos vendedores, fornecedores e clientes. O modelo considera as seguintes necessidades do sistema:

1. Venda de produtos por diferentes vendedores na mesma plataforma.
2. Cada produto tem um fornecedor associado.
3. Clientes podem realizar pedidos, utilizando diferentes formas de pagamento.
4. Suporte a clientes PF (Pessoa Física) ou PJ (Pessoa Jurídica), com endereços associados.
5. Controle de status do pedido e código de rastreamento para envio.

## **📋 Descrição Geral do Sistema**
O sistema permite o cadastro e a gestão de:

* Contas de usuários (Pessoa Física ou Jurídica).
* Pedidos compostos por um ou mais produtos.
* Produtos vendidos na plataforma, com fornecedores associados.
* Vendedores terceiros que disponibilizam produtos.
* Endereços para contas, fornecedores e pedidos.
* Formas de pagamento associadas às contas.
  
## **🧩 Descrição das Entidades**
1. Conta
* Representa uma conta de usuário, que pode ser **Pessoa Física** (PF) ou **Pessoa Jurídica** (PJ).
* Contém dados como:
  * ``nome_Conta``
  * ``email_Conta``
  * ``status_Conta``
  * ``data_cadastro_Conta``
* **Relacionamentos**:
**1:1** com ``Pessoa_Fisica`` ou ``Pessoa_Juridica`` (herança).
**1:N** com ``Endereco``.
**1:N** com ``Forma_Pagamento``.
**1:N** com ``Pedido``.
----

2. **Pessoa_Fisica e Pessoa_Juridica**
* Subclasses de ``Conta`` que representam clientes PF e PJ, respectivamente.
* **Atributos principais**:
  * ``Pessoa_Fisica``: ``cpf``
  * ``Pessoa_Juridica``: ``cnpj``
* **Relacionamento**:
  * **1:1** com ``Conta`` (cada conta só pode ser PF ou PJ).
----

3. **Pedido**
* Representa uma compra feita por um cliente.
* **Atributos principais**:
  * **status_Pedido** (ENUM: entregue, em andamento, cancelado, etc.)
  * ``data_Pedido``
  * ``endereco_entrega_Pedido``
  * ``codigo_rastreamento``
* **Relacionamentos**:
  * **N:1** com ``Conta`` (cliente que realizou o pedido).
  * **N:1** com ``Endereco`` (endereço de entrega do pedido).
  * **1:N** com ``Item_Pedido`` (itens que compõem o pedido).
----

4. **Item_Pedido**
* Representa os produtos que fazem parte de um pedido.
* **Atributos principais**:
  * ``quantidade_Item_Pedido``
  * ``preco_unitario_Item_Pedido``
* **Relacionamentos**:
  * **N:1** com **Pedido**.
  * **N:1** com **Produto**.
----

5. **Produto**
* Representa os produtos disponíveis na plataforma.
* **Atributos principais**:
  * ``nome_Produto``
  * ``estoque_Produto``
  * ``preco_Produto``
* **Relacionamentos**:
  * **N:1** com ``Categoria``.
  * **N:M** com ``Fornecedor`` (via ``Fornecimento_de_Produtos``).
  * **N:M** com ``Vendedor`` (via ``Venda_de_Vendedor``).
----

6. **Vendedor**
* Representa os vendedores (terceiros) que ofertam produtos na plataforma.
* **Atributos principais**:
  * ``nome_Vendedor``
  * ``cpf_cnpj``
  * ``email_Vendedor``
* **Relacionamento**:
  * **1:N** com ``Endereco``.
  * **N:M** com ``Produto`` (via ``Venda_de_Vendedor``).
----

7. **Fornecedor**
* Representa os fornecedores dos produtos.
* **Atributos principais**:
  * ``nome_Fornecedor``
  * ``cnpj_Fornecedor``
* **Relacionamento**:
  * **1:N** com ``Endereco``.
  * **N:M** com ``Produto`` (via ``Fornecimento_de_Produtos``).
----

8. **Endereco**
* Representa os endereços associados a contas, fornecedores e vendedores.
* **Atributos principais**:
  * ``cep``
  * ``logradouro``
  * ``numero``
  * ``tipo_endereco`` (residencial, comercial, etc.)
* **Relacionamentos**:
  * **N:1** com ``Conta``.
  * **N:1** com ``Fornecedor``.
  * **N:1** com ``Vendedor``.
----

9. **Forma_Pagamento**
* Representa as formas de pagamento cadastradas por cada conta.
* **Atributos principais**:
  * ``tipo_Forma_Pagamento`` (cartão, boleto, pix, etc.)
  * ``detalhes_Forma_Pagamento``
* **Relacionamento**:
  * **N:1** com ``Conta``.
------
## 🔗 Relacionamentos entre as Entidades
|**Relacionamento**|**Descrição**|
|:---|:---|
|``Conta`` ↔ ``Pessoa_Fisica``|Uma conta é de Pessoa Física (1:1).|
|``Conta`` ↔ ``Pessoa_Juridica``|Uma conta é de Pessoa Jurídica (1:1).|
|``Conta`` ↔ ``Endereco``|Uma conta pode ter vários endereços (1:N).|
|``Conta`` ↔ ``Forma_Pagamento``|Uma conta pode ter várias formas de pagamento (1:N).|
|``Conta`` ↔ ``Pedido``|Uma conta pode realizar vários pedidos (1:N)|
|``Pedido`` ↔ ``Endereco``|Cada pedido está associado a um endereço (N:1).|
|``Pedido`` ↔ ``Item_Pedido``|Um pedido possui vários itens (N:1).|
|``Item_Pedido`` ↔ ``Produto``|Cada item corresponde a um produto (N:1).|
|``Produto`` ↔ ``Categoria``|Cada produto pertence a uma categoria (N:1).|
|``Produto`` ↔ ``Fornecedor``|Um produto pode ter vários fornecedores (N:M).|
|``Produto`` ↔ ``Vendedor``|Um produto pode ser vendido por vários vendedores (N:M).|
|``Fornecedor`` ↔ ``Endereco``|Cada fornecedor possui um endereço (1:N).|
|``Vendedor`` ↔ ``Endereco``|Cada vendedor possui um endereço (1:N).|

## 📈 Diagrama do Banco de Dados (Modelo ER)
O diagrama abaixo apresenta o modelo atualizado, com as entidades, relacionamentos e suas chaves primárias/estrangeiras:
<div align = "center">
  <img src = "https://github.com/WenFra005/Modelo-conceitual-de-ecommerce-MySQL/blob/main/modelo-conceitual/Modelo%20Conceitual.png" alt = "modelo conceitual" width = "700"/>
</div>

## 💻 Tecnologias Utilizadas
* **MySQL**🐬: Sistema de gerenciamento de banco de dados relacional.
* **MySQL Workbench**🛠: Ferramenta de modelagem e criação do banco de dados.
* **ChatGPT**🤖: IA generativa criada pela OpenAI para auxílio do desenvolvimento.
----
Caso tenha alguma dúvida ou sugestão, sinta-se à vontade para abrir uma issue ou entrar em contato! 😊🚀





