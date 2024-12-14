# Домашнее задание к занятию 6 «Создание собственных модулей»

## Подготовка к выполнению

1. Создайте пустой публичный репозиторий в своём любом проекте: `my_own_collection`.
2. Скачайте репозиторий Ansible: `git clone https://github.com/ansible/ansible.git` по любому, удобному вам пути.
3. Зайдите в директорию Ansible: `cd ansible`.
4. Создайте виртуальное окружение: `python3 -m venv venv`.
5. Активируйте виртуальное окружение: `. venv/bin/activate`. Дальнейшие действия производятся только в виртуальном окружении.
6. Установите зависимости `pip install -r requirements.txt`.
7. Запустите настройку окружения `. hacking/env-setup`.
8. Если все шаги прошли успешно — выйдите из виртуального окружения `deactivate`.
9. Ваше окружение настроено. Чтобы запустить его, нужно находиться в директории `ansible` и выполнить конструкцию `. venv/bin/activate && . hacking/env-setup`.

## Основная часть

Ваша цель — написать собственный module, который вы можете использовать в своей role через playbook. Всё это должно быть собрано в виде collection и отправлено в ваш репозиторий.

**Шаг 1.** В виртуальном окружении создайте новый `my_own_module.py` файл.

**Шаг 2.** Наполните его содержимым:

**Шаг 3.** Заполните файл в соответствии с требованиями Ansible так, чтобы он выполнял основную задачу: module должен создавать текстовый файл на удалённом хосте по пути, определённом в параметре `path`, с содержимым, определённым в параметре `content`.

**Шаг 4.** Проверьте module на исполняемость локально.

**Шаг 5.** Напишите single task playbook и используйте module в нём.

**Шаг 6.** Проверьте через playbook на идемпотентность.

**Шаг 7.** Выйдите из виртуального окружения.

**Шаг 8.** Инициализируйте новую collection: `ansible-galaxy collection init my_own_namespace.yandex_cloud_elk`.

**Шаг 9.** В эту collection перенесите свой module в соответствующую директорию.

**Шаг 10.** Single task playbook преобразуйте в single task role и перенесите в collection. У role должны быть default всех параметров module.

**Шаг 11.** Создайте playbook для использования этой role.

**Шаг 12.** Заполните всю документацию по collection, выложите в свой репозиторий, поставьте тег `1.0.0` на этот коммит.

**Шаг 13.** Создайте .tar.gz этой collection: `ansible-galaxy collection build` в корневой директории collection.

**Шаг 14.** Создайте ещё одну директорию любого наименования, перенесите туда single task playbook и архив c collection.

**Шаг 15.** Установите collection из локального архива: `ansible-galaxy collection install <archivename>.tar.gz`.

**Шаг 16.** Запустите playbook, убедитесь, что он работает.

**Шаг 17.** В ответ необходимо прислать ссылки на collection и tar.gz архив, а также скриншоты выполнения пунктов 4, 6, 15 и 16.


## Решение


1. создал my_own_module.py
2. наполнил содержимым
3. используя лекцию изменил для соответсвия задаче
4. проверил модуль локально ( для проверки используем значения из файла для тестирования test_my_own_module.json )  
	python3 -m my_own_module test_my_own_module.json  
	![результат](/images/4.png)
5. добавил single task playbook c названием test_playbook.yml и содержимым :  
---
- name: Module testing  
  hosts: localhost  
  tasks:  

  - name: Test module ( creating ffile with text)  
    my_own_module:  
      path: './test.txt'  
      content: "Hello world!"  
---
6. запустил дважды  
	![результат](/images/4.png)
7. вышел используя deactivate
8.  создал новую коллекцию   
	ansible-galaxy collection init my_own_namespace.yandex_cloud_elk  
9. положилмодуль в соответсвующую папку plugins\modules
10. переделал задачу в роль
11. создал плейбук
12. выложил коллекцию в гит   
	[результат](https://github.com/barmaq/my_own_collection/tree/main)
13. создаль локальный архив из коллекции   
	ansible-galaxy collection build
14. создал директорию и перенс туда плейбук и архив коллекции
15. установил коллекцию 
	ansible-galaxy collection install -p ansible_collections /home/barmaq/ansible/test/my_own_collection/my_own_namespace/yandex_cloud_elk/my_own_namespace-yandex_cloud_elk-1.0.0.tar.gz  
	![результат](/images/15.png)
16. запустил  
	![результат](/images/16.png)
17. [коллекция](https://github.com/barmaq/my_own_collection/tree/main)
	[tar.gz](https://github.com/barmaq/my_own_collection/tree/main)	
