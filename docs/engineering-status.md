# Ficha reproduzivel do ambiente

Antes de comparar desempenho, registrar em um arquivo de ensaio: commit do
guia, data, Ubuntu/kernel (`lsb_release -a`, `uname -r`), ROS_DISTRO,
arquitetura (`uname -m`), ambiente VM ou nativo, recursos atribuidos, Gazebo,
versoes de pacotes e origem da instalacao. Valores desta ficha: UNKNOWN.
Nao colocar tokens, enderecos privados ou identificadores pessoais no log.

Sequencia de aceite: terminal novo → source /opt/ros/jazzy/setup.bash →
`ros2 doctor --report` → talker/listener em dois terminais → workspace colcon
minimo → exemplo GAIA. Salvar comando, codigo de retorno e comportamento
observado. Mensagem recebida demonstra comunicacao naquele ambiente, nao
determinismo temporal. Nao executar comandos de ROS no PowerShell Windows.

ALTO: fechar instalacao reproduzivel em uma maquina identificada; MEDIO:
medir uso de recursos e latencia VM/nativo sob a mesma carga; BAIXO:
automatizar apenas etapas estaveis. Hipotese de comparacao: virtualizacao
altera latencia; manter carga, taxa, QoS e versoes constantes. Medicoes:
NOT_MEASURED. Nao concluir que dual boot sera mais rapido sem dados.

Para entender esta implementacao: estude shell/source, overlay/underlay,
DDS e QoS. Desafio: explique por que dois terminais com ROS_DOMAIN_ID
diferentes nao participam do mesmo dominio de descoberta.

Referencia principal: [instalacao oficial Jazzy no Ubuntu](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html).
O guia oficial orienta dependencias; nao confirma sua configuracao fisica.
