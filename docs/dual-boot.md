# Ubuntu 24.04 em dual boot com Windows

[Início](../README.md) · Próximo: [ROS 2](ros2-jazzy.md)

Dual boot instala dois sistemas no computador; você escolhe um ao iniciar. A simulação usa CPU/GPU diretamente, mas a instalação modifica o armazenamento.

## Antes de começar

Faça backup dos arquivos em outro dispositivo e guarde a chave de recuperação do BitLocker fora do computador. Identifique o modelo e a capacidade do SSD. Separe um pendrive vazio de 16 GB ou mais e a [ISO Desktop 24.04 amd64](https://releases.ubuntu.com/24.04/).

No Windows, confira **Gerenciamento de Disco** e reserve, como planejamento do Gaia, cerca de 100 GB para Ubuntu e simulações. Se necessário, use **Diminuir Volume** na partição de dados/Windows para criar espaço **não alocado**. Não exclua partições EFI, recuperação ou Windows. O espaço disponível para redução depende dos arquivos existentes.

Se houver BitLocker e o instalador bloquear a instalação ao lado do Windows, siga a [orientação Canonical para BitLocker](https://ubuntu.com/tutorials/install-ubuntu-desktop#12-additional-installing-ubuntu-alongside-windows-with-bitlocker): desligar a criptografia exige aguardar a descriptografia; apenas suspender a proteção não é o mesmo procedimento. Em computador institucional, a configuração pode depender da administração de TI.

## Instalar

1. Grave a ISO no pendrive com o [balenaEtcher](https://etcher.balena.io/), conferindo o dispositivo de destino. A gravação apaga o pendrive.
2. Reinicie e abra o menu de boot do fabricante. Escolha a entrada UEFI do pendrive.
3. Use **Try Ubuntu** para testar teclado, rede, tela e touchpad.
4. Abra o instalador, selecione idioma, teclado e instalação interativa. Confira rede e drivers oferecidos.
5. Na tela do disco, escolha **instalar ao lado do Windows Boot Manager**, quando disponível. Confira o espaço destinado a cada sistema.
6. Revise o resumo: Windows deve permanecer e apenas o espaço previsto deve ser usado. **Não escolha “apagar disco” no SSD que contém o Windows.**
7. Termine a configuração de usuário/fuso e reinicie, retirando o pendrive quando solicitado.

As telas e o particionamento automático são descritos no [tutorial oficial Ubuntu](https://ubuntu.com/tutorials/install-ubuntu-desktop). Se a opção de instalar ao lado não aparecer, não improvise exclusões: confira BitLocker, UEFI e detecção do SSD antes de avançar. Para alerta Intel RST, siga a [orientação específica](https://help.ubuntu.com/rst); mudar o modo de armazenamento sem preparar o Windows pode impedir seu boot.

## Depois de instalar

Teste o boot dos **dois sistemas**, pelo menu inicial ou seleção UEFI. No Ubuntu, abra o terminal:

```bash
cat /etc/os-release
sudo apt update
sudo apt upgrade
```

Confira `24.04` e `noble`. Reinicie se solicitado pelas atualizações. Em **Software e Atualizações → Drivers adicionais**, confira a GPU; faça a configuração MOK quando solicitada pelo instalador de drivers com Secure Boot. Não desative Secure Boot indiscriminadamente.

Resultado esperado: Ubuntu e Windows iniciam normalmente, a rede funciona e a tela está utilizável. Continue em [instalar ROS 2 Jazzy](ros2-jazzy.md).
