# Домашнее задание к занятию «Введение в Terraform» - Тертерян Вячеслав

---

### Задание 1

1. Ответ на пункт два, если все верно понял то в тех что удовлетворяют данному правилу:
```
# .tfstate files
.terraform*
```  

2. Вот секретное содержимое:
```
 "result": "bc9Oo8nTPDTlfI7p",
```  

3. Ошибки залючались в наличии тайтла и соблюдение правил присвоение имен. Вот исправленный:
```
resource "docker_image" "nginx"{
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 8000
  }
}
```  
![alt text](https://github.com/Marsianec/homework18-1/blob/main/img/1.png)  

4. Опсаность применения ключа auto-approve в том, что изменения применятся сразу и если кто-то внес изменения в код, которые вы не увидели, они могут сломать всю систему. Мне кажется что ее применение имеет место быть только в случае если мы уверены в версии и правильности кода (в идиале работает и имеет доступ к коду только 1 человек) и перед этим были проведены тестирования кода в изолированной среде.  
![alt text](https://github.com/Marsianec/homework18-1/blob/main/img/2.png)  

5. Вот что будет после удаления:
```
{
  "version": 4,
  "terraform_version": "1.5.7",
  "serial": 11,
  "lineage": "fd2d326c-b1cd-e073-e6a2-f75ce14a2eb8",
  "outputs": {},
  "resources": [],
  "check_results": null
}
```  

6. Если я правильно понимаю, то не удален он будет так как по умолчанию как при триггере он остается чтоб при необходимости развертывания инфраструктуры при смене кода. Вот строчка из документации:
"A map of arbitrary strings that, when changed, will force the docker_image resource to be replaced. This can be used to rebuild an image when contents of source code folders change"  