El fichero ``vuln.c`` contiene un código vulnerable ya que copiamos utilizando funciones inseguras lo que nos pase el usuario como input a un buffer. El input del usuario puede ser mayor que el buffer lo que hace que se pueda desbordar.

El archivo ``buffer_dps.pdf`` subido a este repositorio contiene un informe más exahustivo que este resumen.

# RESUMEN:
Utilizamos msfvenom para generar un shellcode para el sistema freeBSD x64 que es la máquina virtual a la que hemos desactivado las protecciones.

## Creación payload
```bash
msfvenom -p bsd/x64/exec CMD="/bin/sh" -f hex 
4831d2e8080000002f62696e2f7368005f52574889e64831c04883c83b0f05
```
## Explotación
Después de hacer debugging con gdb terminamos creando ``exploit_iterative1.py`` para explotar la vulnerabilidad probando con diferentes direcciones de memoria cercanas a las vistas con gdb.

### Extra
Se crea una versión del binario vulnerable con el setuid activado y se retoca el shellcode para que aproveche esta situación: ``exploit_iterative2.py``.