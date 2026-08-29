# Descripcion
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.

Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!
## Solucion
raxel05-academy@webshell:~$ ssh -p 62391 ctf-player@atlas.picoctf.net
ctf-player@atlas.picoctf.net's password: 
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Higher! Try again.
Enter your guess: 750
Higher! Try again.
Enter your guess: 850
Lower! Try again.
Enter your guess: 800
Higher! Try again.
Enter your guess: 825
Higher! Try again.
Enter your guess: 835
Higher! Try again.
Enter your guess: 845
Lower! Try again.
Enter your guess: 840
Higher! Try again.
Enter your guess: 842
Congratulations! You guessed the correct number: 842
Here's your flag: picoCTF{g00d_gu355_3af33d18}
## Notas Adicionales
+ funcionamiento del algoritmo de busqueda binaria
## Referencias
https://webshell.cylabacademy.org
