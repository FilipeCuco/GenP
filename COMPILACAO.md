# Guia de Compilação do GenP

Este documento fornece instruções detalhadas para compilar o GenP a partir do código-fonte. Siga estas etapas para construir o executável do programa.

## Índice

1. [Requisitos do Sistema](#requisitos-do-sistema)
2. [Preparação do Ambiente](#preparação-do-ambiente)
3. [Processo de Compilação](#processo-de-compilação)
4. [Solução de Problemas](#solução-de-problemas)
5. [Estrutura do Projeto](#estrutura-do-projeto)

## Requisitos do Sistema

- Windows 10 ou superior (64 bits)
- PowerShell 5.0 ou superior
- Privilégios de administrador
- Conexão com a internet (para download de dependências)
- Aproximadamente 50 MB de espaço em disco

## Preparação do Ambiente

Antes de iniciar o processo de compilação, verifique se você tem as permissões necessárias e se a política de execução do PowerShell está configurada corretamente.

### Verificação da Política de Execução do PowerShell

1. Abra o PowerShell como administrador
2. Execute o comando:
   ```powershell
   Get-ExecutionPolicy -Scope CurrentUser
   ```
3. Se o resultado for "Restricted" ou "AllSigned", execute:
   ```powershell
   Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
   ```

## Processo de Compilação

O projeto inclui scripts automatizados que facilitam o processo de compilação. Você pode escolher entre dois métodos:

### Método 1: Usando o Arquivo Batch (Recomendado)

1. Navegue até a pasta `Source Code` no diretório do projeto
2. Clique com o botão direito em `run_build.bat`
3. Selecione "Executar como administrador"
4. Siga as instruções na tela

### Método 2: Usando o PowerShell Diretamente

1. Abra o PowerShell como administrador
2. Navegue até a pasta `Source Code` no diretório do projeto
3. Execute o comando:
   ```powershell
   .\build.ps1
   ```
4. Siga as instruções na tela

## O Que Acontece Durante a Compilação

O script de compilação realiza as seguintes operações:

1. **Verificação do ambiente**:
   - Verifica se o script está sendo executado como administrador
   - Verifica a política de execução do PowerShell
   - Verifica a existência dos diretórios necessários

2. **Preparação das dependências**:
   - Baixa e instala o AutoIt (se não estiver presente)
   - Baixa e instala o SciTE para AutoIt (se não estiver presente)
   - Copia o UPX para o diretório de compilação
   - Verifica e prepara o arquivo wintrust.dll modificado

3. **Compilação do código**:
   - Compila o script AutoIt (GenP-3.6.9.au3) usando o AutoIt3Wrapper
   - Aplica compressão UPX ao executável gerado
   - Copia os arquivos necessários para o diretório de lançamento

4. **Finalização**:
   - Verifica se a compilação foi bem-sucedida
   - Exibe o caminho para o executável gerado

## Solução de Problemas

### Erro de Permissão

**Problema**: Mensagem de erro indicando falta de permissões administrativas.

**Solução**: Certifique-se de executar o script como administrador. Clique com o botão direito no arquivo batch ou no PowerShell e selecione "Executar como administrador".

### Falha no Download de Dependências

**Problema**: O script não consegue baixar o AutoIt ou o SciTE.

**Solução**: 
- Verifique sua conexão com a internet
- Tente baixar manualmente os arquivos dos links fornecidos no script
- Coloque os arquivos baixados na pasta `Source Code` e execute o script novamente

### Erro na Compilação do AutoIt

**Problema**: O AutoIt3Wrapper falha ao compilar o script.

**Solução**:
- Verifique se o AutoIt e o SciTE foram instalados corretamente
- Verifique se há erros de sintaxe no arquivo GenP-3.6.9.au3
- Tente reinstalar o AutoIt e o SciTE

## Estrutura do Projeto

```
GenP/
├── Release/                  # Diretório onde o executável compilado será colocado
└── Source Code/
    ├── GenP/                 # Código-fonte principal
    │   ├── GenP-3.6.9.au3    # Script AutoIt principal
    │   ├── Skull.ico         # Ícone do aplicativo
    │   └── config.ini        # Arquivo de configuração
    ├── UPX/                  # Ferramenta de compressão de executáveis
    │   └── upx.exe           # Executável UPX
    ├── WinTrust/             # Componentes para modificação do wintrust.dll
    │   ├── patch_wintrust.ps1 # Script para modificar o wintrust.dll
    │   └── wintrust.dll      # Arquivo wintrust.dll original
    ├── build.ps1             # Script PowerShell de compilação
    └── run_build.bat         # Script batch para iniciar a compilação
```

## Notas Importantes

- O processo de compilação requer conexão com a internet para baixar as dependências necessárias (AutoIt e SciTE).
- O executável compilado será colocado na pasta `Release`.
- O script de compilação cria um ambiente de compilação temporário em `C:\GenP-BuildEnv` por padrão. Este caminho pode ser alterado no script `build.ps1` se necessário.
- Todos os logs de compilação são armazenados na pasta `Logs` dentro do diretório `Source Code`.

---

**Nota**: Este guia foi criado apenas para fins educacionais. A compilação e uso do GenP podem violar os termos de serviço de certos softwares. Use por sua própria conta e risco.