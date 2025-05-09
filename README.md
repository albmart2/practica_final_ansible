# Práctica final Ansible
A continuación se explica un poco el desarrollo de la práctica final de Ansible
## Parte I
1. Creo el archivo ```inventory```, en el cual se definen los hosts gestionados por ansible.
2. Creo el archivo ```asnsible.cfg``` en el mismo directorio donde voy a ejecutar los playbooks. En este archivo, indicaré a Ansible que inventario utilizar por defecto.
3. Creo el archivo ```users.yml```. Este playbook se ejecutará sobre los hosts y creará los usuarios que le indicado.
4. Añado al proyecto el archivo ```verify_user.yml```
### Ejecutar los playbooks
1. Si carlos no existe, el modo --check (o modo de comprobación) mostrará que la tarea para carlos realizaría un cambio (lo crearía).

    ```bash
    ansible-playbook verify_user.yml --check
    ```
2. Para verificar la existencia sin crear, podrías usar el módulo command para ejecutar id <username> y comprobar el código de retorno, o usar el módulo ansible.builtin.getent si solo quieres verificar.
    ```bash
    ansible-playbook users.yml
    ```
    Después de esto, los usuarios carlos y marta deberían existir.
3. Ahora, ejecuta verify_users.yml --check (asumiendo que usa state: present):
    ```bash
    ansible-playbook verify_user.yml --check
    ```
    Si los usuarios fueron creados correctamente por users.yml, este comando no debería reportar errores ni cambios para las tareas de los usuarios, porque state: present es idempotente (no hace nada si el estado deseado ya se cumple). Si sigue reportando cambios, asegúrate de que users.yml se ejecutó sin errores.
## Parte II
1. Creo el playbook ```dev_deploy.yml``` en el que se realiza lo siguiente:
	- Instalar httpd
	- Iniciar y habilitar httpd
	- Desplegar template
	- Copiar index.html
	- Configurar firewall
2. Creo el playbook ```get_web_content.yml```.
3. Creo el playbook ```site.yml```, el cual importará los otros dos playbooks.
4. Ejecuto el playbook ```site.yml```.
	```bash
	ansible-playbook site.yml
	```
