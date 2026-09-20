# Instalar ROS 2 Jazzy no Ubuntu 24.04

[Início](../README.md) · Próximo: [primeiros testes](primeiros-passos.md)

Execute no **Bash do Ubuntu**, após instalar o sistema por dual boot ou VM. ROS 2 organiza programas robóticos que trocam mensagens; o simulador será instalado depois.

## 1. Conferir sistema e idioma

```bash
cat /etc/os-release
dpkg --print-architecture
locale
```

Espere Ubuntu **24.04/noble** e, neste roteiro, `amd64`. Se a versão for diferente, pare e escolha a documentação correspondente. Se `locale` já mostra UTF-8, mantenha seu idioma; caso contrário:

```bash
sudo apt update
sudo apt install locales
sudo locale-gen en_US.UTF-8
sudo update-locale LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

## 2. Habilitar os repositórios

```bash
sudo apt update
sudo apt install software-properties-common curl python3
sudo add-apt-repository universe
```

O pacote oficial `ros2-apt-source` instala a configuração do repositório e suas chaves. Baixe a versão mais recente desse pacote para **noble**:

```bash
ROS_APT_SOURCE_VERSION=$(curl -fsSL https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | python3 -c 'import json,sys; print(json.load(sys.stdin)["tag_name"])')
test -n "$ROS_APT_SOURCE_VERSION"
curl -fL -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.noble_all.deb"
sudo dpkg -i /tmp/ros2-apt-source.deb
```

Execute um bloco de cada vez e só prossiga se os comandos terminarem sem erro. Isso adapta o [procedimento oficial de repositórios](https://github.com/ros2/ros2_documentation/blob/jazzy/source/Installation/_Apt-Repositories.rst) à versão escolhida pela equipe. Não use instruções antigas com chaves/repositórios de outra distribuição.

## 3. Instalar ROS e ferramentas

```bash
sudo apt update
sudo apt upgrade
sudo apt install ros-jazzy-desktop ros-dev-tools
```

O pacote Desktop inclui RViz e exemplos. `ros-dev-tools` fornece ferramentas de desenvolvimento como colcon/rosdep/vcs. Se houver conflito de dependências, confira se `/etc/apt/sources.list.d/ubuntu.sources` habilita `noble-updates` e `noble-backports`, conforme a [documentação oficial Jazzy](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html).

Inicialize o rosdep apenas se ainda não estiver configurado:

```bash
if [ ! -f /etc/ros/rosdep/sources.list.d/20-default.list ]; then
  sudo rosdep init
fi
rosdep update
```

`rosdep` consulta quais dependências um pacote precisa e como instalá-las. Rode `rosdep update` como usuário normal.

## 4. Carregar o ambiente

Em **cada terminal**:

```bash
source /opt/ros/jazzy/setup.bash
export ROS_DOMAIN_ID=42
export ROS_AUTOMATIC_DISCOVERY_RANGE=LOCALHOST
echo "$ROS_DISTRO"
```

O resultado deve ser `jazzy`. Domínio 42 e descoberta local são uma convenção para as aulas individuais: permitem testar os nós do mesmo PC/VM sem misturar robôs da rede. Quando a equipe for distribuir nós entre computadores, o domínio deve coincidir, a descoberta precisa permitir a rede e as interfaces devem ser configuradas conscientemente.

Para carregar somente a instalação Jazzy automaticamente em novos terminais:

```bash
grep -qxF 'source /opt/ros/jazzy/setup.bash' ~/.bashrc || echo 'source /opt/ros/jazzy/setup.bash' >> ~/.bashrc
```

Não acrescente automaticamente workspaces experimentais ao bashrc: isso dificulta saber quais pacotes estão em uso.

## 5. Testar antes de instalar simuladores

**Terminal A:**

```bash
source /opt/ros/jazzy/setup.bash
export ROS_DOMAIN_ID=42
export ROS_AUTOMATIC_DISCOVERY_RANGE=LOCALHOST
ros2 run demo_nodes_cpp talker
```

**Terminal B:**

```bash
source /opt/ros/jazzy/setup.bash
export ROS_DOMAIN_ID=42
export ROS_AUTOMATIC_DISCOVERY_RANGE=LOCALHOST
ros2 run demo_nodes_py listener
```

Espere mensagens `Publishing` no primeiro e `I heard` no segundo. Encerre com Ctrl+C. Essa sequência é o [teste oficial das APIs C++/Python](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html).

Agora avance para [primeiros passos](primeiros-passos.md) e para o [simulador do humanoide](https://github.com/Pedronsjaja/gaia-humanoid-robot/tree/main/docs/simulacao).

## Python do ROS e Python da bancada

Os pacotes ROS do Ubuntu usam o Python do sistema. Comece com o ambiente ROS carregado, sem Conda e sem a `.venv` da bancada LX-225. Não use `sudo pip` nem `--break-system-packages` para contornar erros de instalação. A integração ROS/LX-225 será um pacote separado, com dependências declaradas.
