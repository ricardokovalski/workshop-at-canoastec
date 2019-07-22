## Envolva seus tipos primitivos

Tudo que for do tipo primitivo, ou seja, **int**, **float**, **boolean** e **string** deve ser encapsulado dentro do objeto. Seguindo este contexto, estaremos prevenindo o **Primitive Obsession**.

O **DDD - Domain-Drive Design** menciona está regra como **ValueObject** que nada mais é do que um objeto-valor pequeno no qual irá cuidar de um tipo específico de dado.

## Exemplo 1

### Antes

```php
<?php

class Order
{
    public function notifyBuyer($email)
    {
        if (filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
            throw new InvalidEmailException;
        }
        
        return $this->repository->sendEmail($email);
    }
}
```

### Depois

```php
<?php

class Email {

    public $email;
    
    public function __construct($email)
    {
        if (filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
            throw new InvalidEmailException;
        }
        
        return $this->email = $email;
    }
}

class Order
{
    public function notifyBuyer($email)
    {
        return $this->repository->sendEmail(new Email($email));
    }
}
```

> :warning: Um possível problema dessa abordagem é que ela adiciona complexidade à base de código. Na tradução do Object Calisthenics, é colocado que todos os tipos primitivos devem ser envolvidos em classes, porém, sabemos que no PHP isso pode se tornar improdutivo e desnecessário, portanto, analise o quanto aquela entrada ou tipo de dado pode sofrer mudanças, se precisa de validação, normalização, etc, só aplique-o se tiver uma real justificativa.

[Regra 2](/manifest/roles/role-02.md) | [Regra 4](/manifest/roles/role-04.md)