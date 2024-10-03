#include <iostream>

using namespace std;

const int NUM_FILEIRAS = 10;
const int NUM_ASSENTOS = 6;
char assentos[NUM_FILEIRAS][NUM_ASSENTOS] = {{'O', 'O', 'O', 'O', 'O', 'O'}};  


void exibirAssentos() {
    cout << "\nMapa de Assentos (X = Reservado, O = Disponível):" << endl;
    for (int i = 0; i < NUM_FILEIRAS; ++i) {
        cout << "Fileira " << i + 1 << ": ";
        for (int j = 0; j < NUM_ASSENTOS; ++j) {
            cout << char('A' + j) << "[" << assentos[i][j] << "] ";
        }
        cout << endl;
    }
    cout << endl;
}


bool assentoJaReservado(int fileira, char poltrona) {
    int coluna = poltrona - 'A';
    return assentos[fileira - 1][coluna] == 'X';
}


bool reservarAssento(int fileira, char poltrona, int tipoPassagem) {
    int coluna = poltrona - 'A';

  
    if (assentos[fileira - 1][coluna] == 'X') {
        cout << "Esse assento já está reservado. Por favor, escolha outro." << endl;
        return false;
    }


    if (tipoPassagem == 2 && (poltrona == 'A' || poltrona == 'F')) {
        cout << "Não é permitido reservar assentos nas janelas para passagens econômicas." << endl;
        return false;
    }

 
    if (tipoPassagem == 1 && !(poltrona == 'A' || poltrona == 'F')) {
        cout << "Recomendamos reservar as poltronas prioritárias A ou F para a classe Executiva." << endl;
    }

 
    assentos[fileira - 1][coluna] = 'X';
    cout << "Assento " << poltrona << " na fileira " << fileira << " reservado com sucesso." << endl;
    return true;
}

int main() {
    bool continuar = true;

    while (continuar) {
        
        exibirAssentos();

       
       

        int fileira;
        char poltrona;
        int tipoPassagem;

        cout << "Digite a fileira (1-10): ";
        cin >> fileira;
        cout << "Digite a poltrona [A][B][C][D][E][F]: ";
        cin >> poltrona;
        poltrona = toupper(poltrona);  
        cout << "Tipo de passagem (1-Executivo, 2-Econômico): ";
        cin >> tipoPassagem;

        
        while (!reservarAssento(fileira, poltrona, tipoPassagem)) {
            
            cout << "Digite uma nova poltrona [A][B][C][D][E][F]: ";
            cin >> poltrona;
            poltrona = toupper(poltrona);  
        }

        
        char resposta;
        cout << "Deseja reservar outra passagem? (s/n): ";
        cin >> resposta;
        resposta = tolower(resposta); 

        if (resposta == 'n') {
            continuar = false;
            cout << "Encerrando o sistema de reservas..." << endl;
        }
    }

    return 0;
}
