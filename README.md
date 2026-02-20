[ProjetoEstruturaDeDados.py](https://github.com/user-attachments/files/25430158/ProjetoEstruturaDeDados.py)

[Uploading 
# =========================
# NÓ DA LISTA ENCADEADA
# =========================
class No:
    def __init__(self, valor):
        self.valor = valor
        self.proximo = None


# =========================
# FILA 
# =========================
class Fila:
    def __init__(self):
        self.inicio = None
        self.fim = None
        self.tamanho = 0

    def enfileirar(self, valor):
        novo = No(valor)
        if self.fim is None:
            self.inicio = novo
            self.fim = novo
        else:
            self.fim.proximo = novo
            self.fim = novo
        self.tamanho += 1

    def desenfileirar(self):
        if self.inicio is None:
            return None
        removido = self.inicio
        self.inicio = self.inicio.proximo
        if self.inicio is None:
            self.fim = None
        self.tamanho -= 1
        return removido.valor

    def esta_vazia(self):
        return self.inicio is None

    def imprimir(self):
        atual = self.inicio
        while atual:
            print(f"Nome: {atual.valor['nome']} | CPF: {atual.valor['cpf']}")
            atual = atual.proximo


# =========================
# PILHA 
# =========================
class Pilha:
    def __init__(self):
        self.topo = None
        self.tamanho = 0

    def empilhar(self, valor):
        novo = No(valor)
        novo.proximo = self.topo
        self.topo = novo
        self.tamanho += 1

    def desempilhar(self):
        if self.topo is None:
            return None
        removido = self.topo
        self.topo = self.topo.proximo
        self.tamanho -= 1
        return removido.valor

    def esta_vazia(self):
        return self.topo is None


# =========================
# PROGRAMA PRINCIPAL
# =========================

fila = Fila()
pilha_frascos = Pilha()
vacinados = []  # Lista comum

# 0 - Empilhar 3 frascos com 5 doses cada
for i in range(3):
    pilha_frascos.empilhar(5)

dose_atual = 0
frascos_usados = 0


def doses_disponiveis():
    total = 0
    atual = pilha_frascos.topo
    while atual:
        total += atual.valor
        atual = atual.proximo
    return total


while True:
    print("\n===== MENU =====")
    print("1 - Adicionar pessoa")
    print("2 - Pessoas da Fila")
    print("3 - Doses disponíveis")
    print("4 - Vacinar uma pessoa")
    print("5 - Exibir total de pessoas vacinadas")
    print("0 - Sair")

    opcao = input("Escolha: ")

    if opcao == "1":
        if fila.tamanho >= 15:
            print("Fila cheia! Limite diário atingido.")
        else:
            nome = input("Nome: ")
            cpf = input("CPF: ")
            fila.enfileirar({"nome": nome, "cpf": cpf})
            print("Pessoa adicionada à fila!")

    elif opcao == "2":
        if fila.esta_vazia():
            print("Fila vazia.")
        else:
            fila.imprimir()

    elif opcao == "3":
        print("Total de doses disponíveis:", doses_disponiveis())

    elif opcao == "4":
        if fila.esta_vazia():
            print("Ninguém na fila.")
        elif pilha_frascos.esta_vazia():
            print("Não há mais vacinas disponíveis.")
        else:
            if dose_atual == 0:
                dose_atual = pilha_frascos.desempilhar()
                frascos_usados += 1

            pessoa = fila.desenfileirar()
            dose_atual -= 1
            numero_dose = 6 - dose_atual - 1

            print("\nPessoa vacinada!")
            print("Nome:", pessoa["nome"])
            print("CPF:", pessoa["cpf"])
            print("Dose número:", numero_dose)

            vacinados.append(pessoa["nome"])

            if dose_atual == 0:
                print("Frasco finalizado!")

    elif opcao == "5":
        print("Total de pessoas vacinadas:", len(vacinados))

    elif opcao == "0":
        print("Encerrando programa.")
        break

    else:
        print("Opção inválida.")
ProjetoEstruturaDeDados.py…]()
