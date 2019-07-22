## Regra 1: Apenas um nível de identação por método

Cada método deve realizar uma única ação. Deste modo, estaremos facilitando a leitura e a manutenção do código, promovendo o SRP e evitando o efeito Hadouken.

Gantanta um único nível de identação extraindo os comportamentos para outros métodos. Usando essa abordagem, estamos aplicando o **Extract Method Pattern**.

## Exemplo 1

### Antes

```php
<?php

public function show($slug)
{
    $lesson = $this->repository->findBySlug($slug);
    
    if ($lesson) {
        if (!empty($lesson->thumb_url)) {
            $this->seo()->addImages($lesson->thumb_url);
        }
        
        if ($lesson->track) {
            $this->seo()->setTitle($lesson->title.' ['.$lesson->track->title.']');
        } else {
            $this->seo()->setTitle($lesson->title);
        }
        
        $this->seo()->setDescription($lesson->description);
        
        return $this->view('lessons::show')->with(compact('lesson'));
    }
    
    return redirect(route('lesson.index'));
}
```

### Depois

```php
<?php

public function show($slug)
{
    $lesson = $this->repository->findBySlug($slug);
    
    if ($lesson) {
        $this->addThumbToImages($lesson->thumb_url);
        $trackTitle = ! $lesson->track ? '' : '['.$lesson->track->title.']';
        $this->seo()->setTitle($lesson->title . $trackTitle);
        $this->seo()->setDescription($lesson->description);
        return $this->view('lessons::show')->with(compact('lesson'));
    }
    
    return redirect(route('lesson.index'));
}

protected function addThumbToImages($thumbURL)
{
    if (empty($thumbURL)) {
        return false;
    }
    
    return $this->seo()->addImages($thumbURL);
}
```

[Object Calisthenics](/manifest/slide-05.md#object-calisthenics) | [Regra 2](/manifest/roles/role-02.md)