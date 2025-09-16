# Guia de Remoção Total do GenP

Este documento fornece instruções detalhadas para remover completamente o GenP e reverter todas as modificações feitas por ele no seu sistema. Siga estas etapas para restaurar a segurança e integridade do seu sistema operacional.

## Índice

1. [Preparação](#preparação)
2. [Restauração do wintrust.dll](#restauração-do-wintrustdll)
3. [Restauração do arquivo hosts](#restauração-do-arquivo-hosts)
4. [Remoção de regras de firewall](#remoção-de-regras-de-firewall)
5. [Desinstalação do GenP](#desinstalação-do-genp)
6. [Verificação do sistema](#verificação-do-sistema)
7. [Considerações finais](#considerações-finais)

## Preparação

Antes de iniciar o processo de remoção, feche todos os aplicativos Adobe e certifique-se de que você tem privilégios de administrador no seu sistema.

## Restauração do wintrust.dll

O componente mais crítico modificado pelo GenP é o arquivo wintrust.dll, que faz parte do sistema de verificação de segurança do Windows.

### Método 1: Usando o SFC (System File Checker)

1. Abra o Prompt de Comando como administrador
2. Execute o comando:
   ```
   sfc /scannow
   ```
3. Aguarde a conclusão do processo (pode levar alguns minutos)
4. Reinicie o computador

### Método 2: Restauração manual

Se o SFC não resolver o problema:

1. Abra o Prompt de Comando como administrador
2. Execute o comando DISM para preparar a restauração:
   ```
   DISM /Online /Cleanup-Image /RestoreHealth
   ```
3. Após a conclusão, execute novamente o SFC:
   ```
   sfc /scannow
   ```
4. Reinicie o computador

## Restauração do arquivo hosts

O GenP modifica o arquivo hosts para bloquear comunicações com servidores de ativação da Adobe.

1. Navegue até `C:\Windows\System32\drivers\etc\`
2. Se existir um arquivo `hosts.bak`, restaure-o substituindo o arquivo hosts atual
3. Caso não exista backup, crie um novo arquivo hosts com o seguinte conteúdo:

```
# Copyright (c) 1993-2009 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
#      102.54.94.97     rhino.acme.com          # source server
#       38.25.63.10     x.acme.com              # x client host

# localhost name resolution is handled within DNS itself.
#       127.0.0.1       localhost
#       ::1             localhost
```

## Remoção de regras de firewall

O GenP cria regras de firewall para bloquear comunicações com servidores Adobe.

1. Abra o menu Iniciar e pesquise por "Firewall do Windows com Segurança Avançada"
2. Clique em "Regras de Entrada" no painel esquerdo
3. Procure por regras com nomes relacionados a "Adobe", "GenP" ou "Creative Cloud"
4. Clique com o botão direito em cada regra encontrada e selecione "Excluir"
5. Repita o processo para "Regras de Saída"

## Desinstalação do GenP

1. Exclua a pasta de instalação do GenP
2. Verifique e remova quaisquer atalhos no menu Iniciar ou na área de trabalho
3. Limpe arquivos temporários:
   - Pressione `Win + R`, digite `%temp%` e pressione Enter
   - Exclua quaisquer pastas ou arquivos relacionados ao GenP

## Verificação do sistema

Após completar todas as etapas acima, é importante verificar se o sistema está íntegro:

1. Execute uma verificação completa com seu antivírus
2. Execute novamente o SFC para garantir que todos os arquivos do sistema estão íntegros:
   ```
   sfc /scannow
   ```

## Considerações finais

### Alternativas legais ao GenP

Considere estas alternativas legais e seguras:

- **Versões de avaliação oficiais**: A Adobe oferece períodos de avaliação para seus produtos
- **Planos com desconto**: Estudantes e educadores têm acesso a preços reduzidos
- **Alternativas de código aberto**: Existem várias alternativas gratuitas e de código aberto para software de criação

### Impacto na segurança

O uso de ferramentas como o GenP compromete seriamente a segurança do seu sistema ao:

- Modificar componentes críticos do sistema operacional
- Desativar mecanismos de segurança projetados para proteger seu computador
- Potencialmente expor seu sistema a vulnerabilidades

A melhor prática para manter seu sistema seguro é utilizar apenas software legítimo e licenciado adequadamente.

---

**Nota**: Este guia foi criado apenas para fins educacionais e para ajudar usuários a restaurar a integridade do sistema após o uso do GenP. Não endossamos a violação de direitos autorais ou termos de serviço de qualquer software.