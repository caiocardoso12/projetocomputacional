//apresentação : https://drive.google.com/file/d/14vaI-AGdFqQ89siwpkWECQd88lBHUrTC/view?usp=drivesdk
//Membros do grupo : Arthur Sales Mendonça 241024562 (criação do vídeo explicativo) Pedro Roberto Miranda de Carvalho 241031932 (criação do vídeo explicativo) Caio Cardoso Guimarães 241008470 (criação dos slides e do código) Karen Beatrice Souza Golçalves 241024526 (criação do código)

#include <iostream>
#include <string>
#include <vector>
#include <limits> 

using namespace std;

struct Contato {
    string nome;
    string email;
    int telefone;
};

vector<Contato> agenda;

void limparCin() {
    cin.clear();
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
}

void adicionar() {
    Contato novoContato;
    cout << "Nome: ";
    getline(cin >> ws, novoContato.nome);
    cout << "Email: ";
    getline(cin, novoContato.email);
    cout << "Telefone: ";
    while (!(cin >> novoContato.telefone)) {
        cout << "Entrada inválida. Por favor, insira um número para o telefone: ";
        limparCin();
    }
    limparCin();
    agenda.push_back(novoContato);
}

void eliminar() {
    int del;
    cout << "Qual contato deseja deletar (índice): ";
    while (!(cin >> del)) {
        cout << "Entrada inválida. Por favor, insira um índice válido: ";
        limparCin();
    }
    if (del >= 0 && del < agenda.size()) {
        agenda.erase(agenda.begin() + del);
    } else {
        cout << "Contato não encontrado.\n";
    }
    limparCin();
}

void editar() {
    int edit;
    cout << "Qual contato deseja editar (índice): ";
    while (!(cin >> edit)) {
        cout << "Entrada inválida. Por favor, insira um índice válido: ";
        limparCin();
    }
    if (edit >= 0 && edit < agenda.size()) {
        cout << "Nome atual: " << agenda[edit].nome << "\n";
        cout << "Novo Nome: ";
        getline(cin >> ws, agenda[edit].nome);
        cout << "Email atual: " << agenda[edit].email << "\n";
        cout << "Novo Email: ";
        getline(cin, agenda[edit].email);
        cout << "Telefone atual: " << agenda[edit].telefone << "\n";
        cout << "Novo Telefone: ";
        while (!(cin >> agenda[edit].telefone)) {
            cout << "Entrada inválida. Por favor, insira um número para o telefone: ";
            limparCin();
        }
    } else {
        cout << "Contato não encontrado.\n";
    }
    limparCin();
}

void listar() {
    cout << "Seus contatos:\n";
    for (size_t i = 0; i < agenda.size(); ++i) {
        const auto& contato = agenda[i];
        cout << i << ". Nome: " << contato.nome << "\n";
        cout << "   Email: " << contato.email << "\n";
        cout << "   Telefone: " << contato.telefone << "\n";
    }
}

void buscar(const string& nome) {
    for (const auto& contato : agenda) {
        if (contato.nome == nome) {
            cout << "Contato encontrado:\n";
            cout << "Nome: " << contato.nome << "\n";
            cout << "Email: " << contato.email << "\n";
            cout << "Telefone: " << contato.telefone << "\n";
            return;
        }
    }
    cout << "Contato não encontrado.\n";
}

int main() {
    int opcao;
    do {
        cout << "\nMenu:\n";
        cout << "1. Adicionar Contato\n";
        cout << "2. Remover Contato\n";
        cout << "3. Buscar Contato\n";
        cout << "4. Listar Contatos\n";
        cout << "5. Editar Contato\n";
        cout << "6. Sair\n";
        cout << "Escolha uma opção: ";
        while (!(cin >> opcao)) {
            cout << "Entrada inválida. Por favor, insira um número entre 1 e 6: ";
            limparCin();
        }

        switch (opcao) {
            case 1:
                adicionar();
                break;
            case 2:
                eliminar();
                break;
            case 3: {
                string nome;
                cout << "Digite o nome do contato: ";
                cin >> ws;
                getline(cin, nome);
                buscar(nome);
                break;
            }
            case 4:
                listar();
                break;
            case 5:
                editar();
                break;
            case 6:
                cout << "Saindo...\n";
                break;
            default:
                cout << "Opção inválida.\n";
        }
    } while (opcao != 6);

    return 0;
}
