# Proyecto-1
En esta ocasión se le presentaran 2 ejercicios usando pseudocodigo, python y c++ 
# El primer ejercicio es denominado el juego del ahorcado en python

import random
AHORCADO = ['''
      +---+
      |   |
          |
          |
          |
          |
    =========''', '''
      +---+
      |   |
      O   |
          |
          |
          |
    =========''', '''
      +---+
      |   |
      O   |
      |   |
          |
          |
    =========''', '''
      +---+
      |   |
      O   |
     /|   |
          |
          |
    =========''', '''
      +---+
      |   |
      O   |
     /|\  |
          |
          |
    =========''', '''
      +---+
      |   |
      O   |
     /|\  |
     /    |
          |
    =========''', '''
      +---+
      |   |
      O   |
     /|\  |
     / \  |
          |
    =========''']
palabras = 'telefono, manzana, fruta, verdura, musica'.split()
 
def buscarPalabraAleat(listaPalabras):
    palabraAleatoria = random.randint(0, len(listaPalabras) - 1)
    return listaPalabras[palabraAleatoria]
 
def displayBoard(AHORCADO, letraIncorrecta, letraCorrecta, palabraSecreta):
    print(AHORCADO[len(letraIncorrecta)])
    print ("")
    fin = " "
    print ('Letras incorrectas:', fin)
    for letra in letraIncorrecta:
        print (letra, fin)
    print ("")
    espacio = '_' * len(palabraSecreta)
    for i in range(len(palabraSecreta)):

        if palabraSecreta[i] in letraCorrecta:
            espacio = espacio[:i] + palabraSecreta[i] + espacio[i+1:]
    for letra in espacio:
    
        print (letra, fin)
    print ("")
 
def elijeLetra(algunaLetra):
    
    while True:
        print ('Adivina una letra:')
        letra = input()
        letra = letra.lower()
        if len(letra) != 1:
            print ('Introduce una sola letra.') 
        elif letra in algunaLetra:
            print ('Esa letra ya existe deseas buscar otra letra? ')
        elif letra not in 'abcdefghijklmnopqrstuvwxyz':
            print ('Elije una letra.')
        else:
            return letra
 
def empezar():
    
    print ('Quieres jugar de nuevo? (Si o No)')
    return input().lower().startswith('s')
 
print ('A H O R C A D O')
letraIncorrecta = ""
letraCorrecta = ""
palabraSecreta = buscarPalabraAleat(palabras)
finJuego = False
while True:
    displayBoard(AHORCADO, letraIncorrecta, letraCorrecta, palabraSecreta)
 = elijeLetra(letraIncorrecta + letraCorrecta)
    if letra in palabraSecreta:
        letraCorrecta = letraCorrecta + letra
        
        letrasEncontradas = True
        for i in range(len(palabraSecreta)):
            if palabraSecreta[i] not in letraCorrecta:
                letrasEncontradas = False
                break
        if letrasEncontradas:
            print ('¡Excelente! La palabra secreta es "' + palabraSecreta + '"! ¡Has ganado Felicitaciones!')
            finJuego = True
    else:
        letraIncorrecta = letraIncorrecta + letra
        if len(letraIncorrecta) == len(AHORCADO) - 1:
            displayBoard(AHORCADO, letraIncorrecta, letraCorrecta, palabraSecreta)
            print ('¡Te has quedado sin palabras!\nDespues de ' + str(len(letraIncorrecta)) + ' letras erroneas y ' + str(len(letraCorrecta)) + ' letras correctas, la palabra era "' + palabraSecreta + '"')
            finJuego = True
    
    if finJuego:
        if empezar():
            letraIncorrecta = ""
            letraCorrecta = ""
            finJuego = False
            palabraSecreta = buscarPalabraAleat(palabras)
        else:
            break
  #se mostrara el juego del ahorcado en c++

#include <iostream>
#include <string>
#include <ctime> 
#include <cstdlib> 

using namespace std;

void LimpiarPantalla();
void JugarPartida();
void Dibujar();

char eleccion;
string palabras[] = {"futbol, voleibol, wifi, gato"};
string palabra, fallidas; 
int nA;
int vida;
bool correcta, completa;

int main(){
    while(true){
        vida = 6;
        palabra = "";
        fallidas = "";
        LimpiarPantalla();
        cout<<"\t::::MENU::::"<<endl;
        cout<<"1) empezar partida"<<endl;
        cout<<"2) Salir."<<endl;
        cout<<"Eleccion: ";
        cin>>eleccion;
        switch(eleccion){
            case '1':
                JugarPartida();
                break;
            case '2':
                return 0;
        }
    }
}

void JugarPartida(){
    srand(static_cast<unsigned>(time(NULL)));
    nA = rand() % 10;
    
    for(int i = 0; i < static_cast<int>(palabras[nA].size()); i++){
        palabra += "-";
    }
    
    while(vida > 0){
        LimpiarPantalla();
        cout<<"\t::: A H O R C A D O :::"<<endl;
        Dibujar();
        cout<<"Fallos: "<<fallidas;
        cout<<"  Progreso: "<<palabra<<endl;
        cout<<"Ingresa una letra(minuscula): ";
        cin>>eleccion;
        
        correcta = false;
        for(int i = 0; i < static_cast<int>(palabras[nA].size()); i++){
            if(palabras[nA][i] == eleccion){
                palabra[i] = eleccion;
                correcta = true;    
            }
        }
        if(!correcta){
            vida--;
            fallidas += eleccion;
        }
        
        completa = true;
        for(int i = 0; i < static_cast<int>(palabra.size()); i++){
            if(palabra[i] == '-'){
                completa = false;
            }
        }
        if(completa){
            LimpiarPantalla();
            cout<<"\t::: A H O R C A D O :::"<<endl;
            Dibujar();
            cout<<"Palabra: "<<palabras[nA]<<endl;
            cout<<"Ganaste. Ingresa un caracter para continuar: ";
            cin>>eleccion;
            return;
        }
    }
    LimpiarPantalla();
    cout<<"\t::: A H O R C A D O :::"<<endl;
    Dibujar();
    cout<<"Palabra: "<<palabras[nA]<<endl;
    cout<<"Perdiste. Ingresa una palabra para seguir jugando: ";
    cin>>eleccion;
}

void Dibujar(){
    switch(vida){
        case 6:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
        case 5:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |      O"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
        case 4:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |      O"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
        case 3:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |      O"<<endl;
        cout<<"  |     /|"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
        case 2:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |      O"<<endl;
        cout<<"  |     /|\\"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
        case 1:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |      O"<<endl;
        cout<<"  |     /|\\"<<endl;
        cout<<"  |     /"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
        case 0:
        cout<<"  --------"<<endl;
        cout<<"  |      |"<<endl;
        cout<<"  |      O"<<endl;
        cout<<"  |     /|\\"<<endl;
        cout<<"  |     / \\"<<endl;
        cout<<"  |"<<endl;
        cout<<"  |"<<endl;
        cout<<" ---"<<endl;
        break;
    }
}


void LimpiarPantalla(){
    if(system("clear") == -1){
        cout<<"Error al borrar la pantalla.";
    }
} 


#El siguiente caso se mostrara el triple de pitagoras en c++

#include <iostream>

using namespace std;

int main() {
    int limite = 500;
    cout << "Triples de Pitagoras menores o iguales a " << limite << ":" << endl;

    for (int lado1 = 1; lado1 <= limite; lado1++) {
        for (int lado2 = lado1; lado2 <= limite; lado2++) {
            for (int hipotenusa = lado2; hipotenusa <= limite; hipotenusa++) {
                if (lado1 * lado1 + lado2 * lado2 == hipotenusa * hipotenusa) {
                    cout << "Lado1: " << lado1 << ", Lado2: " << lado2 << ", Hipotenusa: " << hipotenusa << endl;
                }
            }
        }
    }

    return 0;
}


#Pitagoras en pseudocodigo 

Algoritmo TriplesPitagoras
    Definir limite, lado1, lado2, hipotenusa como Entero
    
    limite <- 500
    
    Escribir "Triples de Pitágoras menores o iguales a ", limite, ":"
    
    Para lado1 <- 1 Hasta limite Hacer
        Para lado2 <- 1 Hasta limite Hacer
            Para hipotenusa <- 1 Hasta limite Hacer
                Si lado1^2 + lado2^2 = hipotenusa^2 Entonces
                    Escribir "Lado1:", lado1, ", Lado2:", lado2, ", Hipotenusa:", hipotenusa
                FinSi
            FinPara
        FinPara
    FinPara
    
FinAlgoritmo

#pitagoras en python 

limite = 500
print("Triples de Pitagoras menores o iguales a", limite, ":")

for lado1 in range(1, limite + 1):
    for lado2 in range(lado1, limite + 1):
        for hipotenusa in range(lado2, limite + 1):
            if lado1 ** 2 + lado2 ** 2 == hipotenusa ** 2:
                print("Lado1:", lado1, ", Lado2:", lado2, ", Hipotenusa:", hipotenusa)

                
