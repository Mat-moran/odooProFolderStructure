# odooProFolderStructure
Estructura de carpetas en proyecto de odoo


# Puesta a punto de un usuario de proyecto odoo para la utilización del programa de gestión
(Se parte de la base de que los pasos previos, (configuración del sistema, instalación de python, git, postgresql, etc...) se han seguido correctamente en el siguiente enlace y que se ha podido iniciar una base de datos sin problemas.

- https://subscription.packtpub.com/book/business_and_other/9781789618921/3/ch03lvl1sec28/installing-odoo-for-production-use
[odoo 12 development cookbook]

# pasos que se han seguido para esta instalación en particular

- Descargar la estructura de carpetas para un odoo de producción: https://github.com/Mat-moran/odooProFolderStructure

- Clonar la versión más reciente de odoo community de: https://github.com/odoo/odoo.git

- Create virtualenv and install the dependencies:
 `virtualenv -p python3 ~/{ruta_carpeta_proyecto}/env/env-odoo-13.0` 
 `source ~/{ruta_carpeta_proyecto}/env/env-odoo-13.0/bin/activate` 
 `pip3 install -r src/odoo/requirements.txt`

- Correccion del archivo "/bin/start-odoo" con los datos actualizados al proyecto actual.

NOTA: a partir de aquí se recomienda desinstalar gcc para que en caso de ataque no se pueda compilar código. (En esta instalación no lo he realizado de momento, {fecha_instalación})


- Como no estaba creado el rol con el nombre del usuario ubrimaq
 "sudo -u postgres createuser -s $USER"

- list_db = True (para activar el database manager)
- Generar clave de admin con pwgen (por ejemplo) `pwgen -s 22`



# COMANDOS UTILES

- \dt ir_translation
- \d ir_translation 
- SELECT id,name,res_id,lang,type,value FROM ir_translation WHERE ir_translation.value = 'Example of a product 2';


# NOTAS

## BackUps

- Hay que quitar la línea "pg_path =  /usr/lib/postgresql/10/bin/postgres" para poder hacer copias de seguridad (solucionado gracias a:https://www.odoo.com/es_ES/forum/ayuda-1/question/command-pg-dump-not-found-87849)

- Los backUps se realizan de forma automática ejecutando un script con CRON. el script está en la carpeta raiz "/" y el archivo CRON se encuentra en "/var/spool/cron/crontabs/{nombre_bd}"

- Cuando se hacen los backUps si no se hacen con la opción de filestores incluida no se guardan las imágenes. Esto es debido a que odoo no guarda los archivos en la base de datos. Los guarda en el filestore. Lo único que hay que hacer es hacer el backup como ".zip" en vez de como ".dump".

- Existen dos tipos de backups físicos y lógicos
(Logical vs. Physical (Basic difference):
Logical backup is using SQL statements. Export using exp tool is logical.
Physical backup is copying the data files either when the database is up and running (HOT BACKUP) or when the database is shutdown (COLD BACKUP))
