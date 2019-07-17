# Símbolos 
 
El archivo `visibility.c` tiene muchos tipos de símbolos. En
este trabajo sólo tienen que compilar el objeto `visibility.o` 
e identificar los símbolos, ejecutando:

```
make object
```

nm visibility.o 

0000000000000000 t add_abs
000000000000002a T main
                 U printf
0000000000000000 r val1  variable constante estatica
0000000000000004 R val2  variable constante global  
0000000000000000 d val3  variable estatica
0000000000000004 D val4  variable global

