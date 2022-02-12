## INSTALACION GITLAB UBUNTU

Instalamos actualizaciones y dependencia.

     sudo apt-get update
    sudo apt-get install -y curl openssh-server ca-certificates tzdata perl

En caso de querer configurar envio de mails podemos instalar POSTFIX, este paso se puede omitir.

    sudo apt-get install -y postfix


Agregamos el repositorio de gitlab CE e instalamos (si queremos la version EE solo debemos cambiar gitlab-ce por gitlab-ee en la url)

    curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash sudo


Suponiendo que nuestra ip es 192.168.0.247 , editamos nuestra lista de host (vi /etc/hosts) y ponemos :

    192.168.0.247 gitlab.local.com

 Guardamos los cambios

En el siguiente paso vamos a realizar la instalacion pasandole como variable la url que tendra nuestro gitlab

sudo EXTERNAL_URL=gitlab.local.com apt-get install gitlab-ce

> Podemos poner gitlab-ce  o gitlab-ee , la diferencia es que la CE es COMUNITY EDITION y la EE es ENTERPRISE EDITION, en este ultima luego del periodo de prueba vamos a neceistar realizar un pago mensual / anual para mantener la suscripcion. En nuestro caso vamos a tener instalada la version CE.
> 
> En la documentacion oficial pasan como parametro EXTERNAL_URL= https://.... como yo lo configure en modo http no hace falta poner http:// ya que en el archivo de configuracion /etc/gitlab/gitlab.rb por defecto ese parametro viene con "http://" , es decir que si nosotros le volvemos a pasar ese parametro al momento de instalarlo, lo agrega una segunda vez y el instalador falla.

Luego de unos minutos ( dependiendo del equipo donde lo estemos instalando) nos tiene que aparecer el siguiente mensaje.
![Instalacion finalizada](https://raw.githubusercontent.com/fncambres/gitlab-install/main/gitfinish.png)

Tal como dice en la imagen en 24 hs con la primer reconfiguracion el archivo temporal con la clave se limpiara.
Hacemos un cat para obtener la clave temporal

    cat /etc/gitlab/initial_root_password

Esto nos devuelve algo asi como 

    Password: 3H1EKtI6Mz55Mii7BNu1G2LYGKUii9QsciVugFx-rYM=


Accedemos via browser a nuestra url de gitlab, en mi caso http://gitlab.local.com y nos deberia aparecer la siguiente pantall, nos logueamos como root y la clave provisoria.

![enter image description here](https://raw.githubusercontent.com/fncambres/gitlab-install/main/inicialpassword.png)

Una vez que ingresamos  podemos ir a Menu --> Admin --> Overview --> Users y seleccionamos el unico usuario que esta creado que deberia ser "Administrator" , editamos su perfil y donde dice "Password" la cambiamos y salvamos los cambios, la sesion se cerrar automaticamente y debemos poner las nuevas credenciales y con esto ya tenemos nuestra instancia de gitlab levantada.


