# camadas do restaurante

## Domínio
Representa Mesa, Categoria, Produto, Pedido e ItemPedido.
Comtém cálculos com o subtotal de um item.
não conhece banco de dados, SOAP ou REST.

## Aplicação
coorderna as operações na classe Restaurante.
Exemplo de regra: mesa ocupada não pode abrir outro pedido.
Use a interface Repositório para consultar e gravar dados.

## infraestrutura
Implementa Reposit´rio na classe JdbcRepositório.
executa SQL e controla as conexões com o banco.

## Entradas SOAP e REST
Recebem solicitações, em chamam Restaurante e devolvem respostas.
A regra de negócio fica na aplicação.

## Dependências do núcleo
A seta significa: uma parte conhece tipos da outra.

aplicação -> dominio
infraestrutura -> aplicação e dominio

A intreface Pepositorio fica na aplicação.
A implementação JdbcRepositoio fica na infraestrutura.
a aplicação usa a intreface sem depender da implementação JDBC.

## Exemplo: abrir pedido
1. Soap ou REST recebe a solicitação com o identificador da mesa.
2. A aplicação consulta a mesa pela interface Repositório.
3. Se a mesa estiver ocupada, a aplicação recusa a operação.
4. Se estiver live, cria o pedido e ocupa a mesa na mesma transação.
5. SOAP ou REST devolve o resultado ao cliente.

As consultas e gravações desses passos são executadas 
pela infraestrutura, por meio da interface Repositório.



