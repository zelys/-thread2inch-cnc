## PROGRAMA PARA DESBASTE ROSCA HILO SIERRA DERECHO 45 GRADOS NEGATIVO

```mpf
;PARAMETROS
R1=0
R2=R1
R3=0.5        ;INCREMENTO POR CICLO
R4=300        ;LARGO DE LA ROSCA
R5=50.8       ;PASO DE LA ROSCA
R6=28         ;DISTANCIA ENTRE FILETES
R7=26         ;PROFUNDIDAD DEL FILETE
R8=0.3        ;INCREMENTO EN X
R9=6          ;INCREMENTO EN Z
R10=R3        ;INCREMENTO DESPUÉS DEL CICLO
;------------------------------------------
;PROGRMAMA
G18 G90 G71 G97 G54
T1D1
S18 M4
DIAMOF
;PRIMER CICLO
CICLO:
;CONDICION 1
IF R1+R8 < R3
R1=R1+R8
ELSE
R1=R3
ENDIF
G0 X0
G0 Z0
G0 X=-R1 Z=-R1
G33 Z=-R4 K=R5
G0 X20
G0 Z0
IF R1 < R3 GOTO CICLO
;SEGUNDO CICLO
R2=R1
CICLO2:
;CONDICION 2
IF R2+R9 < R6
R2=R2+R9
ELSE
R2=R6
ENDIF
G0 X=-R1
G0 Z=-R2
G33 Z=-R4 K=R5
G0 X20
G0 Z0
IF R2 < R6 GOTO CICLO2
;CONDICION FINAL
IF R3 < R7
R3=R3+R10
GOTO CICLO
ELSE
IF R3 == R7
M30
ELSE
R3=R7
GOTO CICLO
ENDIF
```

## PROGRAMA PARA ACABADO ROSCA HILO SIERRA DERECHO 45 GRADOS NEGATIVO

```mpf
;PARAMETROS
R0=2476   ;DIAMETRO DE INICIO
R1=0      ;INICIO EJE X
R2=0      ;INICIO EJE Z
R3=0.3    ;INCREMENTO EN X
R4=0.3    ;INCREMENTO EN Z
R5=300    ;LONGITUD DEL CICLO
R6=26     ;VALOR LIMITE PARADA (X-Z)
R7=50.8   ;PASO DE LA ROSCA
;-----------------------------------
;PROGRAMA
G18 G90 G71 G97 G54
T1D1
S18 M4
DIAMOF
R0=(R0/2)-R1
R8=0
R9=0
;CICLO Y CONDICIONES
WHILE (R8 < R6) AND (R9 < R6)
IF (R8+R3 > R6) OR (R9+R4 > R6)
R7=R6
R8=R6
ELSE
R8=R8+R3
R9=R9+R4
ENDIF
IF R3==0
R8=0
ENDIF
IF R4==0
R9=0
ENDIF
MSG("POSICIÓN EJE X " <<R8<<" - POSICIÓN EJE Z " <<R9<<"")
;EJECUCIÓN
G0 X=R0
G0 Z=-R2
G0 X=R0-R8 Z=-R2-R9
G33 Z=-R5 K=R7
G0 X=(R0+R1)+20
G0 Z=-R2
ENDWHILE
M30
```
