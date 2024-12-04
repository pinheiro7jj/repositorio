# La class sport bike

# descrição
Aqui será apresentado um código, para uma loja de bicicletas, terá uma pagina de cadastro, um carrinho para adicionar suas compras, você poderá ver o preço antes de adicionar ao carrinho e quando você colocar mais de um item no carrinho ele irá somar os preços dos produtos.
# código
    import tkinter as tk
      from tkinter import ttk, messagebox


      #Função para abrir a janela de busca de produtos
      def abrir_janela():
          janela2 = tk.Toplevel()
          janela2.title("Janela Nova")
          janela2.configure(bg='white')

          # Carrinho de compras
          carrinho = {}

          # Mensagem do sistema
          mensagem = tk.Label(
              janela2, text="Buscar Produtos", fg='white', bg='black', width=65, height=5, font='Georgia 25 bold')
          mensagem.grid(row=0, column=0, columnspan=3, sticky="NSEW")

          # Dicionário de produtos
          produtos = {
              'Bicicleta Hupinaja': 4000,
              'Bicicleta Gios 4trix': 2800,
              'Bicicleta Viking X': 1450,
              'Bicicleta Sense Activ': 3290,
              'Bicicleta Sense Grom 24': 4290,
              'Bicicleta Swift Enduravox Comp': 10000,
              'Bicicleta Caad Optimo Cannondale': 7990,
              'Bicicleta Absolute Nero 5': 2000,
              'Bicicleta Fun Evo': 3190,
              'Bicicleta Sense Versa Comp': 7990,
              'Bicicleta Impact Race': 9990,
              'Bicicleta Aro 26 Monark Barra Circular': 840,
          }

          # Combobox para seleção de produtos
          moedas = list(produtos.keys())
          moeda = ttk.Combobox(janela2, values=moedas)
          moeda.grid(row=1, column=0, sticky="w", padx=10, pady=10)

          # Label para exibir o preço do produto selecionado
          preco_label = tk.Label(janela2, text="Preço: ", bg="white", fg="black", font='Georgia 10 bold')
          preco_label.grid(row=1, column=1, sticky="w", padx=10)

          # Função para exibir o preço do produto selecionado
          def exibir_preco(event):
              produto_selecionado = moeda.get().strip()
              if produto_selecionado in produtos:
                  preco = produtos[produto_selecionado]
                  preco_label.config(text=f"Preço: R$ {preco}")
              else:
                  preco_label.config(text="Preço: Produto inválido")

          moeda.bind("<<ComboboxSelected>>", exibir_preco)

          # Label para o valor total do carrinho
          total_label = tk.Label(janela2, text="Total: R$ 0.00", bg="white", fg="black", font='Georgia 10 bold')
          total_label.grid(row=4, column=0, columnspan=3, pady=10)

          # Função para adicionar produtos ao carrinho
          def adicionar_ao_carrinho():
              produto_selecionado = moeda.get().strip()
              if produto_selecionado in produtos:
                  if produto_selecionado in carrinho:
                      carrinho[produto_selecionado] += 1
                  else:
                      carrinho[produto_selecionado] = 1
                  atualizar_carrinho()
              else:
                  messagebox.showerror("Erro", "Selecione um produto válido!")

          # Função para remover produtos do carrinho
          def remover_do_carrinho():
              produto_selecionado = moeda.get().strip()
              if produto_selecionado in carrinho:
                  carrinho[produto_selecionado] -= 1
                  if carrinho[produto_selecionado] <= 0:
                      del carrinho[produto_selecionado]
                  atualizar_carrinho()
              else:
                  messagebox.showerror("Erro", "Este produto não está no carrinho!")

          # Função para atualizar a exibição do carrinho e o total
          def atualizar_carrinho():
              lista_carrinho.delete(0, tk.END)  # Limpa a lista
              total = 0
              for produto, quantidade in carrinho.items():
                  lista_carrinho.insert(tk.END, f"{produto} (Quantidade: {quantidade})")
                  total += produtos[produto] * quantidade
              total_label.config(text=f"Total: R$ {total:.2f}")

          # Botão para adicionar ao carrinho
          botao_adicionar = tk.Button(janela2, text="Adicionar ao carrinho", command=adicionar_ao_carrinho)
          botao_adicionar.grid(row=2, column=0, padx=10, pady=10)

          # Botão para remover do carrinho
          botao_remover = tk.Button(janela2, text="Remover do carrinho", command=remover_do_carrinho)
          botao_remover.grid(row=2, column=1, padx=10, pady=10)

          # Lista para exibir o carrinho
          lista_carrinho = tk.Listbox(janela2, width=60, height=10)
          lista_carrinho.grid(row=3, column=0, columnspan=3, padx=10, pady=10)

          # Função para finalizar a compra
          def finalizar_compra():
              if carrinho:
                  total = sum(produtos[produto] * quantidade for produto, quantidade in carrinho.items())
                  messagebox.showinfo("Compra Finalizada", f"Total: R$ {total:.2f}\nObrigado pela compra!")
                  carrinho.clear()
                  atualizar_carrinho()
              else:
                  messagebox.showerror("Erro", "O carrinho está vazio!")

          # Botão para finalizar a compra
          botao_finalizar = tk.Button(janela2, text="Finalizar Compra", command=finalizar_compra)
          botao_finalizar.grid(row=5, column=0, columnspan=3, pady=10)


      #Função para abrir a janela de cadastro
      def abrir_cadastro():
          janela_cadastro = tk.Toplevel()
          janela_cadastro.title("Cadastro do Cliente")
          janela_cadastro.configure(bg='white')

          # Label e entrada para nome
          label_nome = tk.Label(janela_cadastro, text="Nome:", fg='black', bg='white', font='Georgia 10 bold')
          label_nome.grid(row=0, column=0, padx=10, pady=10, sticky="w")
          entrada_nome = tk.Entry(janela_cadastro, width=30)
          entrada_nome.grid(row=0, column=1, padx=10, pady=10)

          # Label e entrada para e-mail
          label_email = tk.Label(janela_cadastro, text="E-mail:", fg='black', bg='white', font='Georgia 10 bold')
          label_email.grid(row=1, column=0, padx=10, pady=10, sticky="w")
          entrada_email = tk.Entry(janela_cadastro, width=30)
          entrada_email.grid(row=1, column=1, padx=10, pady=10)

          # Label e entrada para telefone
          label_telefone = tk.Label(janela_cadastro, text="Telefone:", fg='black', bg='white', font='Georgia 10 bold')
          label_telefone.grid(row=2, column=0, padx=10, pady=10, sticky="w")
          entrada_telefone = tk.Entry(janela_cadastro, width=30)
          entrada_telefone.grid(row=2, column=1, padx=10, pady=10)

          # Função para validar o cadastro
          def validar_cadastro():
              nome = entrada_nome.get().strip()
              email = entrada_email.get().strip()
              telefone = entrada_telefone.get().strip()

              if not nome or not email or not telefone:
                  messagebox.showerror("Erro", "Todos os campos são obrigatórios!")
              elif not email.endswith("@gmail.com"):
                  messagebox.showerror("Erro", "E-mail inválido! Use um e-mail @gmail.com")
              else:
                  messagebox.showinfo("Cadastro", "Cadastro realizado com sucesso!")

          # Botão para validar o cadastro
          botao_cadastrar = tk.Button(janela_cadastro, text="Cadastrar", command=validar_cadastro)
          botao_cadastrar.grid(row=3, column=0, columnspan=2, pady=10)


      #Janela principal
      janela = tk.Tk()
      janela.title("Janela Principal")
      janela.configure(bg='black')

      mensagem = tk.Label(
          janela, text="La Class Sport Bike", fg='black', bg='beige', width=65, height=7, font='Georgia 25 bold')
      mensagem.grid(row=1, column=1, columnspan=2, sticky="NSEW")

      #Botão para abrir a página de busca de produtos
      botao_produtos = tk.Button(janela, text="Página de busca de produtos", fg='white', bg='black', command=abrir_janela)
      botao_produtos.grid(row=2, columnspan=3, pady=10)

      #Botão para abrir a página de cadastro
      botao_cadastro = tk.Button(janela, text="Página de cadastro", fg='white', bg='black', command=abrir_cadastro)
      botao_cadastro.grid(row=3, columnspan=3, pady=10)

      janela.mainloop()



# contato

vinicius pinheiro -
email:vinicius_pinheiro1@estudante.sesisenai.org.br

guilherme antunes torres -
email:guilherme_a_torres@estudante.sesisenai.org.br
