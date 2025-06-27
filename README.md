# InovaTech 
import os
import csv

DATA_DIR = "data"
NOTAS_FILE = os.path.join(DATA_DIR, "notas_fiscais.csv")

def criar_pasta_data():
    if not os.path.exists(DATA_DIR):
        os.makedirs(DATA_DIR)

def salvar_nota_fiscal(numero, valor, descricao):
    criar_pasta_data()
    arquivo_existe = os.path.isfile(NOTAS_FILE)
    with open(NOTAS_FILE, mode='a', newline='', encoding='utf-8') as f:
        writer = csv.writer(f)
        if not arquivo_existe:
            writer.writerow(["Número", "Valor", "Descrição"])
        writer.writerow([numero, valor, descricao])

def listar_notas():
    if not os.path.isfile(NOTAS_FILE):
        print("Nenhuma nota fiscal lançada ainda.")
        return
    with open(NOTAS_FILE, mode='r', encoding='utf-8') as f:
        reader = csv.reader(f)
        next(reader)  # pular cabeçalho
        print("\nNotas Fiscais Lançadas:")
        for row in reader:
            print(f"Número: {row[0]}, Valor: R${row[1]}, Descrição: {row[2]}")
        print()

def menu():
    print("===================================")
    print("      Bem-vindo ao InovaTech       ")
    print("  IA para Contabilidade e Finanças ")
    print("===================================\n")

    print("1 - Lançar Nota Fiscal")
    print("2 - Gerar Relatório Financeiro (em desenvolvimento)")
    print("3 - Planejamento Financeiro (em desenvolvimento)")
    print("4 - Resumo Mensal (em desenvolvimento)")
    print("5 - Listar Notas Fiscais")
    print("0 - Sair")

    escolha = input("\nEscolha uma opção: ")

    if escolha == '0':
        print("Encerrando o InovaTech. Até logo!")
        return False
    elif escolha == '1':
        numero = input("Número da nota fiscal: ")
        valor = input("Valor da nota fiscal (ex: 1500.00): ")
        descricao = input("Descrição da nota fiscal: ")
        salvar_nota_fiscal(numero, valor, descricao)
        print("Nota fiscal lançada com sucesso!\n")
        return True
    elif escolha == '5':
        listar_notas()
        return True
    else:
        print(f"Opção {escolha} em desenvolvimento...\n")
        return True

def main():
    continuar = True
    while continuar:
        continuar = menu()

if __name__ == "__main__":
    main()
    
