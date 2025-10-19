# 🚀 Tutorial: Instalando Armbian em TV Box com RK3229

Este guia mostra como configurar sua TV Box com chip RK3229 usando o Armbian, desde a gravação do multitool até o autologin via SSH.

É possível seguir a documentação de instalação com outros chips (amlogic, allwinner e etc), porem é necessario efetuar o teste com imagens apropriadas do armbian.



## ⚠️ Requisitos importantes

- **Adaptador de cartão SD para USB**  
  Certifique-se de possuir um adaptador compatível. Você pode comprá-lo [aqui](https://mercadolivre.com/sec/2trNZa2).

- **Cartão SD com no mínimo 32GB**  
  É necessário um cartão com essa capacidade mínima. Você pode comprá-lo [aqui](https://mercadolivre.com/sec/2mhNMv8).

- **Patch Cord CAT6**
  É necessário um patch cord para conexao estavel. Você pode comprá-lo [aqui](https://mercadolivre.com/sec/23CxYAc).

- **Tv Box**
  É necessário uma tv box com rockchip. Você pode comprá-lo [aqui](https://mercadolivre.com/sec/23CxYAc).



---

## 🛠️ Etapa 1: Gravar o Multitool no cartão SD

Você pode baixa-lo [aqui]().


```bash
sudo unxz -c /home/elima/Downloads/armbian/multitool_f.img.xz | sudo dd of=/dev/sda bs=4M status=progress conv=fsync
```

Agora mova a imagem do armbian para a pasta images.
Você pode baixa-la [aqui]().
#### ⚠️ Se houver erro ao mover a imagem para a pasta images, desmonte o disco e expanda a partição MULTITOOL.

---

## 📺 Etapa 2: Preparar a TV Box com o controle remoto

### Passos para configuração inicial
0. Deixe o **cartão SD** posicionado na bandeja
1. Acesse o menu **Configurações** da TV Box.
2. Selecione a opção **Redefinição de fábrica**.
3. Quando a tela exibir **"Reiniciando"**, insira o **cartão SD** na bandeja .
4. Aguarde o processo de **boot** — pode levar alguns minutos.
5. Utilize o **cabo HDMI original** da TV Box para garantir compatibilidade.

#### ⚠️  Durante essa fase, a imagem pode piscar ou apresentar **pixels verdes**. Isso é **normal** e esperado.

#### 🔌 Conecte um **teclado USB** na porta da TV Box para facilitar a navegação.

---

## 📄 Etapa 3: Navegar no Multitool

### Instruções passo a passo

1. Use a **seta para baixo** até o fim do contrato e pressione **Enter**.

2. No menu de opções, selecione:

   - **3. Erase flash** → pressione **Enter** e aguarde.
   - Após sucesso, pressione **Enter** para continuar.
   - **5. Burn image to flash** → pressione **Enter**.
   - Selecione o **device** → pressione **Enter**.
   - Selecione a **imagem** → pressione **Enter**.
   - Aguarde a **gravação**.
   - Ao final, pressione **Enter** no botão **OK**.

3. Volte ao menu e selecione:

   - **7. Shutdown**


---


## 🔌 Etapa 4: Preparar para o boot do Armbian

### Passos para inicialização

1. **Remova os seguintes itens da TV Box:**
   - Fonte da tomada
   - Teclado USB
   - **Cartão SD**

#### ⚠️⚠️⚠️ Remover o cartao irá manter o multitool e armbian no cartao para utilizar em outra tv box, caso nao remova-o, o armbian utilizará como um disco com ponto de montagem. ⚠️⚠️⚠️


2. **Insira o cabo de rede RJ45** na porta Ethernet da TV Box.

3. **Reconecte o teclado** na porta usb.

3. **Reconecte a fonte de energia** para ligar a TV Box.

⏳ **Aguarde o carregamento do Armbian.**

---


## ⌨️ Etapa 5: Configuração inicial no terminal

1. Conecte o **teclado USB** à TV Box.
2. Siga os **passos exibidos na tela**.
3. Ao final, você verá uma **tela de login** semelhante à de sistemas Linux.

---

## 🔐 Etapa 7: Acesso via SSH e ajustes finais

Após reiniciar o dispositivo:

1. Faça login com seu **usuário e senha**.
2. Acesse via **SSH** usando o comando:

```bash
ssh usuario@ip-local
```

---


## 🔓 Etapa 8: Configurar Autologin
Essa parte e necessaria para quando ocorrer reboot do sistema.

### 📁 Criar diretório e editar arquivo de configuração

Execute os comandos abaixo no terminal para configurar o login automático:


```bash
sudo mkdir -p /etc/systemd/system/getty@tty1.service.d
sudo nano /etc/systemd/system/getty@tty1.service.d/autologin.conf
```

### 📄 Conteudo do arquivo 

#### Coloque o nome do seu usuario.

```bash
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin seu-usuario --noclear %I $TERM
```


---

## ✅ Etapa 9: Finalização

Agora você pode:

- **Desligar** o dispositivo
- **Movê-lo** para junto do roteador com patch cord de classificação cat6
- **Ligá-lo novamente**

🔁 O **login será automático** e o acesso poderá ser feito via **SSH**.


--- 


## 🛡️ Recomendações finais

- 🔒 **Mude a senha** para algo mais forte e seguro.
- 🏷️ **Renomeie o dispositivo** para facilitar sua identificação na rede.


--- 


## 💖 Apoie Nosso Projeto 💖

Se você achou esta documentação útil, considere apoiar nosso trabalho tornando-se um patrocinador.

- [☕ PayPal](https://www.paypal.com/donate/?business=9BBJLYB3U435C&no_recurring=0&currency_code=BRL)  
- [💳 MercadoPago](https://link.mercadopago.com.br/doarparalue)  
- [₿ Bitcoin] Ou envie um satoshi para este endereço de carteira:  
  **bc1q6j9ca23ekw8t5px30lg9t8qds6yqrhazhp0y99**


---


Feito! Sua TV Box com RK3229 está pronta para rodar Armbian com acesso remoto via SSH. 😎



---

## 🐞 Encontrou um Bug?

Se você encontrou algum erro, comportamento inesperado ou tem sugestões de melhoria, sua contribuição é muito bem-vinda!

### 📬 Como reportar um problema

1. Acesse a seção de [Issues no GitHub](https://github.com/SEU_REPOSITORIO/issues).
2. Clique em **"New Issue"**.
3. Descreva detalhadamente:
   - O que você estava tentando fazer
   - O que aconteceu de errado
   - Passos para reproduzir o problema
   - Prints de tela ou logs, se possível

🔧 Isso nos ajuda a melhorar continuamente o projeto e oferecer uma experiência cada vez melhor para todos!

Agradecemos pelo seu apoio e colaboração 💙
