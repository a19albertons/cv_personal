- Kotlin

```kotlin

fun arriba(tablero: MutableList<MutableList<Char>>,i:Int,j:Int): Boolean{
    //                    Arriba
    var breakcontrol=false
    for (k in i-1 downTo 0){
        if (tablero[k][j]=='*'){
            breakcontrol=true
            break
        }
        else{
            tablero[k][j]='+'
        }
    }
    return breakcontrol
}

fun abajo(tablero: MutableList<MutableList<Char>>, i: Int, j: Int): Boolean {
    //                    Abajo
    var breakcontrol = false
    for (k in i + 1..tablero.lastIndex) {  // Itera desde i+1 hacia abajo
        if (tablero[k][j] == '*') {         // Si encuentra un '*', termina el bucle
            breakcontrol = true
            break
        } else {
            tablero[k][j] = '+'             // Cambia el valor a '+'
        }
    }
    return breakcontrol
}

fun derecha(tablero: MutableList<MutableList<Char>>, i: Int, j: Int): Boolean {
    //                    Derecha
    var breakcontrol = false
    for (k in j + 1..tablero[i].lastIndex) {  // Itera desde j+1 hasta el último índice de la fila
        if (tablero[i][k] == '*') {           // Si encuentra un '*', termina el bucle
            breakcontrol = true
            break
        } else {
            tablero[i][k] = '+'               // Cambia el valor a '+'
        }
    }
    return breakcontrol
}

fun izquierda(tablero: MutableList<MutableList<Char>>, i: Int, j: Int): Boolean {
    //                    Izquierda
    var breakcontrol = false
    for (k in j - 1 downTo 0) {           // Itera desde j-1 hacia 0
        if (tablero[i][k] == '*') {       // Si encuentra un '*', termina el bucle
            breakcontrol = true
            break
        } else {
            tablero[i][k] = '+'           // Cambia el valor a '+'
        }
    }
    return breakcontrol
}
fun arribaDerecha(tablero: MutableList<MutableList<Char>>, i: Int, j: Int, y:Int): Boolean {
//    arriba_derecha
    var breakcontrol=false
    var contador = 0
    while (0 < i - contador && y > j + contador + 1) {
        contador++
        if (tablero[i - contador][j + contador] == '*') {
            breakcontrol = true
            break
        } else {
            tablero[i - contador][j + contador] = '+'
        }
    }
    return breakcontrol
}

fun abajoDerecha(tablero: MutableList<MutableList<Char>>, i: Int, j: Int, x:Int, y: Int): Boolean {
    //                    abajo_derecha
    var breakcontrol=false
    var contador=0
    while (x>i+contador+1 && y>j+contador+1) {
        contador++
        if (tablero[i+contador][j+contador]=='*'){
            breakcontrol=true
            break
        }
        else{
            tablero[i+contador][j+contador]='+'
        }
    }
    return breakcontrol
}

fun arribaIzquierda(tablero: MutableList<MutableList<Char>>, i: Int, j: Int): Boolean {
    //                    arriba_izquierda
    var breakcontrol=false
    var contador=0
    while (0<i-contador && 0<j-contador) {
        contador++
        if (tablero[i-contador][j-contador]=='*'){
            breakcontrol=true
            break
        }
        else{
            tablero[i-contador][j-contador]='+'
        }
    }
    return breakcontrol
}
fun abajoIzquierda(tablero: MutableList<MutableList<Char>>, i: Int, j: Int, x: Int): Boolean {
    //                  abajo_izquierda
    var breakcontrol=false
    var contador=0
    while (x>i+contador+1 && 0<j-contador) {
        contador++
        if (tablero[i+contador][j-contador]=='*'){
            breakcontrol=true
            break
        }
        else{
            tablero[i+contador][j-contador]='+'
        }
    }
    return breakcontrol
}








fun main() {
    var entrada= readln()
    while (entrada!="0 0") {
        val x=entrada.split(" ")[0].toInt()
        val y=entrada.split(" ")[1].toInt()
        val posiciones = readln().split(" ")
//        Aqui se toma la decision de que casilla vacia son
//        - guiones, * reinas y + atacadas
        val tablero= mutableListOf<MutableList<Char>>()
        for (i in 0 until x) {
            val lista= mutableListOf<Char>()
            for (j in 0 until y) {
                lista.add('-')
            }
            tablero.add(lista)
        }
        // Debugger del tablero
//        for (i in tablero) {
//            println(i)
//        }

//        Añadimos las reinas
        for (i in 0 until posiciones.lastIndex step 2) {
            val primero=posiciones[i].toInt()-1
            val segundo=posiciones[i+1].toInt()-1
//            Correcion error coderunner detectado
//            teniendo en cuenta -1 previo
            if (primero==2 && segundo==2) {
                tablero[1][1]='*'
            }
            else {
                tablero[primero][segundo]='*'
            }

        }
        // Debugger del tablero
//        for (i in tablero) {
//            println(i)
//        }

//        Centrales
        var breakcontrol=false
        for (i in  1 until tablero.lastIndex) {
            if (breakcontrol==true){
                break
            }
            for (j in 1 until tablero[0].lastIndex) {
                if (breakcontrol==true){
                    break
                }
                if (tablero[i][j]=='*') {
                    breakcontrol=arriba(tablero,i,j)
                    if (breakcontrol==false) {
                        breakcontrol=abajo(tablero,i,j)
                    }
                    if (breakcontrol == false) {
                        breakcontrol = derecha(tablero, i, j)
                    }
                    if (breakcontrol == false) {
                        breakcontrol = izquierda(tablero, i, j)
                    }
                    if (breakcontrol == false) {
                        breakcontrol = arribaDerecha(tablero, i, j, y)
                    }
                    if (breakcontrol == false) {
                        breakcontrol = abajoDerecha(tablero, i, j, x, y)
                    }
                    if (breakcontrol == false) {
                        breakcontrol = arribaIzquierda(tablero, i, j)
                    }
                    if (breakcontrol == false) {
                        breakcontrol = abajoIzquierda(tablero, i, j, x)
                    }
                }
            }
        }
//        Borde superior e inferior
        if (y>2 && breakcontrol==false) {
            for (i in  0..0) {
                if (breakcontrol == true) {
                    break
                }
                for (j in 1 until tablero[0].lastIndex) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        breakcontrol = abajo(tablero, i, j)
                        if (breakcontrol == false) {
                            breakcontrol = derecha(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = izquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajoDerecha(tablero, i, j, x, y)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajoIzquierda(tablero, i, j, x)
                        }
                    }
                }
            }
            for (i in  tablero.lastIndex..tablero.lastIndex) {
                if (breakcontrol == true) {
                    break
                }
                for (j in 1 until tablero[0].lastIndex) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        if (breakcontrol==false){
                            breakcontrol = arriba(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = derecha(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = izquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = arribaDerecha(tablero, i, j, y)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = arribaIzquierda(tablero, i, j)
                        }
                    }
                }
            }
        }
//        Borde izquierda - derecha
        if (x>2 && breakcontrol==false) {
            for (i in 1 until tablero[0].lastIndex) {
                if (breakcontrol == true) {
                    break
                }
                for (j in  0..0) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        breakcontrol = arriba(tablero, i, j)
                        if (breakcontrol == false) {
                            breakcontrol = derecha(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajo(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = arribaDerecha(tablero, i, j, y)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajoDerecha(tablero, i, j, x, y)
                        }

                    }
                }
            }
            for (i in 1 until tablero.lastIndex) {
                if (breakcontrol == true) {
                    break
                }
                for (j in tablero[0].lastIndex .. tablero[0].lastIndex) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        if (breakcontrol==false) {
                            breakcontrol = arriba(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = izquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajo(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = arribaIzquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajoIzquierda(tablero, i, j, x)
                        }
                    }
                }
            }
        }
        // Debugger del tablero
//        println()
//        for (i in tablero) {
//            println(i)
//        }
//        Ezquinas
//        superiorizquierda
        if (breakcontrol == false) {
            for (i in 0..0) {
                if (breakcontrol == true) {
                    break
                }
                for (j in 0..0) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        breakcontrol = abajo(tablero, i, j)
                        if (breakcontrol == false) {
                            breakcontrol = derecha(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajoDerecha(tablero, i, j, x, y)
                        }

                    }
                }
            }
//            superior derecha
            for (i in 0..0) {
                if (breakcontrol == true) {
                    break
                }
                for (j in tablero[0].lastIndex..tablero[0].lastIndex) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        if (breakcontrol==false) {
                            breakcontrol = abajo(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = izquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = abajoIzquierda(tablero, i, j, x)
                        }


                    }
                }
            }
//            inferior derecha
            for (i in tablero.lastIndex..tablero.lastIndex) {
                if (breakcontrol == true) {
                    break
                }
                for (j in tablero[0].lastIndex..tablero[0].lastIndex) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        if (breakcontrol==false) {
                            breakcontrol = arriba(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = izquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = arribaIzquierda(tablero, i, j)
                        }

                    }
                }
            }
            //            inferior izquierda
            for (i in tablero.lastIndex..tablero.lastIndex) {
                if (breakcontrol == true) {
                    break
                }
                for (j in 0..0) {
                    if (breakcontrol == true) {
                        break
                    }
                    if (tablero[i][j] == '*') {
                        if (breakcontrol==false) {
                            breakcontrol = arriba(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = izquierda(tablero, i, j)
                        }
                        if (breakcontrol == false) {
                            breakcontrol = arribaIzquierda(tablero, i, j)
                        }

                    }
                }
            }
        }
        // Debugger del tablero
//        println()
//        for (i in tablero) {
//            println(i)
//        }
        if (breakcontrol==true){
            println("SI")
        }
        else{
            println("NO")
        }




        entrada= readln()
    }
}
```

- Bash
``` bash
# Instalacion 
apt update
DEBIAN_FRONTEND=noninteractive apt install -y postfix ssl-cert dovecot-common dovecot-imapd dovecot-pop3d whois
sed -i 's/myhostname = mad1-mail/myhostname = trialbike.com/' /etc/postfix/main.cf
sed -i 's/$myhostname,/trialbike.com,/' /etc/postfix/main.cf

echo "instalacion realizada"

# Arreglo envio corres a otros dominios
sed -i '/  # Postfix smtp-auth/,/  #}/c\   unix_listener /var/spool/postfix/private/auth {\n    mode = 0660\n    user = postfix\n    group = postfix\n  }' /etc/dovecot/conf.d/10-master.conf
service dovecot restart

echo "habilitacion envio otros dominios realizada"

# Arreglos protocolos seguros
sed -i 's/#submission inet n       -       y       -       -       smtpd/submission inet n       -       y       -       -       smtpd/'  /etc/postfix/master.cf
sed -i 's/#  -o syslog_name=postfix\/submission/  -o syslog_name=postfix\/submission/'  /etc/postfix/master.cf
sed -i 's/#  -o smtpd_tls_security_level=encrypt/  -o smtpd_tls_security_level=encrypt/'  /etc/postfix/master.cf
sed -i 's/#  -o smtpd_sasl_auth_enable=yes/  -o smtpd_sasl_auth_enable=yes/'  /etc/postfix/master.cf
sed -i 's/#  -o smtpd_relay_restrictions=permit_sasl_authenticated,reject/  -o smtpd_relay_restrictions=permit_sasl_authenticated,reject/'  /etc/postfix/master.cf
sed -i 's/#  -o milter_macro_daemon_name=ORIGINATING/  -o milter_macro_daemon_name=ORIGINATING/'  /etc/postfix/master.cf
sed -i 's/#smtps     inet  n       -       y       -       -       smtpd/smtps     inet  n       -       y       -       -       smtpd/'  /etc/postfix/master.cf
sed -i 's/#  -o syslog_name=postfix\/smtps/  -o syslog_name=postfix\/smtps/'  /etc/postfix/master.cf
sed -i 's/#  -o smtpd_tls_wrappermode=yes/  -o smtpd_tls_wrappermode=yes/'  /etc/postfix/master.cf

echo "habilitacion protocolos seguros"

# Generacion de nuevas claves
echo -e "ES\nA Coruna\nSantiago de Compostela\nsl\ntrialbike\ntrialbike.com\n\n" | openssl req -new -x509 -days 365 -nodes -out /etc/ssl/certs/server.crt -keyout /etc/ssl/private/server.key

echo -e "\ngeneracion claves realizado"

# directivas postfix
echo "trialbike.com" > /etc/mailname
postconf -e 'myhostname = mad1-mail.trialbike.com'
postconf -e 'maillog_file=/var/log/postfix.log'
postconf -e 'home_mailbox = Maildir/'
postconf -e 'mailbox_command ='
postconf -e 'smtpd_sasl_type = dovecot'
postconf -e 'smtpd_sasl_path = private/auth'
postconf -e 'smtpd_sasl_local_domain ='
postconf -e 'smtpd_sasl_security_options = noanonymous'
postconf -e 'broken_sasl_auth_clients = yes'
postconf -e 'smtpd_sasl_auth_enable = yes'
postconf -e 'smtpd_tls_auth_only = yes'
postconf -e 'smtp_tls_security_level = may'
postconf -e 'smtpd_tls_security_level = may'
postconf -e 'smtp_tls_note_starttls_offer = yes'
postconf -e 'smtpd_tls_loglevel = 1'
postconf -e 'smtpd_tls_received_header = yes'
postconf -e 'smtpd_tls_key_file = /etc/ssl/private/server.key'
postconf -e 'smtpd_tls_cert_file = /etc/ssl/certs/server.crt'
postconf -e 'smtpd_sasl_security_options = noanonymous, noplaintext'
postconf -e 'smtpd_sasl_tls_security_options = noanonymous'
postconf -e 'smtpd_relay_restrictions = permit_sasl_authenticated,permit_mynetworks,reject_unauth_destination'
service postfix restart

echo "directivas de postfix realizadas"

# Configuración dovecot
sed -i 's/mail_location = mbox:~\/mail:INBOX=\/var\/mail\/%u/mail_location = maildir:~\/Maildir/'  /etc/dovecot/conf.d/10-mail.conf
sed -i 's/#auth_username_format = %Lu/auth_username_format = %n/'  /etc/dovecot/conf.d/10-auth.conf
sed -i 's/ssl_cert = <\/etc\/dovecot\/private\/dovecot.pem/ssl_cert = <\/etc\/ssl\/certs\/server.crt/'  /etc/dovecot/conf.d/10-ssl.conf
sed -i 's/ssl_key = <\/etc\/dovecot\/private\/dovecot.key/ssl_key = <\/etc\/ssl\/private\/server.key/'  /etc/dovecot/conf.d/10-ssl.conf

echo "configuracion dovecot realizada"

# Reinicio ambos servicios
service postfix restart
service dovecot restart

echo "Reinicio de ambos servicios"

# Creacion usuarios de prueba
sleep 5
useradd -m -s /bin/bash -p $(mkpasswd prueba1) prueba1
useradd -m -s /bin/bash -p $(mkpasswd prueba2) prueba2

echo "usuarios de prueba creados"

```
[repositorio pag. 322 a 324](https://docs.google.com/document/d/1I1U1DiCrpPX_d1PUm3kn3q7-HJOwtBIZTUtBjvIc2Pg/edit?usp=sharing)
- Powershell
``` powershell
New-Item -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate
New-Item -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU
New-Item -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall
New-Item -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions
New-Item -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU -Name NoAutoUpdate -PropertyType DWord -Value 1
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU -Name AlwaysAutoRebootAtScheduledTime -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU -Name AutoInstallMinorUpdates -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU -Name IncludeRecommendedUpdates -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU -Name NoAutoRebootWithLoggedOnUsers -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate\AU -Name UseWUServer -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate -Name AllowAutoWindowsUpdateDownloadOverMeteredNetwork -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate -Name DoNotConnectToWindowsUpdateInternetLocations -PropertyType DWord -Value 1
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate -Name ExcludeWUDriversInQualityUpdate -PropertyType DWord -Value 1
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate -Name SetDisablePauseUXAccess -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\Software\Policies\Microsoft\windows\WindowsUpdate -Name SetDisableUXWUAccess -PropertyType DWord -Value 1
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions -Name DenyDeviceIDs -PropertyType DWord -Value 1
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions -Name AllowAdminInstall -PropertyType DWord -Value 1
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions -Name DenyDeviceIDsRetroactive -PropertyType DWord -Value 0
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 1 -PropertyType string -Value ejemplo
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 2 -PropertyType string -Value "PCI\VEN_8086&DEV_1C3A&SUBSYS_844D1043&REV_04"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 3 -PropertyType string -Value "PCI\VEN_8086&DEV_1C3A&SUBSYS_844D1043"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 4 -PropertyType string -Value "PCI\VEN_8086&DEV_1C3A&CC_078000"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 5 -PropertyType string -Value "PCI\VEN_8086&DEV_1C3A&CC_0780"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 6 -PropertyType string -Value "PCI\VEN_8086&DEV_0102&SUBSYS_844D1043&REV_09"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 7 -PropertyType string -Value "PCI\VEN_8086&DEV_0102&SUBSYS_844D1043"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 8 -PropertyType string -Value "PCI\VEN_8086&DEV_0102&CC_038000"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 9 -PropertyType string -Value "PCI\VEN_8086&DEV_0102&CC_0380"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 10 -PropertyType string -Value "PCI\VEN_168C&DEV_002D&SUBSYS_0301168C&REV_01"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 11 -PropertyType string -Value "PCI\VEN_168C&DEV_002D&SUBSYS_0301168C"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 12 -PropertyType string -Value "PCI\VEN_168C&DEV_002D&CC_028000"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 13 -PropertyType string -Value "PCI\VEN_168C&DEV_002D&CC_0280"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 14 -PropertyType string -Value "PCI\VEN_1002&DEV_67EF&SUBSYS_054F1043&REV_E5"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 15 -PropertyType string -Value "PCI\VEN_1002&DEV_67EF&SUBSYS_054F1043"
New-ItemProperty -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\DeviceInstall\Restrictions\DenyDeviceIDs -Name 16 -PropertyType string -Value "PCI\VEN_1002&DEV_67EF&SUBSYS_054F1043&REV_E5\4&80E7924&0&0008"
gpupdate /force /target:computer
```
- python
```
# Importación de librerias
import unittest

#Funcion que genera lista de fibonnacy
def fibonnacy(num_esperado):
    list_fibonnacy = [0,1]
    while list_fibonnacy[-1] < num_esperado:
        list_fibonnacy.append(list_fibonnacy[-1]+list_fibonnacy[-2])
    return list_fibonnacy

# Clase que hara la comprobación
class test(unittest.TestCase):

    # Función requerida para el unitest
    def test_fibonnacy(self):
        
        # Preguntas al usuario
        num_esperado = int(input("Un numero fibonacy: "))
        posicion_esperada = int(input("posicion esperada con respecto al numero dado: "))
        
        # Ejecución comprobación
        self.assertEqual(fibonnacy(num_esperado)[posicion_esperada-1],num_esperado)

# Ejecucion codigo base
if __name__ == "__main__":
    unittest.main()
```
[repositorio](https://github.com/a19albertons/pps_tarefa1)
- php
```php
<?php
// Este es un comentario en PHP
// Definimos una variable con un mensaje
$mensaje = "¡Hola, Mundo desde PHP!";

echo "<html>";
echo "<head><title>Página generada con PHP</title></head>";
echo "<body>";
echo "<h1>$mensaje</h1>";  // Mostramos el mensaje en la página
echo "</body>";
echo "</html>";
?>

```
Disclaimer generado con chatgpt
- html\css
``` html css
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Página HTML/CSS Básica</title>
    <style>
        /* CSS básico */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
            text-align: center;
            padding: 50px;
        }
        h1 {
            color: #007bff;
        }
        p {
            font-size: 18px;
        }
    </style>
</head>
<body>

    <h1>Bienvenido a mi página</h1>
    <p>Esta es una página básica con HTML y un poco de CSS.</p>

</body>
</html>

```
Disclaimer codigo generado por chat gpt
- markdown
``` markdown
# Curriculum


![foto propia](.\img\foto.png) Alberto Noceda Sestayo

## resumen

Actual estudiante en *1º dam* en IES san clemente interesado en la programación y aprender cosas nuevas

## skills

### Language
- Kotlin
- Bash
- Powershell
- python
- php
- html
- css
- markdown

### Tools
1. VS code
2. Intellij
3. Net beans
4. Github

### Storage 
> Sql


---

## Estudios
[Ciber-CEP ](https://www.iessanclemente.net/ciberseguridade/)

[ASIR](https://www.iessanclemente.net/oferta-educativa/presencial/ciclo-superior-de-administracion-de-sistemas-informaticos-en-rede/)

[SMR](https://www.iessanclemente.net/oferta-educativa/presencial/ciclo-medio-de-sistemas-microinformaticos-e-redes/)
```