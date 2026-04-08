# sistema-lava-rapido
Descrição
Esse programa em C# simula um sistema simples de atendimento para um lava rápido, permitindo registrar serviços, calcular valores e gerar um recibo final.
O sistema funciona como um menu interativo no console, onde o usuário (atendente) pode escolher serviços de lavagem para um cliente, informar quantidades e, ao final, ver o total a pagar.
Como o programa funciona
1. Entrada de dados
O programa começa pedindo o nome do cliente.
Esse nome será exibido no recibo final.
2. Menu de serviços

Dentro de um laço do...while, o sistema mostra as opções:

Carro pequeno → R$ 30,00
Carro grande → R$ 50,00
Moto pequena → R$ 15,00
Moto grande → R$ 25,00
Lavagem de motor → R$ 40,00
Lavagem de chassi → R$ 35,00
Finalizar atendimento

O usuário escolhe uma opção digitando um número.

Código completo
using System;

class Program
{
    static void Main()
    {
        string cliente = LerCliente();
        ExecutarSistema(cliente);
    }

    // Função para ler o nome do cliente
    static string LerCliente()
    {
        Console.Write("Digite o nome do cliente: ");
        return Console.ReadLine();
    }

    // Função principal do sistema
    static void ExecutarSistema(string cliente)
    {
        int opcao;
        double total = 0;
        string resumo = "";

        do
        {
            MostrarMenu();
            opcao = int.Parse(Console.ReadLine());

            if (opcao >= 1 && opcao <= 6)
            {
                Console.Write("Quantidade: ");
                int quantidade = int.Parse(Console.ReadLine());

                string servico = "";
                double preco = ObterPrecoEServico(opcao, out servico);

                double subtotal = preco * quantidade;
                total += subtotal;

                resumo += $"{servico} x{quantidade} = R$ {subtotal:F2}\n";

                Console.WriteLine("✅ Serviço adicionado!");
            }
            else if (opcao != 7)
            {
                Console.WriteLine("❌ Opção inválida!");
            }

        } while (opcao != 7);

        MostrarRecibo(cliente, resumo, total);
    }

    // Menu
    static void MostrarMenu()
    {
        Console.WriteLine("\n===== LAVA RÁPIDO =====");
        Console.WriteLine("1 - Carro pequeno (R$ 30,00)");
        Console.WriteLine("2 - Carro grande (R$ 50,00)");
        Console.WriteLine("3 - Moto pequena (R$ 15,00)");
        Console.WriteLine("4 - Moto grande (R$ 25,00)");
        Console.WriteLine("5 - Lavagem de motor (R$ 40,00)");
        Console.WriteLine("6 - Lavagem de chassi (R$ 35,00)");
        Console.WriteLine("7 - Finalizar");
        Console.Write("Escolha uma opção: ");
    }

    // Retorna preço e nome do serviço
    static double ObterPrecoEServico(int opcao, out string servico)
    {
        double preco = 0;
        servico = "";

        switch (opcao)
        {
            case 1:
                servico = "Carro pequeno";
                preco = 30;
                break;
            case 2:
                servico = "Carro grande";
                preco = 50;
                break;
            case 3:
                servico = "Moto pequena";
                preco = 15;
                break;
            case 4:
                servico = "Moto grande";
                preco = 25;
                break;
            case 5:
                servico = "Lavagem de motor";
                preco = 40;
                break;
            case 6:
                servico = "Lavagem de chassi";
                preco = 35;
                break;
        }

        return preco;
    }

    // Exibe o recibo final
    static void MostrarRecibo(string cliente, string resumo, double total)
    {
        Console.WriteLine("\n===== RECIBO =====");
        Console.WriteLine($"Cliente: {cliente}");
        Console.WriteLine("Serviços:");
        Console.WriteLine(resumo);
        Console.WriteLine($"TOTAL: R$ {total:F2}");
        Console.WriteLine("Obrigado pela preferência!");
    }
}
