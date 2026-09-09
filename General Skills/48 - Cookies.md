
# Descripcion
Who doesn't love cookies? Try to figure out the best one.
## Solucion
`marquez@marquez-VirtualBox:~/Escritorio$ for i in {1..20}; do   curl -s http://wily-courier.picoctf.net:50714/check     -H "Cookie: name=$i" | grep "pico"; done`
            `<p style="text-align:center; font-size:30px;"><b>Flag</b>: <code>picoCTF{3v3ry1_l0v3s_c00k135_a4dadb49}`

## Notas Adicionales
+ con un ciclo en el bash usando curl -s y modificando la cookie en cada iteracion buscar la bandera con un grep
## Referencias

