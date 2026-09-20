# Primeiros passos da equipe

[Início](../README.md)

## Vocabulário com exemplos do Gaia

| Termo | Significado | Exemplo futuro no robô |
| --- | --- | --- |
| Nó | Programa participante | Ler a IMU |
| Tópico | Fluxo de mensagens | Publicar inclinação e aceleração |
| Mensagem | Estrutura dos dados | JointState com nomes e posições em radianos |
| Serviço | Solicitação com resposta | Consultar uma configuração |
| Ação | Objetivo demorado com feedback/cancelamento | Executar trajetória de uma junta |
| Parâmetro | Configuração do nó | Limite, taxa e caminho de arquivo |
| Launch | Inicia um conjunto de processos | Simulador + modelo + controladores |
| TF | Relações entre sistemas de coordenadas | Câmera em relação ao tronco |
| Workspace | Pasta de fontes e compilação | ~/gaia_ws |
| RViz | Visualizador dos dados ROS | Mostrar juntas e sensores |
| Gazebo | Simulador físico e de sensores | Gerar contatos com o chão |

ROS 2 não decide sozinho o que o robô deve fazer: conecta os programas que implementam percepção, decisão e controle.

## Exercício após talker/listener

Com os dois exemplos funcionando, abra um terceiro terminal com o mesmo ambiente/domínio:

```bash
source /opt/ros/jazzy/setup.bash
export ROS_DOMAIN_ID=42
export ROS_AUTOMATIC_DISCOVERY_RANGE=LOCALHOST
ros2 node list
ros2 topic list
ros2 topic info /chatter
ros2 topic echo /chatter --once
ros2 interface show std_msgs/msg/String
```

Identifique os dois nós, o tópico e o campo de texto da mensagem. Depois feche os exemplos e abra `rviz2`: uma cena vazia é normal, ainda não carregamos um robô.

## Workspace

`src/` guarda fontes, `build/` artefatos de compilação, `install/` pacotes prontos e `log/` registros. Após compilar, `source install/setup.bash` torna os pacotes visíveis naquele terminal. Não envie build/install/log ao Git.

O [tutorial do OP3 no Gaia](https://github.com/Pedronsjaja/gaia-humanoid-simulation/tree/main/docs/simulacao) cria o workspace real. Não é necessário inventar um pacote agora.

## Ficha de validação por computador

Copie para o registro interno da equipe:

```text
Pessoa/data:
Computador, CPU, RAM e GPU:
Dual boot ou VM (RAM/vCPU atribuídas):
Ubuntu:
ROS_DISTRO:
Talker/listener: passou/falhou + mensagem
RViz abriu:
Observações:
```

Meta da primeira aula: cada pessoa consegue instalar, testar e explicar o caminho de uma mensagem. Próxima meta: inserir o OP3 no Gazebo e observar o estado de uma junta.

Referências: [conceitos ROS 2](https://docs.ros.org/en/jazzy/Concepts.html), [tutorial de tópicos](https://docs.ros.org/en/jazzy/Tutorials/Beginner-CLI-Tools/Understanding-ROS2-Topics/Understanding-ROS2-Topics.html) e [RViz](https://docs.ros.org/en/jazzy/Tutorials/Intermediate/RViz/RViz-Main.html).
