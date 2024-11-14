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

```
- Powershell
``` powershell

```
- python
```

```
[repositorio]()
- php
```php
```
- html\css
``` html css

```
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