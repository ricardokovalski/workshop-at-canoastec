# Use apenas um ponto por linha

O ponto nada mais é que a famosa setinha **->** do PHP.

Essa regra reforça o OCP e facilita a leitura do código.

É um exemplo da **Lei de Deméter** - não deve encadear chamadas de métodos.

> :warnig: Tem uma exceção nesta regra. Não é aplicada em **Fluent Interfaces** e a qualquer coisa que se implemente o **Chaining Pattern** (muito usado em **Query Builders**).