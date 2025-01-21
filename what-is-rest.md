# O que é REST
REST (Representational State Transfer) é um estilo arquitetural que guia a interação em sistemas distribuídos de hipermídia. Ele organiza os componentes de uma aplicação e define como eles devem interagir para modificar o estado da aplicação, independentemente do formato de dado utilizado (como XML ou JSON). Antes de ser chamado de REST, era conhecido como HTTP Object Model.

## Princípios Fundamentais do REST
### Cliente-Servidor
A arquitetura REST separa as responsabilidades entre cliente e servidor:
- Cliente: Focado na interface do usuário, responsável por exibir informações e interagir com o usuário.
- Servidor: Gerencia a lógica de negócio e armazenamento de dados, sem precisar conhecer a interface do cliente.
Essa separação permite maior flexibilidade e facilita a evolução independente de ambos os lados.

### Stateless
No REST, o estado da comunicação cliente-servidor não é mantido. Cada requisição deve conter todas as informações necessárias para que o servidor processe e responda corretamente.
#### Benefícios:
- Escalabilidade: facilita o uso de balanceadores de carga, cache e proxies.
- Independência: clientes e servidores não dependem de estados persistentes para operar.
Nota: Cookies podem quebrar o padrão stateless, pois introduzem dependências de estado.

### Cache
As respostas do servidor podem ser armazenadas em cache por intermediários, como proxies e clientes. Isso otimiza o uso da rede e melhora a eficiência geral do sistema.
Para que o cache funcione corretamente, é necessário:
- Definir cabeçalhos HTTP como Cache-Control.
- Garantir que os dados armazenados em cache sejam válidos e consistentes.

### Interface Uniforme
A comunicação entre componentes de um sistema REST segue uma interface uniforme, tornando-a:
- Consistente: Todas as interações têm uma estrutura previsível.
- Auto descritiva: Os recursos e suas representações explicam seu próprio propósito e uso, facilitando a integração.
Exemplo de boas práticas:
- Uso de verbos HTTP padrão como GET, POST, PUT, DELETE.
- URLs claras e orientadas a recursos (e.g., /usuarios/123).

### Arquitetura em Camadas
O design em camadas permite que diferentes componentes sejam substituídos ou modificados sem impactar diretamente o cliente ou o servidor.
Benefícios:
- Modularidade: Facilita a introdução de proxies, servidores de cache e balanceadores de carga.
- Manutenção: A arquitetura pode ser atualizada ou escalada sem interromper o funcionamento geral.
