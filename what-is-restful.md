# O que é RESTful
RESTful refere-se a uma boa implementação dos princípios do HTTP, REST e APIs, garantindo que os sistemas distribuídos sejam eficientes, escaláveis e fáceis de integrar.

## Características Principais
### Hypertext Driven
Uma API RESTful deve ser orientada por hipermídia, ou seja, as respostas devem fornecer links que permitam ao cliente navegar pelos recursos disponíveis. Isso é conhecido como HATEOAS (Hypermedia as the Engine of Application State).
Benefícios:
- Reduz o acoplamento entre cliente e servidor.
- Fornece ao cliente informações claras sobre como interagir com a API.

Exemplo de resposta orientada por hipermídia:
```json
{
  "usuario": {
    "id": 123,
    "nome": "João Silva",
    "links": [
      { "rel": "self", "href": "/usuarios/123" },
      { "rel": "pedidos", "href": "/usuarios/123/pedidos" }
    ]
  }
}
```
## Problem Details
Para lidar com erros e problemas de forma consistente, APIs RESTful utilizam o padrão Problem Details for HTTP APIs (RFC 7807). Este formato padroniza as respostas de erro, tornando-as mais claras e amigáveis.

Exemplo de resposta de erro no padrão Problem Details:
```json
{
  "type": "https://example.com/problemas/usuario-nao-encontrado",
  "title": "Usuário não encontrado",
  "status": 404,
  "detail": "O usuário com o ID 123 não foi encontrado no sistema.",
  "instance": "/usuarios/123"
}
```
Campos principais:
- type: URL descrevendo o tipo do problema.
- title: Descrição curta do problema.
- status: Código de status HTTP.
- detail: Detalhe específico do problema.
- instance: URI específica do recurso relacionado ao problema.
