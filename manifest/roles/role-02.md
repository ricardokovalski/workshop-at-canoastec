# regra 2: Não use o Else

Primeiro que não serve para nada. E segundo você não precisa e também nunca precisou.

Esta regra emprega o conceito **early return**, ou seja, retorne o seu valor o quanto antes.

Trabalhe sempre com o **return** ou **continue**, sabendo-se que ao cair em destes, o código abaixo não será executado, o que ajuda na remoção do else ao inverter ou até modificar a validação antes usada.

## Exemplo 1

### Antes

```php
<?php

protected function index()
{
    if ($this->security->isGranted('ADMIN')) {
        $view = 'admin.pages.index';
    } else {
        $view = 'home.pages.access_denied';
    }
    
    return view($view);
}
```

### Depois

```php
<?php

protected function index()
{
    if ($this->security->isGranted('ADMIN')) {
        return view('admin.pages.index');
    }
    
    return view('home.pages.access_denied');
}
```

## Exemplo 2

### Antes

```php
<?php

foreach ($members as $member) {
    if ($member->paid()) {
        $report[] = [$member->name => 'Paid'];
    } else {
        $report[] = [$member->name => 'Not Paid'];
    }
}
```

### Depois

```php
<?php

foreach ($members as $member) {
    if ($member->paid()) {
        $report[] = [$member->name => 'Paid'];
        continue;
    }
    $report[] = [$member->name => 'Not Paid'];
}
```

[Regra 1](/manifest/roles/role-01.md) | [Regra 3](/manifest/roles/role-03.md)