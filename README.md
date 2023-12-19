
#Criar um menu interativo
import time
nome_completo = input("Digite seu nome completo: ").split(" ")
pri_nome = nome_completo[0]
time.sleep(0.5)
confirma = int(input("Confirmar acesso ? \n[1]Sim\n[2]Não\n"))

print(f"Olá {pri_nome}, seja bem vindo!")

saldo = 0
limite = 500
esaque = 0
edeposito = 0
numero_saque = 0

#Iniciar as 3 opções
while confirma == 1:
    print(" MENU PRINCIPAL ".center(30, "#"))
    time.sleep(0.5)
    opcoes = int(input('''Selecione a operação que deseja realizar: \n
[1] Saque (um, para saque)\n
[2] Depósito (dois, para depósitos)\n
[3] Extrato (três, para extratos)\n
[4] Sair (quatro, para sair)\n
'''))

    if opcoes == 1: #Saque
        print(" SAQUE ".center(30, "#"))
        print(f"Seu saldo atual: R${saldo:.2f}\n")
        loop = 3
        while loop > 0 and loop <= 3:
            if limite <= 0:
                print("Você excedeu seu limite para saque, por favor tente novamente amanhã.\n")
                break
            else:
                saque = float(input("Qual valor deseja sacar?\nR$"))
                if saque <= saldo and saque <= limite and saque > 0:
                    saldo_saque = saldo - saque
                    saldo = saldo_saque
                    print("Aguarde a contagem das notas!\n")
                    time.sleep(2.5)
                    print(f"Você sacou R${saque:.2f}\n")
                    reducao_limite = limite - saque
                    limite = reducao_limite #Atualização da variável limite
                    esaque += saque #Registro do saque
                    loop -= 1
                    print(f"Seu saldo atual é de: R${saldo:.2f}\nVocê ainda possui {loop} saques restantes e R${limite:.2f} de limite diário para saque.\n")
                    time.sleep(2)
                    if limite <= 0:
                        print("Você excedeu seu limite diário para saque, por favor tente novamente amanhã.\n")
                        time.sleep(2)
                        break
                    saida = int(input("Deseja encerrar a operação? \n[1]Sim\n[2]Não\n"))
                    if saida == 1:
                        print("Encerrando!\n")
                        time.sleep(2)
                        break
                elif saque == 0:
                    print("Não é possível sacar zero reais!\n")
                    time.sleep(2)
                else:
                    print("Você não possui saldo ou limite para saque o suficiente para realizar esta operação.\n")
                    time.sleep(2)
                    break
    elif opcoes == 2: #Deposito
        print(" DEPOSITO ".center(30, "#"))
        print(f"Saldo atual: R${saldo:.2f}\n")
        condicao = int(input("Deseja realizar um depósito ? \n[1]Sim\n[2]Não\n"))
        if condicao == 1:
            deposito = float(input("Qual valor deseja depositar?\nR$"))
            saldo += deposito #Atualização do valor da variável saldo
            print("Depósito realizado com sucesso!\n")
            print(f"Seu novo saldo atual é de: R${saldo:.2f}\n")
            edeposito += deposito #Registro do depósito
        elif condicao == 2:
            print("Saindo!\n")
        else:
            print("Por favor, digite uma opção válida!\n")
    elif opcoes == 3: #Extrato
        print(" EXTRATO ".center(30, "#"))
        print("Aguarde um segundo...\n")
        time.sleep(3)
        print(f"Você depositou R${edeposito:.2f} e sacou R${esaque:.2f}, seu saldo atual R${saldo:.2f}.")
    elif opcoes == 4: #Sair
        print("Encerrando!")
        break
    else:
        print("Por favor, digite uma opção válida!")
