# Envolva suas collections em classes

Dado que temos um conjunto de registros e caso necessitamos manipular o mesmo, entende-se que é importante criar uma classe dedicada apenas para este conjunto.  

Assim, ao atualizar aquele valor, com certeza será em sua collection.

Seguindo o comportamento dessa regra, você deixa os comportamentos relacionados.

O grande objetivo dessa regra é aderir o SRP e *High Cohesion*.

## Exemplo 

### Antes

```php
<?php

foreach ($customers as $customer) {
    if ($customer->isGoldAccount()) {
        $customer->addBonus(new Money('R$ 50,00'));
    }
}
```

No exemplo acima, vamos adicionar um bônus aos clientes do tipo gold. A variável **$customers** é um array e por isso para modificar a coleção, precisamos iterá-la com um foreach e ainda internamente verificar se o tipo do cliente é gold.

Se usarmos uma classe que envolva essa coleção de customers, ou seja, uma *CustomerCollection*, por exemplo, e nessa classe existisse o método *filterGoldAccounts* para filtrar o tipo de cliente e o método *addBonus* para adicionar um bônus aos clientes, a usabilidade ficaria da seguitne forma:

### Depois

```php
<?php

$customersCollection = new CustomersCollection();

$goldCustomers = $customersCollection->filterGoldAccounts();

$goldCustomers->addBonus(new Money('R$ 50,00'));

$goldCustomers->save();
```
Assim, temos coleções que são específicas e inteligentes o suficiente para melhorar a usabilidade e evitar erros.

Vejamos um outro exemplo.

## Exemplo 2

### Antes

```php
<?php

foreach ($orders as $order) {
    if ($order->isPendent()) {
        $this->sendNotification($order);
    }
}
```

### Depois

```php
<?php

$ordersCollection = new OrdersCollection();

$ordersPendent = $ordersCollection->filterOrdersStatusPendent();

$ordersPendent->sendNotification();
```

[Regra 3](/manifest/roles/role-03.md) | [Regra 5](/manifest/roles/role-05.md)
