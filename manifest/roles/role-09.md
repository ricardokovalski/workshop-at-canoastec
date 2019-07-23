# Regra 9 - Não use Getters ou Setters

Pode parecer uma regra bem estranha em um prmeiro momento, mas a ideia é bem básica. Retiramos os getters e setters para poder adicionar decisões no próprio objeto. Qualquer decisão baseada inteiramente no estado de um objeto deve ser feita diretamente nele.

São muitos os benefícios quando se é aplicada essa regra. Se Reduz a duplicidade de regras e melhora a compreensão do objeto.

Também enriquecemos nosso objeto com lógica e métodos mais valiosos e significativos, não apenas o usando como uma classe com apenas dados.

## Exemplo 1

### Antes

```php
<?php
class Buyer
{
    protected $name;
    protected $purchases;
    
    public function getName() {/**/}
    public function setName($name) {/**/}
    
    public function getPurchases() {/**/}
    public function setPurchases($purchases) {/**/}
}
```

### Depois

```php
<?php
class Buyer
{    
    protected $name;    
    protected $purchases;
    
    public function addNewPurchase()
    {
        $this->purchases++;
    }
}
```

## Exemplo 2

### Antes

```php
<?php
class Account
{
    protected $balance;
    
    public function getBalance() {/**/}
    public function setBalance($balance) {/**/}
}
```

### Depois

```php
<?php
class Account
{
    protected $balance;
    
    public function addBalance($balance)
    {
        $this->balance += $balance;
    }
    
    public function debit($debit)
    {
        $this->balance -= $debit;
    }
}
```
[Regra 8](/manifest/roles/role-08.md) | [Object Calisthenics](/manifest/slide-05.md#as-regras)