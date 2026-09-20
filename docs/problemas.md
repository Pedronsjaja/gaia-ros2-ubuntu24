# Problemas frequentes

[Início](../README.md)

| Sintoma | Conferir |
| --- | --- |
| Instalador não mostra Windows | BitLocker, UEFI, SSD e RST; não substituir por “apagar disco” |
| Windows pede recuperação depois do boot | Use a chave de recuperação guardada; não formate para contornar |
| Ubuntu na VM não tem rede | Adaptador virtual habilitado e NAT; confira rede do Windows |
| `ros2: command not found` | `source /opt/ros/jazzy/setup.bash` no terminal atual |
| Pacote ros-jazzy não encontrado | Ubuntu noble, Universe e instalação do ros2-apt-source |
| Dependências de ros-dev-tools incompatíveis | Atualizações do Ubuntu e suites noble-updates/noble-backports |
| Falha de assinatura/repositório duplicado | Confira fontes ROS existentes e guia oficial atual; não desative verificação de assinatura |
| Erro no download via API GitHub | Rede, limite da API ou resposta inválida; repita depois, sem instalar arquivo vazio |
| Talker funciona, listener não recebe | Mesmo domínio, descoberta e terminal; ambos dentro da mesma VM para o primeiro teste |
| Mudou domínio e lista de nós está estranha | Encerre exemplos, `ros2 daemon stop`, reabra com o mesmo ambiente |
| ROS funciona no host mas não em outro PC | LOCALHOST restringe descoberta; planeje rede/sub-rede, multicast, domínio e firewall |
| RViz/Gazebo lento ou preto | Drivers, GPU virtual/Guest Additions; compare com execução sem GUI |
| `externally-managed-environment` | Use pacotes apt/rosdep para o ROS; não altere o Python global com pip |
| Máquina fica sem memória na compilação | Reduza paralelismo, feche aplicativos e aumente recursos se possível |

Para comunicar o problema, registre sistema, etapa, comando completo e últimas linhas do erro. Logs de ROS normalmente ficam em `~/.ros/log`; logs de compilação no `log/` do workspace.

Não confunda um problema de instalação com um problema do modelo: primeiro teste talker/listener; depois RViz; depois Gazebo; por último os controladores do robô.
