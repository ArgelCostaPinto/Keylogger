# Projeto Keylogger Educacional em Python

Este projeto consiste em dois scripts de keylogger desenvolvidos em Python para fins educacionais. O objetivo é demonstrar como a captura de eventos de teclado pode ser implementada e como os dados podem ser armazenados ou transmitidos.

> [!WARNING]
> **Aviso Legal e Ético:** Este software foi criado exclusivamente para fins de estudo e aprendizado. O uso de keyloggers para monitorar um computador sem o consentimento explícito do proprietário é ilegal na maioria das jurisdições e constitui uma grave violação de privacidade. O autor não se responsabiliza pelo mau uso deste código.

---

## Funcionalidades

O projeto oferece duas abordagens para o registro de teclas:

1.  **Log Local (`keylogger.pyw`):** Captura as teclas digitadas e as salva em um arquivo de texto (`log.txt`) na mesma pasta do script. A extensão `.pyw` permite que ele seja executado em segundo plano no Windows, sem abrir uma janela de console.
2.  **Envio por E-mail (`keylogger_email.py`):** Captura as teclas e as envia para um endereço de e-mail especificado em intervalos de tempo regulares.

Ambos os scripts são projetados para gerar logs limpos, ignorando teclas modificadoras como `Shift`, `Ctrl` e `Alt`.

---

## Arquivos do Projeto

### `keylogger.pyw`

Este script utiliza a biblioteca `pynput` para escutar os eventos do teclado.

- **Operação:**
  - Ao ser executado, ele monitora todas as teclas pressionadas.
  - Caracteres normais são salvos diretamente.
  - Teclas especiais como `Espaço`, `Enter` e `Backspace` são formatadas para melhor legibilidade.
  - Os dados são anexados ao arquivo `log.txt`.

### `keylogger_email.py`

Além da `pynput`, este script usa as bibliotecas `smtplib` e `threading` para gerenciar o envio de e-mails.

- **Operação:**
  - As teclas digitadas são armazenadas em uma variável em memória.
  - A cada `30` segundos (configurável na variável `INTERVALO_ENVIO`), o conteúdo registrado é enviado para o e-mail de destino.
  - As credenciais de e-mail (remetente e senha) estão definidas diretamente no código para fins de demonstração.
  - Utiliza `atexit` para tentar enviar os logs restantes quando o script é encerrado.

---

## Como Usar

### 1. Pré-requisitos

- Python 3.x instalado.
- Instalar a biblioteca `pynput`:
  ```bash
  pip install pynput
  ```

### 2. Configuração (Apenas para `keylogger_email.py`)

Para que o envio de e-mail funcione, você precisa de uma **Senha de App** da sua conta Google. A sua senha principal não funcionará se a verificação em duas etapas estiver ativa.

1.  **Ative a Verificação em Duas Etapas** na sua Conta do Google.
2.  Acesse Senhas de app e gere uma nova senha para "E-mail" em um "Computador Windows".
3.  O Google fornecerá uma senha de 16 caracteres.

Abra o arquivo `keylogger_email.py` e edite as seguintes linhas com suas informações:

```python
# Endereço de e-mail que enviará os logs
EMAIL_ORIGEM = "seu-email@gmail.com"

# Endereço de e-mail que receberá os logs
EMAIL_DESTINO = "email-destino@exemplo.com"

# Cole aqui a senha de app de 16 caracteres, SEM ESPAÇOS
SENHA_EMAIL = "suasenhadeappsemespacos"
```

> [!NOTE]
> A senha de e-mail presente no código-fonte (`keylogger_email.py`) foi invalidada após a publicação deste projeto para garantir a segurança da conta. Você **precisará** gerar e configurar sua própria Senha de App para que o script funcione.

### 3. Execução

- **Para salvar em arquivo local:**
  No Windows, basta dar um duplo clique no arquivo `keylogger.pyw`. Em outros sistemas, execute no terminal:
  ```bash
  python keylogger.pyw
  ```

- **Para enviar por e-mail:**
  Execute o script através do terminal:
  ```bash
  python keylogger_email.py
  ```

