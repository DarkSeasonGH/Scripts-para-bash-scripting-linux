IROS A LA PARTE DE PREVIEW PARA VER EL CODIGO BIEN Y QUE NO SE VEA DESORDENADO


# Scripts-para-bash-scripting-linux
Hola gente aqui os dejo unos scripts mios sencillos de automatizacion de tareas en linux y lo basico de shell script
Los he hecho yo todos menos el de nmap automatizado
Es todo basico pero os puede servir para aprender shell scripting, es algo interesante en mi opinion





1
SCRIPT PARA ACTUALIZAR SISTEMA

#!/bin/bash

# Este es un script para actualizar los paquetes del sistema operativo

# TITULO
echo "Inicializando paquetes del sistema operativo..."
sleep 2
echo ""
sleep 2
echo ""

# ACTUALIZAR LISTA DE PAQUETES
echo "Actualizando lista de paquetes... [----0%----]"
sudo apt update
echo "Lista de los paquetes actualizada correctamente [----50%----]"
sleep 2
echo ""

# ACTUALIZAR PAQUETES  
echo "Actualizando los paquetes... [----50%----]"
sleep 2
sudo apt upgrade -y 
echo "Paquetes actualizados correctamente [----75%----]"
sleep 2
echo ""

# ELIMINAR PAQUETES INNECESARIOS
echo "Eliminando los paquetes innecesarios... [----75%----]"
sleep 2
sudo apt autoremove -y
echo "Paquetes eliminados correctamente [----100%----]"
sleep 2
echo ""

# DESPEDIDA
echo "Operación completada [----100%----]"
echo "Autor del script: Alejandro Doral"








2 
HACER BACKUP DE EL DIRECTORIO USER

#!/bin/bash

# Ruta de la carpeta a respaldar
ORIGEN="/home/kali"

# Ruta de la ubicación de respaldo
DESTINO="/home/backups"

# Crear una copia de seguridad con la fecha actual en el nombre
cp -r $ORIGEN $DESTINO

echo "Copia de seguridad creada en /home/backups"






3 
LO BASICO DE LOS BUCLES

#!/bin/bash

for i in 1 2 3 4; do
   echo "Esta es la iteracion $i"
done

for i in {1..5}; do
   echo "Esta es la iteracion $i"
done

for i in /home/kali/Documents/*; do
   echo "Aquí hay un fichero: $i"
done






4 
LO BASICO DE CASE

#!/bin/bash

echo "Elige una opción:"
echo "1. Saludar"
echo "2. Despedirse"
echo "3. Salir"

read opcion

case $opcion in
    1)
        echo "¡Hola!"
        ;;
    2)
        echo "Adiós."
        ;;
    3)
        echo "Saliendo del programa..."
        exit 0
        ;;
    *)
        echo "Opción no válida."
        ;;
esac





5
COMPRIMIR DOCUMENTS

#!/bin/bash

# Directorio a comprimir
DIRECTORIO="/home/kali/Documents"

# Archivo ZIP de salida
ARCHIVO_ZIP="respaldo_$(date +%Y%m%d).zip"

# Crear archivo ZIP
zip -r $ARCHIVO_ZIP $DIRECTORIO

echo "Archivos comprimidos en $ARCHIVO_ZIP."





6
ENVIAR UNA NOTIFICACION 

#!/bin/bash

#Este script es para mandar una notificacion de saludo a nosotros mismos en el escritorio"

echo "Parece que se esta generando una notificacion..."
echo ""

echo "Generando notificacion [----25%----]"
sleep 1
echo "Generando notificacion [----50%----]"
sleep 1
echo "Generando notificacion [----75%----]"
sleep 1
echo "Generando notificacion [----100%----]"
sleep 1

TITULO="Mensaje al escritorio"

MENSAJE="Hola esto esta siendo enviado con notify-send"

DESPEDIDA="En fin... chao querido user kali"

notify-send "$TITULO" "$MENSAJE" "$DESPEDIDA"
notify-send "Holaaaaaaaaaaaaaaaaaaaaaa" "Notificación de prueba"


echo ""
echo "Viste la notificacion arriba a la derecha?"
echo "tutor del script: Alejandro Doral"





7.LO BASICO DE IF

#!/bin/bash

variable1="cadenatexto"

#NORMAL
if [ $variable1 = "cadenatexto" ]; then
   echo "Aqui va el codigo que se ejecuta cuando la expresion es true"
else
   echo "Aqui va el codigo que se ejecuta cuando la expresion es falsa"
fi


#OR
if [ 4 -lt 10 ] || [ "texto" = "texto2" ]; then
   echo "Al menos una de las condiciones es verdadera"
else
   echo "Ninguna de las condiciones es verdadera"
fi


#AND
if [ 4 -lt 10 ] && [ "texto" = "texto2" ]; then
   echo "4 si que es menor que 10 pero texto y texto2 no son lo mismo"
else
   echo "no se"
fi


#EXIT
if [ "hola" = "hola" ]; then
   echo "Hola es igual a Hola"
   exit 0
else
   echo "Dio error"
   exit 1
fi





8
INFORMACION DE MEMORIA Y PROCESOS
#!/bin/bash

# Obtiene el espacio en disco
espacio_disco=$(df -h)

# Ejecuta htop en modo no interactivo
htop_informacion=$(htop -b -n 1)

# Obtiene los procesos en ejecución
procesos=$(ps)

echo "El espacio del disco duro es:"
echo "$espacio_disco"
echo ""

echo "La información que nos da htop es:"
echo "$htop_informacion"
echo ""

echo "Los procesos del sistema en ejecución son:"
echo "$procesos"
echo ""

echo "Autor del script: Alejandro Doral"





9
INFORMACION DEL USER

#!/bin/bash

quien_soy=$(whoami)

tiempo=$(uptime)

raiz_directorios=$(tree)

echo "El usuario actual es $quien_soy"

echo ""

echo "El tiempo usado en este sistema es $tiempo"

echo ""

echo "La raiz de directorios es $raiz_directorios"

echo ""

echo "Autor del script: Alejandro Doral"





10
LO BASICO DE READ

#!/bin/bash

echo "Introduce tres variables"

read var1
read var2
read var3

echo "Tu primera variable es $var1"
echo "Tu segunda variable es $var2"
echo "Tu tercera variable es $var3"





11
PARA AUTOMATIZAR NMAP

#!/bin/bash
     
    # Este programa parse los resultados de nmap y construye un documento html
     
    TITULO="Resultados nmap"
    FECHA_ACTUAL="$(date)"
    TIMESTAMP="Informe generado el $FECHA_ACTUAL por el usuario $USERNAME"
     
    nmap_exec () {
        echo "[INFO] Ejecutando nmap en la red $1, por favor espere unos segundos..."
        sudo nmap -sV $1 > $2
        echo "[OK] Fichero $2 generado correctamente"
        return 0
    }
     
    generar_html () {
    cat <<EOF
    <html>
        <head>
            <title>$TITULO</title>
       </head>
      <body>
        <h1>$TITULO</h1>
        <p1>$TIMESTAMP</p1>
      </body>
    </html>
     
    EOF
    }
     
    #Generamos el reporte raw con nmap
    nmap_exec "192.168.239.0/24" "salida_nmap.raw"
     
    # Generamos el reporte con los resultados de nmap en HTML
    echo "[INFO] Generando reporte html..."
    generar_html > resultados_nmap.html
    echo "[OK] Reporte resultados_nmap.html generado correctamente"





12
LO BASICO DE UNTIL

#!/bin/bash

var=4

until [ $var -lt 1 ]; do
   echo "El valor de la variable es: $var"
   var=$((var -1))
done






13
LO BASICO DE WHILE

#!/bin/bash

while true; do
   clear
   cat <<EOF

Por favor elige:
   1. A
   2. B
   3. Salir
EOF
   read -p "Introduce la opcion [1-3]: " opcion

   if [ "$opcion" = "3" ]; then
       echo "Saliendo del programa..."
       break
   elif [ "$opcion" = "1" ]; then
       echo "Has elegido la opción A"
       # Aquí va el código correspondiente para la opción A
   elif [ "$opcion" = "2" ]; then
       echo "Has elegido la opción B"
       # Aquí va el código correspondiente para la opción B
   else
       echo "Opción no válida. Introduce una opción válida [1-3]."
   fi

   read -p "Presiona Enter para continuar..."
done







Y esto es todo de momento
En un futuro alomejor subo mas shell scripts con linux, espero que sirva de algo
Chao
