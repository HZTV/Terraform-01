# Домашнее задание к занятию «Введение в Terraform»

Пункт 1: ![Скриншот 30-01-2024 110521](https://github.com/HZTV/Terraform-01/assets/149588305/d0b260ef-d818-446c-b484-a38d60cc3195)

Задание 1

Пункт 2:
Секретные данные можно сохранить в файле personal.auto.tfvars

Пункт 3: ![image](https://github.com/HZTV/Terraform-01/assets/149588305/cfd5ac51-e373-42c4-b465-37c1ccd2fdb4)

Пункт 4:
Ошибка не указано локальное имя ресурса в "docker_image"
Неправильная обращение к локальному имени ресурса в {random_password.random_string_FAKE.resulT}"
Ошибка неправильное обращение к типу и имени локального ресурса в image = docker_image.nginx.image_id
Неправильно имя локального ресурса (начиналось с единицы) resource "docker_container" "1nginx"

Пункт 5: ![Скриншот 31-01-2024 104652](https://github.com/HZTV/Terraform-01/assets/149588305/9fe7842a-1bcc-4be0-8918-d42321e54686)

````
   resource "docker_image" "image_id" { 
   name = "nginx:latest" 
   keep_locally = true 
  
   resource "docker_container" "nginx" {
   image = docker_image.image_id.name
   name  = "exsample_${random_password.random_string.result}"
````
   
Пункт 6: ![Скриншот 31-01-2024 110821](https://github.com/HZTV/Terraform-01/assets/149588305/1107919d-7129-428b-9638-f6f8d36ebc5d)

````terraform apply  -auto-approve```` - опасен тем, что не требуется подтверждения (не надо писать yes в консоли). Коды сразу выполняется, и даже нет плана действий от терраформа. 
Т.е. при такой команде не будет показано сколько элементов инфраструктуры будет изменено или уничтожено.
Данный ключ ````-auto-approve```` может пригодится при автоматизации.

Пункт 7: ![Скриншот 31-01-2024 110919](https://github.com/HZTV/Terraform-01/assets/149588305/16c2151b-9922-4990-9201-8b02399d8122)

````
  "version": 4,
  "terraform_version": "1.5.6",
  "serial": 39,
  "lineage": "e470bc56-e3d3-2d4e-5415-ad681402d1a9",
  "outputs": {},
  "resources": [],
  "check_results": null
````
Пункт 8:
Образ контейнера не был удален т.к. при создании этого образа было указа параметр:
````keep_locally = true ````
Если выставить ````false````, то после ````terraform destroy```` image будет удален.

Из документации:  

````keep_locally(Boolean) Если true, образ Docker не будет удален при операции уничтожения. ````

````Если это значение ложно, оно удалит изображение из локального хранилища докера при операции уничтожения.````
