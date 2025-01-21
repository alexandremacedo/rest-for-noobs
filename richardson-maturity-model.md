# Níveis de Maturidade de Richardson
Os níveis de maturidade de Richardson são utilizados para analisar o grau de implementação dos princípios REST em uma API.

## Nível 0: The Swamp of POX
No nível 0, a API não implementa os princípios fundamentais do REST.
- Usa recursos e verbos de maneira incorreta.
- Centraliza chamadas em um único endpoint.
Exemplo: Uma API que possui apenas um endpoint genérico, como /api, onde todas as operações são realizadas sem distinção de recursos.

## Nível 1: Resources
No nível 1, os recursos são expostos por meio de URIs específicas, tirando a API do nível 0.
- Representação de entidades através de URIs claras.
- Exemplos de endpoints para uma coleção de produtos:
  - /products para listar ou criar produtos.
  - /products/1 para acessar um produto específico.
Boas práticas:
- As operações nos recursos devem ser diferenciadas por verbos HTTP (como GET, POST, etc.).

## Nível 2: HTTP Verbs - O mais complexo
No nível 2, a API faz bom uso dos verbos HTTP, atribuindo responsabilidades claras para cada operação. Isso facilita o uso e a compreensão dos recursos.
### Lista de verbos
| **Verbo**   | **Objetivo**                        | **Idempotente** | **Safe** |
|-------------|-------------------------------------|----------------|---------|
| `GET`       | Recuperar recursos                  | Sim            | Sim     |
| `POST`      | Criar um recurso                    | Não            | Não     |
| `PUT`       | Substituir recurso completamente    | Sim            | Não     |
| `PATCH`     | Atualizar parcialmente um recurso   | Sim            | Não     |
| `DELETE`    | Remover um recurso                  | Sim            | Não     |
| `HEAD`      | Obter cabeçalhos                    | Sim            | Sim     |
| `OPTIONS`   | Verificar métodos permitidos        | Sim            | Sim     |
| `TRACE`     | Depurar requisição                  | Sim            | Não     |
| `CONNECT`   | Estabelecer túnel                   | Não            | Não     |

Boas Práticas:
- Evite endpoints como DELETE /products (para deletar o último produto da lista sem especificidade).
- Prefira algo como POST /products/remove-last-item para operações mais seguras e intencionais.
- Ou DELETE /products/:productId
- É mais eficiente cachear verbos idempotentes como GET e PUT.
Nota: O verbo PATCH, criado em 2010 por Roy Fielding.

### Interface Uniforme e Status Codes
#### Status Codes Mais Utilizados:
- 200: Sucesso geral.
- 201: Recurso criado.
- 204: Recurso deletado sem conteúdo de retorno.
- 400: Erro do cliente.
- 500: Erro do servidor.

### Content Negotiation
- Use os cabeçalhos Content-Type e Accept para validar tipos de mídia/arquivos.
- Middlewares são úteis para validar os tipos de mídia permitidos.

### OPTIONS e CORS
- O método OPTIONS retorna os metadados do recurso, como métodos permitidos.
- CORS (Cross-Origin Resource Sharing):
  - Garante segurança na comunicação entre sistemas.
  - Utiliza cabeçalhos como Access-Control-Headers e Access-Control-Origin.
  - Realiza pré-verificações (pre-flight) antes de operações como POST.
  - Ajuda a prevenir ataques CSRF.

## Nível 3: Hypermedia Controls
No nível 3, a API retorna links para navegar entre recursos relacionados, utilizando hipermídia como parte da resposta.

Exemplo de HATEOAS:
```json
{
  "file": {
    "id": 123,
    "name": "relatorio.pdf",
    "links": [
      { "rel": "self", "href": "/files/123" },
      { "rel": "download", "href": "/files/123/download" }
    ]
  }
}
```
Formatos Comuns:
- JSON HAL (application/hal+json): Um formato popular, mas ainda não amplamente adotado.
- Seguir a RFC de hyperlinks já é suficiente para implementar controles de hipermídia corretamente.
- Referência de Implementação
  - [API Tools Laminas](https://api-tools.getlaminas.org/)



