# Ubuntu 24.04 em máquina virtual

[Início](../README.md) · Próximo: [ROS 2](ros2-jazzy.md)

A VM executa Ubuntu dentro do Windows, usando um arquivo como disco. É uma boa entrada para aulas de ROS 2; o desempenho do Gazebo depende da GPU virtual e pode ser insuficiente em alguns computadores.

## Criar a VM

Use o [VirtualBox oficial](https://www.virtualbox.org/wiki/Downloads) e a [ISO Ubuntu Desktop 24.04 amd64](https://releases.ubuntu.com/24.04/). Este roteiro considera host Intel/AMD.

1. Instale o VirtualBox para Windows e crie uma máquina chamada `Gaia-Ubuntu24`.
2. Selecione a ISO. Para acompanhar as telas, escolha instalação manual/interativa em vez da opção automática, quando disponível.
3. Como ponto de partida do laboratório, atribua **8 GB de RAM, 4 vCPUs e disco virtual dinâmico de 80 GB**. Não atribua toda a memória/CPU do host; se ele tem pouca RAM, reduza e espere limitações.
4. Mantenha rede **NAT** para baixar os pacotes. Inicialmente todos os nós ROS rodam dentro da mesma VM.
5. Nas configurações de tela, use o controlador gráfico Linux sugerido pelo VirtualBox (VMSVGA) e teste aceleração 3D. A disponibilidade depende do host.
6. Inicie a VM e siga a instalação do Ubuntu. A opção de usar todo o disco é apropriada **somente para o disco virtual vazio que acabou de criar**, sem acesso a discos físicos.
7. Reinicie a VM e retire a ISO da unidade virtual.

A [aula oficial Ubuntu/VirtualBox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox) mostra a criação, instalação e integração do sistema convidado. Os valores de RAM/disco acima são uma sugestão do Gaia.

## Preparar para o laboratório

Dentro do Ubuntu:

```bash
cat /etc/os-release
sudo apt update
sudo apt upgrade
```

Instale as **Guest Additions** conforme o guia do VirtualBox para melhorar resolução e integração. Tire um snapshot após concluir as atualizações; depois tire outro quando ROS 2 estiver funcionando. Snapshot não substitui backup fora do disco da VM.

Mantenha os workspaces ROS em `~/gaia_ws`, no disco Linux da VM. Pastas compartilhadas com Windows podem dificultar permissões, links simbólicos e compilação.

## Rede, USB e gráficos

| Uso | Orientação |
| --- | --- |
| Talker/listener dentro da VM | NAT normalmente basta |
| ROS entre VM e outro PC/robô | Rede bridge pode ser necessária; confira multicast, firewall e mesmo domínio ROS |
| BusLinker USB | Selecione o dispositivo no menu USB da VM; host e convidado não podem usá-lo simultaneamente |
| Gazebo lento/tela preta | Verifique aceleração 3D e drivers; use o modo sem janela do laboratório |
| Host sem virtualização disponível | Confira VT-x/AMD-V no firmware e conflitos/configuração do hipervisor |

Não use uma VM com atrasos imprevisíveis para validar equilíbrio do robô real. Para aulas, medir taxas e gravar dados, ela continua útil.

Resultado esperado: Ubuntu 24.04 abre, rede funciona e o terminal está disponível. Continue em [ROS 2 Jazzy](ros2-jazzy.md).
